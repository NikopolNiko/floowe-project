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
6. **[Weryfikacja Zrozumienia](#-weryfikacja-zrozumienia--odpowiedzi-na-4-kryteria-z-zadania)** — bezpośrednie odpowiedzi na 4 kryteria oceny z zadania:
   - Kryterium 1: Wyjaśnienie decyzji projektowych
   - Kryterium 2: Objaśnienie diagramu Event Storming
   - Kryterium 3: Różnica Event / Komenda / Akcja UI
   - Kryterium 4: Uzasadnienie sensu biznesowego funkcji

---

## ❓ Weryfikacja Zrozumienia — Odpowiedzi na 4 Kryteria z Zadania

> Poniżej wyczerpujące odpowiedzi na każde pytanie które może pojawić się podczas rozmowy technicznej. Każda sekcja zawiera nie tylko "co" ale "dlaczego tak, a nie inaczej" oraz "jak zmierzymy sukces".

---

### Kryterium 1 — Wyjaśnienie decyzji projektowych

#### 1A: Dlaczego te 3 funkcje, a nie inne?

**Matryca Impact vs Effort** (wybór oparty o 4 kryteria: retencja, aktywacja, monetyzacja, ryzyko):

```
                HIGH IMPACT
                    │
     Team Collab ●  │  ● Analytics
                    │
LOW EFFORT ─────────┼───────── HIGH EFFORT
                    │
                    │  ● Content Cal
                    │
                LOW IMPACT
```

> Effort: Content Calendar (160-200h) < Analytics (120-160h, wysoka złożoność API) < Team Collaboration (200-240h, RBAC + workflow)

Każda funkcja rozwiązuje **inny, niezależny problem na różnym etapie cyklu życia użytkownika**:

| Funkcja | Problem | Etap lejka | Hipoteza wartości |
|---------|---------|-----------|-------------------|
| Analytics Dashboard | Użytkownik nie widzi ROI → churn w 60 dni | **Retention** | Widoczność wyników = motywacja do zostania |
| Content Calendar | Nieregularne publikacje → słabe SEO → użytkownik nie rozumie dlaczego nie działa | **Activation** | Rytm publikacji = dowód działania produktu |
| Team Collaboration | Solo-only model → blok dla agencji i SME 5+ osób | **Monetization** | Team seats = nowa warstwa przychodów |

**Odrzucone alternatywy i dlaczego:**

| Kandydatura | Powód odrzucenia |
|-------------|-----------------|
| YouTube/TikTok integration | Brak potwierdzonego popytu (assumption risk, zero danych) |
| A/B testing artykułów | Wartość tylko przy dużym traffic (>10K sesji/m) — większość SME tego nie ma |
| Template system | Nice-to-have, nie eliminuje żadnego core pain point |
| AI Image Generation | Commodity (Canva, Midjourney) — nie jest przewagą różnicującą |

---

#### 1B: Dlaczego Content Calendar jest Phase 1, a nie Analytics?

| Kryterium | Content Calendar (Phase 1) | Analytics (Phase 2) |
|-----------|---------------------------|---------------------|
| **Złożoność techniczna** | Niska — własna PostgreSQL tabela + Bull job queue + UI calendar | Wysoka — GA4 API + Google Search Console + OAuth per user + GDPR |
| **Zależności zewnętrzne** | Brak (w pełni pod kontrolą zespołu) | 3 zewnętrzne API, każde z innymi rate limits i auth flow |
| **Czas do wartości** | ~6 tygodni, wartość widoczna od pierwszego planowania | ~4 miesiące, wartość widoczna dopiero po 30+ dniach danych historycznych |
| **Ryzyko blokady** | Brak ryzyk zewnętrznych | GA4 delays 24h, GSC bot detection, LinkedIn API approval 4-6 tygodni |

**Kluczowa zależność**: Analytics bez danych historycznych jest bezużyteczne. Content Calendar generuje regularne dane → Analytics je analizuje. Fazy muszą iść w tej kolejności. Budowanie Analytics pierwszego = płacenie za feature który nie może działać przez pierwsze 2 miesiące.

---

#### 1C: Dlaczego te konkretne Acceptance Criteria?

**Przykład — AC dla Team Collaboration, story US-TC-001:**

> *"Jako Admin mogę zaprosić Editora / Reviewera — konto aktywne po kliknięciu linku (wygasa 48h)"*

Każdy element ma uzasadnienie:
- **48h expiry**: standardowy security pattern (krótszy niż GitHub/Google = 7 dni). Balans bezpieczeństwo vs UX (pracownik ma czas zrealizować w ciągu 2 dni roboczych)
- **Tylko Admin może zapraszać**: zapobiega "invite sprawl" — każdy member nie może sam rozrastać teamu bez wiedzy płatnika
- **Konto aktywne po kliknięciu, nie od razu**: email confirmation = weryfikacja że adres jest prawdziwy (billing protection)

**Przykład — AC dla Analytics, data freshness:**

> *"Dane z GA4 odświeżane co 24h, z Search Console co 48h"*

Uzasadnienie: GA4 API ma wbudowany 24h data processing delay (dokumentacja Google). Obiecywanie "real-time" byłoby kłamstwem. AC odzwierciedla rzeczywiste możliwości API, nie życzenia.

---

#### 1D: Dlaczego RBAC z 3 rolami (Admin / Reviewer / Editor), a nie 2 albo 5?

**Dlaczego nie 2 role (Admin/Reviewer):**
Brak roli Editor oznaczałby, że Reviewer musiałby mieć dostęp do edycji artykułów. W kontekście agencji: copywriter nie powinien móc zmieniać już zatwierdzonych treści. Merge roli = naruszenie separacji odpowiedzialności.

**Dlaczego nie 5 ról (np. +SuperAdmin +Viewer):**
Floowe to produkt SME, nie enterprise. SuperAdmin to over-engineering na tym etapie (1 organizacja = 1 konto billing). Viewer (read-only) to nice-to-have, nie user story z demand — do Phase 4.

**Model uprawnień:**

| Akcja | Admin | Reviewer | Editor |
|-------|-------|----------|--------|
| Tworzy artykuł | ✅ | ❌ | ✅ |
| Edytuje artykuł | ✅ | ❌ | ✅ (własne) |
| Zatwierdza/odrzuca | ✅ | ✅ | ❌ |
| Publikuje | ✅ | ❌ | ❌ |
| Zarządza teamem | ✅ | ❌ | ❌ |
| Widzi billing | ✅ | ❌ | ❌ |

---

#### 1E: Dlaczego Google Analytics 4, a nie Matomo / Mixpanel / własna analityka?

| Narzędzie | Powód odrzucenia |
|-----------|-----------------|
| **Matomo** | Self-hosted → infrastruktura + maintenance po stronie użytkownika → bariera wejścia za wysoka dla SME |
| **Mixpanel** | Skoncentrowany na event tracking aplikacji, nie na SEO/content performance — błędne narzędzie do problemu |
| **Własna analityka** | Wymaga śledzenia kodu na każdej stronie klienta → problem zgody właściciela domeny → nierealistyczne |
| **GA4** ✅ | 95%+ polskich SME już ma GA4 na swojej stronie (zero konfiguracji po stronie klienta), oficjalne API, dobrze udokumentowane |

**Dlaczego Google Search Console dodatkowo:**
GA4 mierzy **ruch** (ile osób weszło). GSC mierzy **widoczność** (na ile fraz Google pokazuje stronę). Razem dają pełny obraz ROI — to kluczowe dla uzasadnienia wartości Floowe.

---

#### 1F: Jak powstały szacunki godzinowe (120-240h)?

Metodologia **T-shirt sizing z dekompozycją** (3 warstwy):

| Warstwa | Analytics (120-160h) | Calendar (160-200h) | Team Collab (200-240h) |
|---------|---------------------|---------------------|------------------------|
| **Backend API** | 40h (OAuth + 3 API integrations) | 30h (CRUD + Bull queue) | 60h (RBAC + workflow engine) |
| **Frontend UI** | 30h (charts, dashboard) | 50h (calendar drag-drop UI) | 40h (review UI, notifications) |
| **Baza danych** | 15h (schema, migracje) | 20h (schedule table, history) | 30h (roles, permissions, audit log) |
| **Testy + QA** | 20h | 30h | 40h |
| **Bufor** | 15h (API surprises) | 30h (UX iterations) | 30h (security audit) |

Bufor dla Analytics wyższy procentowo ze względu na nieciągłość zewnętrznych API. Bufor dla Calendar wyższy ze względu na UX complexity drag-and-drop kalendarza (rework risk).

---

### Kryterium 2 — Rozumienie diagramu Event Storming

#### 2A: Legenda — co oznacza każdy element

| Element | Kolor (konwencja) | Definicja | Przykład w diagramie Floowe |
|---------|--------------------|-----------|----------------------------|
| **Event** | 🟠 pomarańczowy | Fakt który się zdarzył — nieodwracalny, w czasie przeszłym | `ArticlePublished`, `PostCreatedOnFacebook` |
| **Command** | 🔵 niebieski | Żądanie zmiany stanu — może zostać odrzucone | `PublishArticle`, `CreateArticle`, `EditArticle` |
| **Actor** | 🟡 żółty | Człowiek lub system inicjujący komendę | `Content Manager`, `Scheduler (system)` |
| **Aggregate** | 🟨 żółty (obramowanie) | Encja biznesowa z logiką i regułami niezmienności | `Article`, `Editor`, `PublicationManager` |
| **Policy** | 🟣 fioletowy | Reguła "kiedy X, to wykonaj Y" — automatyczna reakcja na event | `AutoAdaptContentToChannels` |
| **Bounded Context** | ramka/subgraph | Logiczna granica domeny gdzie pojęcia mają jednoznaczne znaczenie | `BC: Content Creation`, `BC: Publication` |

---

#### 2B: Walkthrough AS-IS krok po kroku

Diagram przesuwa się od lewej (Content Creation) do prawej (Publication). Oto pełny ślad jednej sesji użytkownika:

```
[AKTOR: Content Manager] 
    │
    │── KOMENDA: CreateArticle
    ▼
[AGREGAT: Article]  ← tworzy się rekord, status = DRAFT
    │
    │── EVENT: ArticleContentGenerated  ← AI wygenerował treść
    ▼
[AGREGAT: Editor]  ← użytkownik widzi WYSIWYG
    │
    │── KOMENDA: EditArticle / AddImages / UpdateSEOMeta  ← 3 komendy, mogą też się nie wykonać
    ▼
    │── EVENT: ArticleEdited / ImagesAdded / SEOMetaUpdated  ← 3 eventy zapisane w historii
    ▼
[AGREGAT: PublicationManager]  ← użytkownik wybiera kanały (Website, FB, LI, X)
    │
    │── KOMENDA: PublishArticle(articleId, channels=[FB, LI, X, Website])
    ▼
[POLICY: AutoAdaptContentToChannels]  ← AUTOMATYCZNA REAKCJA na komendę
    │  Reguły: Website=full article, FB=image+excerpt+link, LI=professional tone, X=thread 280ch
    │
    │── EVENT: ArticlePublished  ← status Article → PUBLISHED
    ▼
    ├── EVENT: PostCreatedOnFacebook
    ├── EVENT: PostCreatedOnLinkedIn
    ├── EVENT: ThreadCreatedOnX
    └── EVENT: ArticleAddedToWebsite
    ▼
[AGREGAT: PublicationHistory]  ← zapisuje pełny log "co, kiedy, gdzie"
```

**Dlaczego PublicationHistory jako oddzielny Agregat?**: Publication Manager odpowiada za *decyzję* (gdzie i kiedy publikować). History odpowiada za *zapis* (co się stało). Separacja pozwala queryować historię bez dotykania logiki decyzyjnej.

---

#### 2C: Dlaczego te konkretne eventy, a nie inne?

Zasada selekcji: event musi być **istotny biznesowo** lub **wyzwalać dalszą logikę**. Przykłady co pominąłem i dlaczego:

| Pominięty event | Dlaczego pominięty |
|----------------|-------------------|
| `UserScrolledEditor` | Zdarzenie UI, nie domeny biznesowej |
| `ArticleSavedAsDraft` | Autosave — techniczny detail, nie zmienia stanu biznesowego |
| `UserClickedPublishButton` | To jest Akcja UI → generuje ona Komendę `PublishArticle`, nie jest Eventem |
| `ImageUploadStarted` | Pośredni krok procesu — Event `ImagesAdded` (kompletny fakt) jest wystarczający |

---

#### 2D: Co robi Policy i kiedy się wyzwala?

**`AutoAdaptContentToChannels`** jest Polityką która wyzwala się po Komendzie `PublishArticle`. Jej zadaniem jest transformacja treści dla każdego kanału:

```
Komenda: PublishArticle(channels=[FB, LI, X, Website])
    │
    └─ POLICY: AutoAdaptContentToChannels
          ├─ dla Website: publikuje pełny artykuł (HTML, wszystkie obrazy, meta SEO)
          ├─ dla Facebook: generuje excerpt (pierwsze 150 znaków) + featured image + URL
          ├─ dla LinkedIn: przepisuje tonem profesjonalnym (B2B framing, hashtagi branżowe)
          └─ dla X: rozbija treść na wątki max 280 znaków (thread format)
```

**Dlaczego Policy, a nie zwykła funkcja w kodzie?**: Policy w Event Storming sygnalizuje *regułę biznesową*, nie implementację. Decyzja *jak* ją zaimplementować (middleware, event handler, saga) to kwestia techniczna. Rozdzielamy model biznesowy od implementacji.

---

#### 2E: Granice Bounded Context — dlaczego takie, a nie inne?

| Bounded Context | Własne pojęcie "Article" | Własne reguły |
|----------------|--------------------------|---------------|
| `Content Creation` | `{id, title, content, seoMeta, status: DRAFT}` | AI może generować treść, WYSIWYG edytor |
| `Publication` | `{articleId, channels, publishedAt, adaptedContent{}}` | Każdy kanał ma inne limity znaków i formaty |
| `Collaboration` (TO-BE) | `{articleId, authorId, reviewerId, approvalStatus}` | Workflow approval, uprawnienia per-rola |
| `Analytics` (TO-BE) | `{articleId, pageViews, ranking, engagementRate}` | Read-only view z zewnętrznych źródeł, brak mutacji |

**Jak widać granicę**: Kiedy `Article` w dwóch kontekstach ma inny kształt i inne reguły **→** to są 2 Bounded Contexts. Scalenie ich w jeden Agregat spowodowałoby, że model danych stałby się niespójny i logika się poplątała.

---

### Kryterium 3 — Różnica Event / Komenda / Akcja UI / Policy / Agregat

#### 3A: Tabela wszystkich 5 elementów

| Element | Kierunek | Odwracalny? | Może być odrzucony? | Przykład w Floowe |
|---------|----------|-------------|---------------------|-------------------|
| **Akcja UI** | User → System | ✅ (nic nie zapisano) | n/d (to tylko kliknięcie) | Kliknięcie przycisku „Opublikuj" |
| **Komenda** | User/System → Agregat | ✅ (jeśli odrzucona) | ✅ (np. limit artykułów = 0) | `PublishArticle(articleId, channels[])` |
| **Event** | Agregat → Historia | ❌ (nieodwracalny) | ❌ (już się stało) | `ArticlePublished`, `PostCreatedOnFacebook` |
| **Policy** | Event → Komenda | n/d (automatyczna) | ✅ (jeśli warunek nie spełniony) | `AutoAdaptContentToChannels` po `ArticlePublished` |
| **Agregat** | Encja z regułami | n/d | Chroni niezmienność | `Article` (nie może być Published bez title) |

---

#### 3B: Pełny trace — od jednego kliknięcia do wszystkich eventów

```
[Użytkownik klika "Opublikuj na wszystkich kanałach"]
        │
        │  AKCJA UI (warstwa prezentacji — przeglądarka, zero logiki)
        ▼
[Frontend wysyła żądanie HTTP POST /articles/{id}/publish]
        │
        │  KOMENDA: PublishArticle(articleId="abc-123", channels=["FB","LI","X","Website"])
        ▼
[AGREGAT: Article — weryfikuje niezmienność]
    Reguła: czy artykuł jest w statusie DRAFT? ✅
    Reguła: czy użytkownik ma artykuły w limicie planu? ✅
    Reguła: czy wybrany co najmniej 1 kanał? ✅
        │
        │  EVENT: ArticlePublished (status: DRAFT → PUBLISHED, publishedAt: now())
        ▼
[POLICY: AutoAdaptContentToChannels — wyzwolona przez ArticlePublished]
        │
        ├─ EVENT: ArticleAddedToWebsite (pełny artykuł, WordPress API call)
        ├─ EVENT: PostCreatedOnFacebook (excerpt + image, Graph API call)
        ├─ EVENT: PostCreatedOnLinkedIn (professional format, LinkedIn API call)
        └─ EVENT: ThreadCreatedOnX (thread 280ch, X API call)
        │
        ▼
[AGREGAT: PublicationHistory — zapisuje pełny log]
    EVENT: PublicationRecorded({articleId, channels, timestamp, statuses})
        │
        ▼
[User Interface odświeża widok — "Opublikowano na 4 kanałach ✅"]
```

**Ważne**: Komendy inicjuje człowiek lub scheduler. Eventy generuje system. Policy to automatyczna reguła łącząca jeden Event z kolejną Komendą.

---

#### 3C: Edge cases — kiedy coś jest Eventem, a kiedy Komendą?

**Pytanie**: `UserCreatedAccount` — Event czy Komenda?

Odpowiedź: `CreateAccount` to **Komenda** (może być odrzucona — email już zajęty). `AccountCreated` to **Event** (fakty w czasie przeszłym — konto istnieje). Konwencja: Komendy = tryb rozkazujący, Eventy = czas przeszły.

**Pytanie**: `ScheduledPublicationTriggered` — kto jest Aktorem?

Odpowiedź: **System** (scheduler, np. Bull job queue). Actor nie musi być człowiekiem — cron job / scheduler jest Aktorem systemowym.

**Pytanie**: Dlaczego Event jest nieodwracalny?

Odpowiedź: Event Sourcing zasada — historia jest append-only. Żeby "cofnąć" PublishArticle nie usuwa się eventu ale tworzy nowy: `ArticleUnpublished`. Pełny audit trail = historia nigdy nie jest modyfikowana, tylko rozszerzana.

---

### Kryterium 4 — Uzasadnienie biznesowe z miernikami sukcesu

#### Feature #1: Real-Time Analytics Dashboard

**Persona**: Właściciel małego biznesu (e-commerce, blog ekspercki, usługi lokalne), 30-50 lat, publikuje 4-8 artykułów/miesiąc, nie ma analityka w zespole.

**Problem**: Płaci 500 PLN/m za Floowe. Po 60 dniach nie widzi wzrostu ruchu (bo efekty SEO pojawiają się po 90+ dniach). Nie wie że to normalne. Anuluje. Churn.

**Wartość**: Dashboard pokazuje dane pośrednie (rankings improving, impressions growing) zanim pojawi się ruch. Użytkownik widzi że "idzie w dobrym kierunku" → zostaje.

**Dlaczego nie Google Analytics bezpośrednio?**: GA4/GSC to narzędzia dla analityków. Floowe agreguje dane w jednym miejscu z interpretacją ("Twój artykuł o [X] wspiął się z pozycji 45 na 12 w Google") — kontekst i wartościowanie jest nieobecne w surowym GA4.

**KPIs sukcesu** (jak zmierzymy że funkcja zadziałała):

| Metryka | Baseline (przed) | Target (po 3 miesiącach) | Jak mierzyć |
|---------|-------------------|--------------------------|-------------|
| Monthly retention rate | ~60% (szacunek branżowy) | ≥70% | Kohortowa analiza churnu w Floowe billing |
| Feature engagement | 0% | ≥40% DAU otwiera dashboard | Product analytics (Mixpanel/Amplitude) |
| NPS po wdrożeniu | nieznany | +15 punktów | Post-release survey |

---

#### Feature #2: Content Calendar & Publishing Scheduler

**Persona**: Marketer treści w agencji lub in-house, publikuje zlecenia dla 3-10 klientów jednocześnie, potrzebuje organizacji tygodniowej.

**Problem**: Publikowanie ad-hoc (5 artykułów w poniedziałek, cisza do piątku) kasuje efekty SEO. Google preferuje regularność sygnałów crawlingowych. Użytkownik nie wie że publikuje źle.

**Dlaczego nie Google Calendar, Trello, Notion?**: Te narzędzia planują — Floowe wykonuje. Planowanie w Notion + ręczna publikacja = 2 narzędzia, context switching. Calendar w Floowe = planowanie + automatyczna publikacja w jednym miejscu.

**KPIs sukcesu**:

| Metryka | Baseline | Target (3 miesiące) | Jak mierzyć |
|---------|----------|---------------------|-------------|
| % użytkowników publikujących wg cyklu 3+/tydzień | ~20% | ≥40% | Analiza wzorców publikacji w Floowe DB |
| Avg. artykułów/miesiąc na konto aktywne | nieznany | +25% wzrost | Query na tabeli articles |
| Churn wśród użytkowników Calendar vs bez | baseline | -15% churn w grupie z Calendar | A/B segment cohort |

---

#### Feature #3: Team Collaboration & Review Workflow

**Persona**: Właściciel agencji contentowej (3-15 copywriterów), Manager marketingu w SME (2-5 osób content team), brand manager dbający o spójność komunikacji.

**Problem**: Jeden login do Floowe → jeden człowiek publikuje → brak kontroli jakości → agencja nie może dać klientowi pewności że niezweryfikowana treść nie trafi na kanały.

**Dlaczego nie osobne narzędzie (Asana, Monday.com)?**: Workflow approval oddzielony od narzędzia publikacji = duplikacja pracy. Approval w Floowe ≡ "zatwierdzam treść i kanały" — action directly connected to outcome.

**KPIs sukcesu**:

| Metryka | Baseline | Target (3 miesiące) | Jak mierzyć |
|---------|----------|---------------------|-------------|
| ARPU (Average Revenue Per User) | ~500 PLN/konto/m | ≥750 PLN/konto/m (team seats) | Billing analytics |
| % kotów z ≥2 użytkownikami | 0% | ≥15% | DB query users_per_account |
| Konwersja trial → paid dla segment agencja | baseline | +20% vs solo baseline | Segment tag w CRM |

---

### Dodatkowe: Założenia których nie można potwierdzić bez dostępu do kodu

| Założenie | Dlaczego ważne | Ryzyko jeśli błędne |
|-----------|----------------|---------------------|
| Stack: React + Node.js + PostgreSQL | Wpływa na koszt integracji job queue (Bull vs Sidekiq) | Różni się o ~40h jeśli inny stack |
| Architektura: monolith, nie microservices | Nowe serwisy Analytics/Collab łatwiej dodać do monolitu inaczej niż do micro | Koszt może wzrosnąć 2x |
| WordPress integration istnieje | W specyfikacji zakładamy ten kanał jako działający | Jeśli nie istnieje — dodatkowy BC: StaticSiteAdapter |
| GA4 na stronie każdego klienta | Kluczowe dla złożoności onboardingu Analytics | Bez GA4 user musi zainstalować tracking — bariera wejścia ~3x wyższa |
| Liczby retention (+40%) | Szacunki branżowe (Mixpanel, Baremetrics benchmarks), nie dane Floowe | Cel retencji może być inny, ale kierunek decyzji ten sam |

---

## 📞 Kontakt / Pytania

Analiza dostępna do dyskusji. Gotów obronić każde design decision i wyjaśnić diagram Event Storming.

---

**Version**: 2.0  
**Last Updated**: Marzec 2026  
**Status**: ✅ Ready for Technical Interview
