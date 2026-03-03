# Specyfikacja Funkcjonalności

## FEATURE #1: Real-Time Analytics Dashboard

---

### 1.1 USER STORY

```gherkin
Jako: Content Manager szukający ROI na swoje artykuły
Chcę: Widzieć real-time metryki wydajności każdego artykułu
Aby: Móc optymalizować strategię content na podstawie danych

Kryteria Akceptacji:
- [ ] Główny Dashboard pokazuje top 3 artykuły po views
- [ ] Widzę views, unique visitors, bounce rate, time on page
- [ ] Widzę engagement metrics per platform (FB likes, LinkedIn impressions, X retweets)
- [ ] Mogę zobaczyć artykuł ranking w Google dla jego keywords
- [ ] Data jest aktualizowana co 6 godzin z Google Analytics 4
- [ ] Mogę wyeksportować raport jako PDF/CSV
- [ ] Porównanie: ten miesiąc vs poprzedni miesiąc
- [ ] Mogę filtrować artykuły po dacie, statusie, platformie, narzędziu
- [ ] Wideę zalecenia: "Artykuł generuje 150 views/dzień, spróbuj repurpose na YouTube"
- [ ] ROI estimate: (PageViews × 0.05 PLN avg) = Estymowana wartość (dla planów płatnych to upsell)
```

### 1.2 BUSINESS CASE

**Uzasadnienie funkcji:**

Bieżący problem: Użytkownicy Floowe nie widzą, czy ich artykuły faktycznie generują traffic czy konwersje. Publikują artykuły i nie mają widoczności na ROI. To prowadzi do **churn'u** (odejścia użytkowników) bo nie rozumieją wartości produktu.

Rozwiązanie: Dashboard Analytics tym pokazuje **konkretne rezultaty** – views, clicks, conversions. To:
1. **Zwiększa retention** – użytkownik widzi wartość (generuje $X/dzień)
2. **Upsell opportunity** – "Upgrade do Premium aby widzieć conversion tracking"
3. **Competitive advantage** – Jasper AI nie ma wbudowanej analityki, a Floowe będzie mieć
4. **Network effect** – Zadowoleni użytkownicy polecają (word-of-mouth)

**Szacunkowy wpływ**: +40% retention, +3% monthly growth

### 1.3 PRZEGLĄD TECHNICZNY

#### Komponenty do Dodania:
```
Frontend:
├── Dashboard/Analytics
│   ├── MetricCards (views, engagement, ranking)
│   ├── LineChart (traffic over time)
│   ├── ChannelBreakdown (pie chart: FB vs LinkedIn vs X vs WWW)
│   ├── TableView (wszystkie artykuły z metrykami)
│   ├── RecommendationWidget (suggestions for optimization)
│   └── ExportButton (PDF/CSV)
├── ArticleDetailPage/Analytics
│   ├── FullMetricsPanel (per article detailed stats)
│   ├── ChannelPerformance (dropdowns for each platform)
│   ├── GoogleRankingCard (position for target keywords)
│   ├── SocialEngagementBubble (likes, shares per channel)
│   └── ComparisonChart (this article vs average)
└── Settings/Analytics
    ├── GoogleAnalytics4Setup
    ├── GoogleSearchConsoleSetup
    ├── TokenManagement
    └── SyncFrequencySettings
```

#### Backend / API Endpoints:
```
GET /api/v1/articles/${articleId}/analytics
├─ Query Params: dateRange, granularity (daily, weekly, monthly)
├─ Response:
│  {
│    pageViews: 1250,
│    uniqueVisitors: 892,
│    averageTimeOnPage: 120,
│    bounceRate: 35.2,
│    ctr: 4.8,
│    conversionCount: 12,
│    channelBreakdown: {
│      website: { views: 800, ctr: 5.2 },
│      facebook: { reach: 3500, engagement: 2.1% },
│      linkedin: { impressions: 1200, ctr: 3.8 },
│      x: { impressions: 450, engagement: 1.2% }
│    },
│    googleMetrics: {
│      keyword: "AI copywriting tools",
│      position: 12,
│      impressions: 340,
│      clicks: 18,
│      ctr: 5.3%
│    },
│    roi_estimate: 62.5 // (pageViews × avg_value_per_view)
│  }

GET /api/v1/dashboard/analytics
├─ Returns summary for all articles (paginated)

POST /api/v1/articles/${articleId}/analytics/export
├─ Params: format (pdf|csv), dateRange
├─ Returns: download link

POST /api/v1/analytics/sync
├─ Trigger manual sync with Google Analytics 4
├─ Requires admin permission
```

#### Integracje:
```
GOOGLE ANALYTICS 4:
├─ OAuth setup (Admin -> Settings -> Integrations)
├─ Requires: Measurement Protocol API access
├─ Data synced: pageViews, uniqueVisitors, bounce rate, avg session duration
└─ Frequency: Every 6 hours (scheduled job)

GOOGLE SEARCH CONSOLE:
├─ OAuth setup
├─ Queries tracked: Top keywords, position, clicks, impressions
├─ Used for: "Your article ranks #12 for 'AI copywriting'"
└─ Frequency: Daily (delayed 24h due to GSC update lag)

SOCIAL MEDIA APIs:
├─ Facebook Graph API: page_insights (reach, engagement)
├─ LinkedIn Official API: post analytics
├─ X (Twitter) API: Tweet engagement metrics
└─ Frequency: Real-time webhooks where available, API polls otherwise
```

#### Tech Stack:
```
Frontend:
├─ React + TypeScript (existing)
├─ Recharts/Chart.js (charting library)
├─ Moment.js / Day.js (date handling)
└─ React-table (for sortable/filterable table)

Backend:
├─ Node.js + Express (existing)
├─ @google-analytics/data (GA4 lib)
├─ @google/search-console (GSC lib)
├─ Bull (job queue for scheduled syncs)
├─ Postgres (store calculated metrics)
└─ Redis (cache for dashboard)

External Services:
├─ Google Analytics 4 API
├─ Google Search Console API
├─ Facebook Graph API v18+
├─ LinkedIn Official API
└─ X (Twitter) API v2
```

#### Database Schema (New):
```sql
-- Articles Analytics Cache (calculated daily)
CREATE TABLE article_analytics (
  id UUID PRIMARY KEY,
  article_id UUID NOT NULL UNIQUE REFERENCES articles(id),
  date_from TIMESTAMP,
  date_to TIMESTAMP,
  
  -- Google Analytics data
  ga_pageviews INTEGER,
  ga_unique_visitors INTEGER,
  ga_bounce_rate DECIMAL(5,2),
  ga_avg_session_duration INTEGER,
  
  -- Social Media
  facebook_reach INTEGER,
  facebook_engagement INTEGER,
  linkedin_impressions INTEGER,
  linkedin_engagement INTEGER,
  x_impressions INTEGER,
  x_engagement INTEGER,
  
  -- Google Search Console
  gsc_position DECIMAL(3,1),
  gsc_impressions INTEGER,
  gsc_clicks INTEGER,
  
  -- Calculated
  total_ctr DECIMAL(5,2),
  roi_estimate DECIMAL(8,2),
  
  last_synced_at TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Article Recommendations (AI suggestions)
CREATE TABLE article_recommendations (
  id UUID PRIMARY KEY,
  article_id UUID NOT NULL REFERENCES articles(id),
  recommendation_type ENUM('REPURPOSE', 'CONTENT_GAP', 'OPTIMIZE_SEO'),
  title VARCHAR(255),
  description TEXT,
  priority ENUM('HIGH', 'MEDIUM', 'LOW'),
  created_at TIMESTAMP
);
```

#### Kompleksność:
- **Effort estimate**: 120-160 hours
- **Ryzyka**: GA4 API delays, social media API rate limits, data accuracy

---

### 1.4 RYZYKA I WYZWANIA

#### Ryzyko #1: Google Analytics 4 API Data Delays
**Problem**: GA4 data pojawia się z 24-48 godzin opóźnieniem  
**Wpływ**: Dashboard pokazuje "wczorajsze" dane, nie real-time  
**Mitigation**:
- Komunikuj w UI: "Data as of 24 hours ago"
- Real-time fallback: Zbieraj page view events bezpośrednio (pixel tracking)
- Opcja manual refresh button

#### Ryzyko #2: Social Media API Rate Limits
**Problem**: X API (Twitter) ma strict rate limits (50 req/15min)  
**Wpływ**: Nie możemy fetchować danych dla 1000 artykułów jednocześnie  
**Mitigation**:
- Batch processing (queue 100 artykułów na dzień)
- Cache results for 24 hours
- Prioritize popular articles

#### Ryzyko #3: Authorization & Data Privacy
**Problem**: Przechowujemy Google Analytics tokens -> security risk  
**Wpływ**: GDPR violation ako token wycieknie  
**Mitigation**:
- Encrypt tokens at rest (AES-256)
- Rotate tokens co 90 dni
- Audit access logs
- Compliance review by DPO

#### Ryzyko #4: False Positive ROI Estimates
**Problem**: Algorytm szacuje ROI (views × $X), ale nie wie actual conversion  
**Wpływ**: Użytkownik czasem misled ("artykuł zarabia $100" ale konwertuje 0%)  
**Mitigation**:
- Disclaimer: "Estimate based on industry averages"
- Allow custom conversion value setup
- Show confidence level (Low/Medium/High)

#### Ryzyko #5: Data Consistency Across Services
**Problem**: GA4 pokazuje 1000 views, ale search console 800  
**Wpływ**: Użytkownik niespokojny, gdzie jest prawda  
**Mitigation**:
- Include footnote explaining differences
- Prioritize GA4 as source of truth
- Regular audits vs Google's public data

#### Wyzwanie: Scalability
**Problem**: 10,000 users × 1,000 articles = 10M API calls/day do GA4  
**Rozwiązanie**:
- Aggregate data hierarchically (daily -> monthly)
- Cache aggressively (Redis)
- Consider data warehouse (BigQuery) for bulk storage

---

## FEATURE #2: Content Calendar & Publishing Scheduler

---

### 2.1 USER STORY

```gherkin
Jako: Content Editorial Manager
Chcę: Zaplanować publikacje artykułów na cały miesiąc w Content Calendar
Aby: Mieć spójną strategię publikacji i publikować w optymalnych czasach

Kryteria Akceptacji:
- [ ] Widzę Calendar view (Month, Week, Day)
- [ ] Mogę drag-drop artykuł do dnia w kalendarzu
- [ ] Mogę ustawić preferred publish time (np. wtorki o 9:00 AM CET)
- [ ] System sugeruje "optimal publish time" bazując na audience habits
- [ ] Mogę schedule serię artykułów (np. 3 artykuły na tydzień przez 8 tygodni)
- [ ] System automatycznie publikuje artykuł w scheduled time
- [ ] Mogę zmienić schedule nawet po zaplanowaniu (do 5 min przed publikacją)
- [ ] Synchronizacja z Google Calendar opcjonalna
- [ ] Powiadomienie 1h przed i 1h po publikacji
- [ ] Buklk operations: schedule 5 artykułów do 10 różnych dni naraz
- [ ] View scheduled publications w tabeli (sortable, filterable)
```

### 2.2 BUSINESS CASE

**Uzasadnienie funkcji:**

Nowy problem: Content consistency jest kluczowy dla SEO. Publikowanie artykułów regularnie (np. 3x/tydzień) zwiększa ranking w Google. Ale użytkownicy Floowe publikują ad-hoc - czasem 5 artykułów dziennie, potem przerwa tydzień.

Rozwiązanie: Content Calendar pozwala:
1. **Zaplanować na miesiące** – regularne publikacje = lepszy SEO
2. **Optimal timing** – AI sugeruje kiedy publikować (When audience is online)
3. **Bulk scheduling** – zaplanować 20 artykułów w 5 minut
4. **Automation** – publikuj sedesza śpię (🌙 automation angle)

**Szacunkowy wpływ**: +15% SEO improvement, +25% time saved on scheduling

### 2.3 PRZEGLĄD TECHNICZNY

#### Komponenty:
```
Frontend:
├── /content-calendar
│   ├── CalendarView (Month/Week/Day modes)
│   │   └─ DragDropZone (artikuł -> data)
│   ├── ArticleList (right sidebar)
│   │   └─ FilterableSearch
│   ├── DAY_DETAIL_MODAL
│   │   ├─ SelectArticles (multi-select)
│   │   ├─ SetPublishTime (time picker)
│   │   ├─ SelectChannels (which platforms)
│   │   └─ ConfirmSchedule button
│   ├── BulkActions toolbar
│   │   ├─ ScheduleSeries button (3 artykuły/dzień na 4 tygodnie)
│   │   └─ ClearSchedule button
│   ├── TimelineView (Gantt-like, shows publications over time)
│   └── ExportCalendar button (Google Calendar, iCal)

├── /schedule/article/${id}
│   ├── ScheduleForm
│   │   ├─ DatePicker
│   │   ├─ TimePicker (with AI suggestion: "Best time: Tue 9:00 AM")
│   │   ├─ ChannelSelector
│   │   ├─ RecurrenceRules (daily, weekly, custom)
│   │   ├─ SeriesConfig (series of N articles)
│   │   └─ SaveSchedule button
│   └─ ScheduledPublications view (confirmations)

└── Settings/Content Strategy
    ├─ Preferred publishing days (checkboxes Mon-Sun)
    ├─ Preferred publishing hours (time range)
    ├─ Target audience timezone (for optimal time calc)
    └─ Series templates (3x/week pattern, etc.)
```

#### API Endpoints:
```
POST /api/v1/articles/${articleId}/schedule
├─ Body: {
│    scheduledPublishDate: "2025-05-15T09:00:00Z",
│    channels: ["website", "facebook", "linkedin"],
│    recurrance: null // or { pattern: "FREQ=WEEKLY;BYDAY=TU", count: 12 }
│  }
├─ Returns: { scheduleId, status: "CONFIRMED", publishAt: "..." }

GET /api/v1/articles/${articleId}/schedule
├─ Returns: scheduled publication details

PATCH /api/v1/articles/${articleId}/schedule
├─ Allows rescheduling (if not within 5 min of publish time)

DELETE /api/v1/articles/${articleId}/schedule
├─ Cancels scheduled publication

GET /api/v1/calendar/publications
├─ Query: dateRange (start, end), granularity
├─ Returns: all publications in calendar view
├─ Response: {
│    "2025-05-15": [
│      { articleId, title, publishTime, channels, status },
│      ...
│    ]
│  }

POST /api/v1/schedule/series
├─ Bulk schedule multiple articles
├─ Body: {
│    articles: [id1, id2, id3],
│    pattern: "FREQ=WEEKLY;BYDAY=MO,WE,FR",
│    startDate: "2025-05-01",
│    count: 12
│  }
├─ Returns: { seriesId, scheduledCount: 36 }

GET /api/v1/schedule/optimal-time
├─ Based on audience engagement patterns
├─ Query: articleCategory (optional)
├─ Returns: { suggestedTime: "2025-05-15T09:00:00Z", confidence: 0.87 }
```

#### Backend Services:
```
SchedulerService:
├─ schedulePublication(articleId, publishDate, channels)
│  └─ Saves to ScheduledPublications table, adds to queue
├─ OptimalTimeCalculator(audienceData)
│  ├─ Analyzes historical article performance
│  ├─ Checks audience timezone distribution
│  ├─ Looks at competitors' publish schedule
│  └─ Returns top 3 time slots with confidence
└─ AutoPublishWorker (Bull queue)
   ├─ Trigger 1 sec before scheduled time
   ├─ Call PublishArticle endpoint
   ├─ Handle retries if failed
   └─ Send notifications

NotificationService:
├─ Send email 1h before: "Your article 'XYZ' will publish in 1 hour"
├─ Send email 1h after: "Success! 'XYZ' published to 3 channels. Views: 12"
└─ In-app notifications (bell icon)
```

#### Tech Stack:
```
Frontend:
├─ React + TypeScript
├─ react-big-calendar (calendar lib)
├─ react-dnd (drag-drop)
├─ date-fns (date handling)
└─ formik + yup (form + validation)

Backend:
├─ Node.js + Express
├─ Bull (job queue for publishing)
├─ node-schedule (cron jobs)
├─ PostgreSQL
└─ Redis (queue & cache)

External:
├─ Google Calendar API (optional export integration)
└─ Twilio/SendGrid (push notifications)
```

#### Database Schema:
```sql
CREATE TABLE scheduled_publications (
  id UUID PRIMARY KEY,
  article_id UUID NOT NULL REFERENCES articles(id),
  scheduled_publish_at TIMESTAMP NOT NULL,
  channels TEXT[] DEFAULT '{}', -- e.g. {"website", "facebook", "linkedin"}
  status ENUM('SCHEDULED', 'CONFIRMED', 'PUBLISHED', 'FAILED', 'CANCELLED'),
  created_by UUID NOT NULL REFERENCES users(id),
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  
  UNIQUE(article_id, scheduled_publish_at)
);

CREATE TABLE publication_series (
  id UUID PRIMARY KEY,
  created_by UUID NOT NULL,
  pattern VARCHAR(255), -- iCal RRULE format: FREQ=WEEKLY;BYDAY=MO,WE
  start_date DATE,
  occurrences INTEGER,
  articles UUID[] DEFAULT '{}',
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_scheduled_pub_at ON scheduled_publications(scheduled_publish_at);
CREATE INDEX idx_scheduled_user ON scheduled_publications(created_by);
```

#### Kompleksność:
- **Effort estimate**: 160-200 hours
- **Ryzyka**: Timezone issues, queue persistence, race conditions on publish

---

### 2.4 RYZYKA I WYZWANIA

#### Ryzyko #1: Timezone Misalignment
**Problem**: User jest w PL, ale target audience w USA. "Optimal time" calculator nie zna tego.  
**Wpływ**: Publikujesz o 9 AM CET gdy audience spać.  
**Mitigation**:
- Allow configurable audience timezone
- Detect from GA4 audience location data
- Show warning: "Your audience is in EST timezone"

#### Ryzyko #2: Queue Persistence (Race Conditions)
**Problem**: Server crashed o 9:05 AM, artykuł zaplanowany na 9:00 AM nie opublikowany.  
**Wpływ**: Artykuł nigdy się nie publikuje.  
**Mitigation**:
- Persist queue to Redis (restarty to synchronizują)
- Job retry logic (retry 3x with exponential backoff)
- Admin dashboard: "Missed publications" alert

#### Ryzyko #3: Bulk Scheduling Confusion
**Problem**: User schedules 50 artykułów na jednym kliknie - oops 30 duplicates.  
**Wpływ**: Spam na social media.  
**Mitigation**:
- Confirmation dialog before bulk operations
- Dry-run preview: "You're about to schedule 50 items"
- Undo button (24 hours window)

#### Ryzyko #4: Social Media API Publishing Limits
**Problem**: X (Twitter) API has rate limits (50 posts/15min). Burst scheduling hits limit.  
**Wpływ**: Niektóre posty się nie publikują.  
**Mitigation**:
- Queue processing with delays
- Stagger publications across channels (1 min apart)
- Smart backoff when rate limit hit

#### Ryzyko #5: Optimal Time Accuracy
**Problem**: AI sugeruje "9 AM" aletv to może być fałsz (mała sample size).  
**Wpływ**: Użytkownik traci trust w rekomendacje.  
**Mitigation**:
- Include confidence score: "Suggested time: 9 AM (confidence: 62%)"
- "Based on X article performances"
- Allow override: user manually picks time

#### Wyzwanie: Multi-Channel Adaptations
**Problem**: Artykuł na WWW jest 2000 słów, ale X limit 280 char.  
**Rozwiązanie**:
- Adaptive content generation (AI tworzy variants)
- Manual override per channel
- Template system for formatting

---

## FEATURE #3: Team Collaboration & Review Workflow

---

### 3.1 USER STORY

```gherkin
Jako: Editorial Manager w zespole contentowym
Chcę: Zapraszać kolegów do przeglądu artykułów przed publikacją
Aby: Zapewnić jakość contentu i mieć unified approval process

Kryteria Akceptacji:
- [ ] Mogę zaprosić zespół członka (email invite)
- [ ] Mogę wyznaczyć role: Viewer, Editor, Reviewer, Approver
- [ ] Draft artykuł mogę wysłać do review (status -> Under Review)
- [ ] Reviewer widzi artykuł, może dodać komentarze (inline)
- [ ] Reviewer może Request Revisions, Approve, nebo Reject
- [ ] Autor dostaje notification: "Jane requested revisions: 'typo in title'"
- [ ] Mogę widzieć Activity log (kto, kiedy, jaką akcję)
- [ ] Approved articles mają green badge
- [ ] Mogę publikować tylko approved artykuły (nie draft/rejected)
- [ ] Notifications są email + in-app + Slack (optional)
- [ ] Permission controls: Only Approver can publish (prevent co-worker misclick)
```

### 3.2 BUSINESS CASE

**Uzasadnienie funkcji:**

Problem: Edytujące zespoły (2+ people) nie mogą efektywnie współpracować w Floowe. Draft artykuł jest tylko widoczny dla autora. Brak formalnego approval procesu. Ryzyko: ktoś publikuje coś źle, bez review.

Rozwiązanie: Built-in collaboration:
1. **Formalne approval process** – zmniejsza błędy (typos, fact-checking)
2. **Team seats opportunity** – "Add 3 team members for $15/user/month" (upsell!)
3. **Enterprise feature** – Premium → Team plan transition
4. **Compliance ready** – Approval logs (dla ISO, GDPR audits)

**Szacunkowy wpływ**: +$50K/year from team plan (upsell), -20% content errors, +15% enterprise deals

### 3.3 PRZEGLĄD TECHNICZNY

#### Komponenty:
```
Frontend:
├── /articles/${id}/team
│   ├── TeamMembersPanel
│   │   ├─ InviteTeamMember (email + role selector)
│   │   ├─ TeamMemberList (active members, roles, activity)
│   │   └─ RemoveTeamMember button
│   ├── ReviewPanel
│   │   ├─ Status badge (Draft / Under Review / Approved / Rejected / Published)
│   │   ├─ ReviewerFeedback (list of reviewer comments)
│   │   ├─ SendForReview button (Draft -> Under Review)
│   │   └─ PublishButton (only for Approver role, only if Approved)
│   └─ ActivityLog (timeline) {
│       │   timestamp: 2025-05-15 09:30 AM
│       │   action: "Jane approved this article"
│       │   approver: "Jane D."
│       │   comments: "Looks good! Minor grammar fix in paragraph 3"
│       │ }

├── /articles/${id}/review (Reviewer's view)
│   ├─ FullArticleDisplay
│   │   └─ InlineComments (click paragraph to add comment)
│   ├─ ReviewActions
│   │   ├─ ApproveButton (green, "It's correct")
│   │   ├─ RequestRevisionsButton (orange, "Changes needed")
│   │   ├─ RejectButton (red, "Don't publish")
│   │   └─ TextArea for feedback
│   └─ ArticleChangesDiff (if edited since sent to review)

├── Dashboard/TeamReviews
│   ├─ "Articles Awaiting Your Review" (2 items)
│   │   └─ CardView with quick preview
│   ├─ "Your Articles Under Review" (1 item, status, reviewers)
│   └─ ReviewActivity feed

└── Settings/Team Management
    ├─ Invite new member (email + role)
    ├─ Change role (Editor -> Reviewer)
    ├─ Remove member
    └─ Team usage (3/5 seats filled)
```

#### API Endpoints:
```
POST /api/v1/articles/${articleId}/team/invite
├─ Body: { email, role: "VIEWER|EDITOR|REVIEWER|APPROVER" }
├─ Returns: invitation token, sends email
├─ Only workspace creator can invite

GET /api/v1/articles/${articleId}/team
├─ Returns: [{ userId, email, role, joinedAt, lastReviewedAt }]

POST /api/v1/articles/${articleId}/team/${userId}/change-role
├─ Body: { newRole: "APPROVER" }

DELETE /api/v1/articles/${articleId}/team/${userId}
├─ Remove team member from article

POST /api/v1/articles/${articleId}/send-for-review
├─ Changes status: Draft -> UnderReview
├─ Body: { reviewersIds: [...], reviewDeadline: Date }

POST /api/v1/articles/${articleId}/reviews/${reviewId}
├─ Reviewer action
├─ Body: { action: "APPROVE|REQUEST_REVISIONS|REJECT", comments: "..." }
├─ Sends notification to author

GET /api/v1/articles/${articleId}/reviews
├─ Returns all reviews with comments, timestamps

POST /api/v1/articles/${articleId}/comments
├─ Inline comments on article
├─ Body: { paragraphId, text, lineNumber }
├─ Mention support: "Great point @jane!"

GET /api/v1/dashboard/team-activities
├─ Timeline of team actions (for dashboard feed)

GET /api/v1/articles/${articleId}/activity-log
├─ Full audit trail (for compliance)
├─ Returns: [{ timestamp, actor, action, details }]
```

#### Backend Services:
```
CollaborationService:
├─ inviteTeamMember(articleId, email, role)
├─ sendForReview(articleId, reviewerIds)
├─ submitReview(articleId, reviewId, action, comments)
├─ addInlineComment(articleId, paragraphId, text)
└─ publishApprovedArticle(articleId)

RoleBasedAccessControl (RBAC):
├─ Viewer: read-only access
├─ Editor: can edit article, add to review
├─ Reviewer: can comment, approve/reject
├─ Approver: can publish approved articles
└─ Owner: full permissions

PermissionMiddleware:
├─ Check role before each action
├─ Prevent Draft publish without approval
└─ Log all permission checks (audit trail)

NotificationService:
├─ Invite: "You've been added to review 'Article Title'"
├─ Sent to Review: "3 team members are reviewing your article"
├─ Review Received: "Jane approved your article"
├─ Mentioned: "Jane mentioned you in comments"
└─ Deadline: "Review deadline in 1 hour"
```

#### Tech Stack:
```
Frontend:
├─ React + TypeScript
├─ react-diff-viewer (show changes)
├─ draft-js or Slate (rich text with inline comments)
├─ socket.io-client (real-time notifications)
└─ formik + yup

Backend:
├─ Node.js + Express
├─ JWT for role-based auth
├─ Socket.io (real-time notifications)
├─ Bull (notification queue)
├─ PostgreSQL (audit logs)
└─ Redis (active sessions)

External:
├─ SendGrid (email invites)
├─ Slack API (optional notifications)
└─ Webhook provider (for custom integrations)
```

#### Database Schema:
```sql
-- Team members per workspace
CREATE TABLE team_members (
  id UUID PRIMARY KEY,
  workspace_id UUID NOT NULL REFERENCES workspaces(id),
  user_id UUID REFERENCES users(id),
  email VARCHAR(255),
  role ENUM('VIEWER', 'EDITOR', 'REVIEWER', 'APPROVER'),
  invited_by UUID NOT NULL REFERENCES users(id),
  joined_at TIMESTAMP,
  invited_at TIMESTAMP DEFAULT NOW(),
  status ENUM('INVITED', 'ACTIVE', 'INACTIVE', 'REMOVED')
);

-- Article reviews
CREATE TABLE article_reviews (
  id UUID PRIMARY KEY,
  article_id UUID NOT NULL REFERENCES articles(id),
  reviewer_id UUID NOT NULL REFERENCES users(id),
  action ENUM('APPROVED', 'REQUEST_REVISIONS', 'REJECTED', 'PENDING'),
  comments TEXT,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  
  UNIQUE(article_id, reviewer_id)
);

-- Inline comments
CREATE TABLE review_comments (
  id UUID PRIMARY KEY,
  article_id UUID NOT NULL REFERENCES articles(id),
  review_id UUID REFERENCES article_reviews(id),
  commenter_id UUID NOT NULL REFERENCES users(id),
  paragraph_id VARCHAR(100), -- Reference to paragraph in editor
  text TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Audit log (compliance)
CREATE TABLE audit_log (
  id UUID PRIMARY KEY,
  workspace_id UUID NOT NULL,
  actor_id UUID NOT NULL,
  action VARCHAR(100),
  resource_type VARCHAR(50),
  resource_id UUID,
  details JSONB,
  created_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_article_reviews ON article_reviews(article_id);
CREATE INDEX idx_audit_timestamp ON audit_log(created_at);
CREATE INDEX idx_audit_actor ON audit_log(actor_id);
```

#### Kompleksność:
- **Effort estimate**: 200-240 hours
- **Ryzyka**: Race conditions on approval, notification delivery, compliance

---

### 3.4 RYZYKA I WYZWANIA

#### Ryzyko #1: Approval Bottleneck
**Problem**: Approver jest na urlopie przez 2 tygodnie, wszystkie artykuły stuck na "Awaiting Approval".  
**Wpływ**: Publikowanie zatrzymane.  
**Mitigation**:
- Fallback approver (secondary person)
- "Delegate approval" option
- Escalation: Owner can manually approve if Approver absent

#### Ryzyko #2: Race Condition on Publish
**Problem**: Article status is Under Review, owner still clicks Publish (multi-tab).  
**Wpływ**: Opublikuj Draft zamiast Approved.  
**Mitigation**:
- Client-side disable Publish button if not Approved
- Server-side validation: reject publish if not all reviewers approved
- Optimistic locking (version field)

#### Ryzyko #3: Comment Notification Spam
**Problem**: Każdy comment = notification. 20 team members = 20 notifs.  
**Wpływ**: Notification fatigue.  
**Mitigation**:
- Thread-based notifications (group comments)
- Digest emails: "3 comments on your article" (not 3 separate)
- User preference: email yes/no, frequency (real-time, hourly, daily)

#### Ryzyko #4: Data Privacy (Sensitive Comments)
**Problem**: Reviewer pisze "Fire this copy, it's terrible" in comment  
**Wpływ**: Drama, morale issue, company culture problem.  
**Mitigation**:
- Educate team on professional tone
- Consider private mode comments (only for author + approver)
- No moderation tool (yet) - future roadmap

#### Ryzyko #5: Onboarding Complexity
**Problem**: New reviewer os confused by interface, doesn't realize they need to click "Approve".  
**Wpływ**: Articles stuck in review indefinitely.  
**Mitigation**:
- Guided tutorial (first time)
- Clear status badges (Red = Action Needed)
- Deadline countdown (visual urgency)

#### Wyzwanie: Multi-Language Comment Support
**Problem**: Team je międzynarodowy, reviewers piszą komentarze po polsku/angielsku/niemiecku.  
**Rozwiązanie**:
- Auto-translate via Google Translate API
- Show original + translated version
- Mark original language

---

## 4. PRIORYTET IMPLEMENTACJI

### Phase 1 (Months 1-2): Feature #2 (Content Calendar)
- Easiest to implement
- Lowest risk
- Highest immediate user value ("Schedule articles for a month!")
- Quick wins = momentum

### Phase 2 (Months 3-4): Feature #1 (Analytics)
- Medium complexity
- Integration heavy (GA4, Search Console)
- High retention impact
- ROI visualization = upsell unlock

### Phase 3 (Months 5-6): Feature #3 (Team Collaboration)
- Most complex (RBAC, permissions)
- Highest revenue impact (team seats = $$$)
- Enterprise enabler
- Can bundle all 3 features into "Pro" tier

---

## 5. SUMMARY TABLE

| Feature | Effort | Risk | Retention Impact | Revenue Impact | Priority |
|---------|--------|------|------------------|-----------------|----------|
| **Analytics** | 120-160h | HIGH | Very High | Medium (#2 upsell) | 2 |
| **Content Calendar** | 160-200h | MEDIUM | Medium | Low | 1 |
| **Team Collaboration** | 200-240h | HIGH | High | High (#3 new tier) | 3 |

