# Floowe - Analiza Produktu i Roadmap Funkcjonalności

## � Repozytorium GitHub

**Link do publicznego repo**: [https://github.com/NikopolNiko/floowe-project](https://github.com/NikopolNiko/floowe-project)

> Analiza wykonana przy użyciu **Claude Code** (claude.ai/code) zgodnie z wymaganiami zadania.

---

## �📋 Spis Treści

To repozytorium zawiera kompletną analizę produktu **Floowe** - aplikacji do automatycznego tworzenia i publikowania treści na stronach internetowych i mediach społecznościowych.

### Dokumenty w Analizie:

1. **[01-Analiza-Aplikacji-Floowe.md](01-Analiza-Aplikacji-Floowe.md)** ✅
   - Przegląd aplikacji (funkcjonalności, grupa docelowa, model biznesowy)
   - Analiza UX/UI i bieżących pain points
   - Identyfikacja punktów integracji z systemami zewnętrznymi
   - Konkurencja i różnicowanie się Floowe
   - Wnioski z analizy

2. **[02-Przepływy-Użytkownika.md](02-Przepływy-Użytkownika.md)** ✅
   - Procesy rejestracji i logowania
   - 5 głównych przypadków użycia (Use Cases):
     - Tworzenie artykułu z sugestii AI
     - Tworzenie artykułu z własnego pomysłu
     - Edycja i publikacja
     - Zarządzanie kanałami publikacji
     - Repurposing starych artykułów
   - Przepływ płatności i Upgrade flow
   - Integracje zewnętrzne (Facebook, Google Search Console)
   - Core business metrics

3. **[03-Event-Storming-AS-IS-TO-BE.md](03-Event-Storming-AS-IS-TO-BE.md)** ✅
   - **Event Storming AS-IS** (Stan Bieżący):
     - Główny przepływ publikacji
     - Events timeline (16 zdarzeń)
     - Pain points i brakujące funkcjonalności
   - **Event Storming TO-BE** (Stan Przyszły):
     - 3 nowe funkcjonalności z 24 nowymi eventami
     - Tier 1: Publication z Analytics
     - Tier 2: Analytics (NEW)
     - Tier 3: Team Collaboration (NEW)
   - Mapa systemów i integracji
   - Krytyczne obserwacje (mocne strony, słabe strony, potencjał wzrostu)

4. **[04-Specyfikacja-Funkcjonalności.md](04-Specyfikacja-Funkcjonalności.md)** ✅
   - **Feature #1: Real-Time Analytics Dashboard**
     - User Story z kryteriami akceptacji
     - Business Case (retention +40%, competitive advantage)
     - Techniczny przegląd (komponenty, API, integracje)
     - 5 ryzyk i mitigation
   
   - **Feature #2: Content Calendar & Publishing Scheduler**
     - User Story (planowanie publikacji na miesiąc)
     - Business Case (SEO improvement +15%, time saved +25%)
     - Techniczny przegląd (calendar view, scheduling, notifications)
     - 5 ryzyk i mitigation
   
   - **Feature #3: Team Collaboration & Review Workflow**
     - User Story (zapraszanie zespołu, approvals, comments)
     - Business Case (+$50K/year z team plan, enterprise enabler)
     - Techniczny przegląd (RBAC, review process, notifications)
     - 5 ryzyk i mitigation
   
   - Priorytet implementacji (Phase 1-3)
   - Summary table (effort, risk, retention, revenue impact)

5. **[05-Ryzyka-Wyzwania-Globalne.md](05-Ryzyka-Wyzwania-Globalne.md)** ✅
   - **4 Kategorie Ryzyka**:
     - **B1-B4**: Ryzyka Biznesowe (Competition, Monetization, Infra, Compliance)
     - **T1-T4**: Ryzyka Techniczne (API Limits, Race Conditions, External Dependencies, Performance)
     - **E1-E3**: Ryzyka Organizacyjne (Resources, Alignment, QA)
     - **M1-M2**: Ryzyka Rynkowe (Adoption, Pricing)
   - **5 Krytycznych Wyzwań**: Złożoność produktu, akuracja danych, automatyzacja vs kontrola, koordynacja zespołu, roadmap leanness
   - Risk Heat Map
   - Response plan i monitoring cadence
   - Podsumowanie (sukces zależy od dedicated team, ścisłej kolaboracji, rigorous QA)

---

## 🎯 Kluczowe Spostrzeżenia

### O Aplicji Floowe

**Co robi?**  
Floowe automatyzuje tworzenie i publikowanie treści marketingowych AI-powered. Użytkownik podaje temat, AI generuje artykuł, Floowe publikuje go jednym kliknięciem na 4 kanały (WWW, Facebook, LinkedIn, X).

**Dla Kogo?**  
Małe i średnie przedsiębiorstwa (SME), przedsiębiorcy, agencje marketingowe szukające szybkiego content marketingu.

**Model Biznesowy**  
Subscription SaaS z 4 planami (Free 3 art/m, Basic 8/m, Standard 12/m, Premium 20/m). Cena: 0-900 PLN/miesiąc.

**Główne Atrybuty**  
✅ Multikanałowa publikacja (WWW + 3 social media)  
✅ AI generowanie treści  
✅ Edytor WYSIWYG  
✅ Integracja grafik (stock + AI)  
✅ Analiza trendów SEO  

**Pain Points AS-IS**  
❌ Brak widoczności ROI (Czy artykuł zarabia?)  
❌ Brak wsparcia dla zespołów  
❌ Publikowanie tylko natychmiast (brak planowania)  
❌ Brak analityki (performance tracking)  
❌ Brak koordynacji (one person per article)  

---

## 💡 3 Proponowane Funkcjonalności

### 1. Real-Time Analytics Dashboard 📊
**Problem**: Użytkownik nie widzi czy artykuły generują traffic/konwersje  
**Rozwiązanie**: Dashboard z metrykami per artykuł (views, engagement, Google ranking, ROI estimate)  
**Wpływ**: +40% retention, competitive advantage vs Jasper AI  
**Effort**: 120-160 godzin

### 2. Content Calendar & Publishing Scheduler 📅
**Problem**: Publikowanie ad-hoc zamiast regularnie (złe dla SEO)  
**Rozwiązanie**: Calendar do zaplanowania publikacji na miesiące z AI suggested optimal times  
**Wpływ**: +15% SEO improve, +25% time saved, +25% user growth  
**Effort**: 160-200 godzin

### 3. Team Collaboration & Review Workflow 👥
**Problem**: SME teamsy nie mogą efektywnie współpracować (brak approvals)  
**Rozwiązanie**: Invite members, review workflow, inline comments, formal approvals  
**Wpływ**: +$50K/year z team plan, enterprise enabler  
**Effort**: 200-240 godzin

---

## 📊 Event Storming Analiza

### AS-IS (Bieżący Stan)
```
User → Create Article → AI generates → Edit → Select Channels → Publish
                                                ↓
                                    (Facebook, LinkedIn, X, WWW)
```

**16 Events**: UserLoggedIn → ArticleContentGenerated → EditorContentEdited → ... → ArticlePublished

**Pain Points**: No analytics, no team collab, no scheduling, no repurposing

### TO-BE (Stan Przyszły)
```
User + Team → Create → AI→ Review (Approval Workflow) → Schedule (Optimal Time) → Auto-Publish
                                                              ↓
                                                    Content Calendar View
                                                              ↓
                                                    Real-Time Analytics
                                                              ↓
                                                    Recommendations (Repurpose)
```

**40 Events**: Team collaboration events + Scheduling events + Analytics events

---

## ⚠️ Główne Ryzyka

### HIGH PRIORITY (Monitor Closely)
1. **B1 - Market Competition**: Jasper AI might launch analytics first → accelerate launch
2. **T1 - API Rate Limits**: Social media APIs throttle → implement queueing system
3. **M1 - Feature Adoption**: Users don't use new features → invest in onboarding

### MEDIUM PRIORITY
- B2: Team plan monetization (SMEs might not pay)
- B3: Infrastructure costs scale (GA4 API = expensive)
- B4: GDPR/Security (token management = risk)
- T2: Race conditions (data consistency)
- T3: External API dependencies (fallback needed)
- T4: Performance degradation (caching required)
- E1: Resource constraints (hiring needed)
- M2: Pricing disconnect (value prop unclear)

### LOW PRIORITY (But Important)
- E2: PM/Design/Eng alignment
- E3: Testing & QA

---

## 🛠️ Techniczny Stack (Assumed)

### Frontend
- React + TypeScript
- WYSIWYG Editor (Draft.js / Slate)
- Charts (Recharts)
- Calendar library (react-big-calendar)
- Drag-drop (react-dnd)

### Backend
- Node.js + Express
- PostgreSQL (data)
- Redis (cache + queue)
- Bull (job queue for scheduling)
- JWT (auth)
- Socket.io (real-time notifications)

### External APIs
- Google Analytics 4, Search Console
- Facebook Graph API
- LinkedIn Official API
- X (Twitter) API v2
- OpenAI (content generation)

---

## 📈 Szacunkowy Wpływ (Roadmap)

| Feature | Retention | Revenue | Timeline |
|---------|-----------|---------|----------|
| Analytics | +40% | +Medium | Months 3-4 |
| Content Calendar | +25% | +Low | Months 1-2 |
| Team Collab | +20% | +HIGH | Months 5-6 |
| **TOTAL** | **~60-80% retention gain** | **+$50K-100K/year** | **6 months** |

---

## 🚀 Implementation Phases

### Phase 1 (Months 1-2): Content Calendar
- Easiest to implement
- Quick wins, momentum
- Foundation for Phase 2

### Phase 2 (Months 3-4): Analytics Dashboard
- Medium complexity
- High retention impact
- Competitive advantage

### Phase 3 (Months 5-6): Team Collaboration
- Most complex (RBAC, permissions)
- Highest revenue impact
- Enterprise enabler

---

## 📝 Metodologia

Analiza wykonana przy użyciu:
- **Product Analysis Framework**: Przegląd aplikacji, funkcjonalności, model biznesowy
- **User Flow Mapping**: 5 głównych case'ów użycia
- **Event Storming**: AS-IS vs TO-BE diagram (Event, Command, Actor model)
- **Feature Specification**: User Stories, Business Cases, Technical Reviews, Risk Analysis
- **Risk Management**: High-impact/high-probability risks z mitigation strategies

## 🤖 Wykorzystanie Claude Code

Zgodnie z wymaganiem zadania, analiza została przeprowadzona przy użyciu **[Claude Code](https://docs.claude.com/claude-code)**:

| Etap | Użycie Claude Code |
|------|--------------------|
| Krok 1 – Analiza Floowe | Analiza strony floowe.com, identyfikacja funkcji, UX/UI, modelu biznesowego |
| Krok 2 – Przepływy | Mapowanie user flows, use cases, płatności |
| Krok 3 – Event Storming | Projektowanie AS-IS / TO-BE, identyfikacja eventów, komend, aktorów |
| Krok 4 – Specyfikacje | Generowanie User Stories, Business Cases, Tech Reviews |
| Ryzyka | Analiza ryzyk dla każdej funkcji i na poziomie roadmapu |

> Claude Code umożliwił szybkie iterowanie nad strukturą dokumentów, weryfikację spójności Event Storming oraz identyfikację edge cases w specyfikacjach technicznych.

---

## 👤 O Analizie

**Narzędzie**: Claude Code (claude.ai/code) — użyte do analizy, event stormingu i projektowania funkcjonalności  
**Data**: Marzec 2026  
**Cel**: Ocena zdolności do analizy produktów i projektowania funkcjonalności w roli Technical PM/BA  
**Focused On**: Product understanding, user empathy, systemic thinking, decision-making rationale

---

## 🔗 Jak Czytać Dokumenty

1. **Zacznij od**: [01-Analiza-Aplikacji-Floowe.md](01-Analiza-Aplikacji-Floowe.md) (zrozumienie produktu)
2. **Następnie**: [02-Przepływy-Użytkownika.md](02-Przepływy-Użytkownika.md) (user flows)
3. **Event Storming**: [03-Event-Storming-AS-IS-TO-BE.md](03-Event-Storming-AS-IS-TO-BE.md) (system design thinking)
4. **Features**: [04-Specyfikacja-Funkcjonalności.md](04-Specyfikacja-Funkcjonalności.md) (detailed specs)
5. **Risk & Mitigation**: [05-Ryzyka-Wyzwania-Globalne.md](05-Ryzyka-Wyzwania-Globalne.md) (risk management)

---

## ❓ Przygotowanie do Rozmowy Technicznej

### Pytanie 1: Czym różni się Event od Komendy od akcji UI?

| Pojęcie | Definicja | Przykład w Floowe |
|---------|-----------|-------------------|
| **Akcja UI** | Kliknięcie przycisku przez użytkownika — warstwa prezentacji, nie biznesowa | Użytkownik klika przycisk „Opublikuj" w edytorze |
| **Komenda** (`Command`) | Intencja/żądanie zmiany stanu systemu. Może zostać odrzucona (np. limit artykułów wyczerpany) | `PublishArticle(articleId, channels[])` |
| **Event** | Fakt który już się zdarzył — nieodwracalny, zapisany w historii systemu | `ArticlePublished`, `PostCreatedOnFacebook` |

**Kluczowa różnica**: Komenda to prośba ("zrób to"), Event to historia ("to się stało"). Jedno kliknięcie UI → 1 Komenda → wiele Eventów (np. `PublishArticle` → `ArticlePublished` + `PostCreatedOnFacebook` + `ThreadCreatedOnX` + `UserNotified`).

---

### Pytanie 2: Dlaczego Content Calendar jest Phase 1, a nie Analytics?

**Decyzja oparta na 3 kryteriach**:

| Kryterium | Content Calendar (Phase 1) | Analytics (Phase 2) |
|-----------|---------------------------|---------------------|
| **Złożoność techniczna** | Niska — własna baza danych, job queue, UI calendar | Wysoka — 3 zewnętrzne API (GA4, GSC, social media), OAuth, GDPR |
| **Ryzyko** | Niskie — brak zewnętrznych zależności | Wysokie — GA4 delays 24h, API rate limits, token security |
| **Time-to-value** | 2 miesiące, użytkownik widzi wartość od razu | 4 miesiące, wartość widoczna dopiero po zebraniu danych historycznych |

**Uzasadnienie biznesowe**: Content Calendar rozwiązuje problem regularności publikacji (bezpośredni wpływ na SEO użytkownika) bez ryzyka regulacyjnego. Analytics bez danych historycznych nie daje wartości — musi być poprzedzone miesiącami regularnych publikacji, które Content Calendar właśnie umożliwia. Fazy są ze sobą zależne: Calendar → dane → Analytics.

---

### Pytanie 3: Dlaczego te 3 funkcje, a nie inne?

**Ramy decyzyjne — Impact vs Effort vs Risk**:

```
                HIGH IMPACT
                    │
     Team Collab ●  │  ● Analytics
                    │
LOW EFFORT ─────────┼───────── HIGH EFFORT
                    │
  Content Cal ●     │
                    │
                LOW IMPACT
```

Wybrane funkcje pokrywają **3 różne problemy wartości**:
1. **Analytics** → użytkownik nie widzi ROI → churn po 60 dniach (retention problem)
2. **Content Calendar** → publikowanie ad-hoc → słabe SEO → użytkownik nie rozumie dlaczego nie działa (activation problem)
3. **Team Collaboration** → jeden użytkownik → brak możliwości skalowania biznesu klienta → brak upsell (monetization problem)

Odrzucone alternatywy i powód:
- **YouTube/TikTok integration** — nowy kanał bez popytu potwierdzonego (assumption risk)
- **A/B testing artykułów** — zbyt niszowe dla SME bez dużego traffic
- **Template system** — nice-to-have, nie rozwiązuje żadnego core pain point

---

### Pytanie 4: Co to jest Bounded Context i jak go widzisz w modelu Floowe?

Bounded Context = logiczna granica domeny, w której określone pojęcia mają jednoznaczne znaczenie i model danych jest spójny wewnętrznie.

**W Floowe zidentyfikowałem 4 Bounded Contexts** (widoczne w diagramach Mermaid):

| Bounded Context | Co zawiera | Dlaczego oddzielny |
|----------------|------------|--------------------|
| `Content Creation` | Article, Editor, AI generation | Inne reguły biznesowe niż publikacja — artykuł może istnieć bez publikacji |
| `Publication` | PublicationManager, Channels, Policy | Odpowiada za dystrybucję — niezależnie od tego jak treść powstała |
| `Collaboration` | TeamWorkflow, Reviews, Permissions | Własny model ról (EDITOR/REVIEWER/APPROVER) — nieistotny dla tworzenia solo |
| `Analytics` | Metrics, Dashboard, Recommendations | Dane read-only z zewnętrznych źródeł — nie modyfikuje artykułów, tylko je obserwuje |

Granice widać po tym, że **`Article` w BC Content Creation** to `{title, content, status: DRAFT}`, a **`Article` w BC Analytics** to `{articleId, pageViews, ranking}` — ten sam obiekt, różna reprezentacja w różnym kontekście.

---

### Pytanie 5: Jakie są założenia których nie możesz potwierdzić bez dostępu do kodu?

1. **Stack techniczny** — założono React + Node.js + PostgreSQL na podstawie typowego SaaS polskiego origin. Może być inne (Next.js, Laravel, różna baza).
2. **Czy WordPress integration istnieje** — na stronie nie potwierdzone jednoznacznie, oznaczone jako `?`
3. **Obecna architektura monolith vs microservices** — wpływa na koszt dodania nowych serwisów (Analytics, Scheduling)
4. **Dane o churnie i retention** — liczby (+40% retention z Analytics) to szacunki branżowe, nie dane Floowe

---

## 📞 Kontakt / Pytania

Analiza dostępna do dyskusji. Gotów obronić każde design decision i wyjaśnić diagram Event Storming.

---

**Version**: 2.0  
**Last Updated**: Marzec 2026  
**Status**: ✅ Ready for Technical Interview
