# Kluczowe Przepływy Użytkownika i Procesy

## 1. PROCESY REJESTRACJI I LOGOWANIA

### 1.1 User Story - Rejestracja
```gherkin
Jako: Nowy użytkownik (przedsiębiorca)
Chcę: Szybko się zarejestrować w Floowe
Aby: Jak najszybciej zacząć tworzyć treści dla mojego biznesu

Kryteria Akceptacji:
- [ ] Mogę się zarejestrować poprzez email
- [ ] Mogę się zarejestrować poprzez Google/Facebook
- [ ] Po rejestracji jestem kierowany na onboarding
- [ ] Moje dane są bezpieczne (encryption, GDPR compliance)
- [ ] Otrzymuję email potwierdzający rejestrację
```

### 1.2 User Story - Logowanie
```gherkin
Jako: Zarejestrowany użytkownik
Chcę: Zalogować się do mojego konta Floowe
Aby: Uzyskać dostęp do moich artykułów i ustawień

Kryteria Akceptacji:
- [ ] Mogę się zalogować email i hasłem
- [ ] Mogę użyć social login (Google, Facebook)
- [ ] Jestem bezpiecznie zalogowany (JWT/Session)
- [ ] Mogę resetować hasło jeśli je zapomnę
- [ ] 2FA jest dostępne (dla Premium)
```

---

## 2. GŁÓWNE PRZYPADKI UŻYCIA (USE CASES)

### Use Case #1: TWORZENIE ARTYKUŁU Z SUGESTII AI
```
Aktor: Content Manager
Precondition: Użytkownik zalogowany,Subskrypcja aktywna

1. Użytkownik wchodzi do Dashboard
2. Klika "Nowy Artykuł"
3. System wyświetla "Sugestie Artykułów" (oparty AI na trendach branży)
4. Użytkownik wybiera sugestię (np. "Jak wybrać konto bankowe dla małego biznesu")
5. System generuje artykuł:
   - Nagłówek
   - Wstęp (hook)
   - Main body (3-5 sekcji)
   - Podsumowanie
   - Call-to-Action
   - Słowa kluczowe (SEO meta)
6. Artykuł pojawia się w edytorze WYSIWYG
7. Użytkownik może edytować tekst, grafikę
8. Użytkownik wybiera kanały publikacji (WWW, Facebook, LinkedIn, X)
9. Klika "Opublikuj"
10. Artykuł jest publikowany na wszystkich wybranych kanałach

Postcondition: Artykuł dostępny publicznie, licznik artykułów na planie zmniejszona
```

### Use Case #2: TWORZENIE ARTYKUŁU Z WŁASNEGO POMYSŁU
```
Aktor: Przedsiębiorca
Precondition: Użytkownik zalogowany, SubskrypcjaAktywna

1. Użytkownik klika "Nowy Artykuł"
2. Wybiera "Mój własny pomysł"
3. Wprowadza:
   - Temat/Nagłówek
   - Słowa kluczowe (3-5)
   - Długość artykułu (krótki/średni/długi)
   - Ton (profesjonalny/humorystyczny/akademicki)
4. System generuje artykuł
5. Artykuł pojawia się w edytorze
6. Użytkownik edytuje/dopasowuje
7. Dodaje grafikę (upload, stock image, AI generation)
8. Publikuje na wybranych kanałach

Postcondition: Artykuł opublikowany
Error Handling: Jeśli użytkownik osiągnął limit artykułów na planie → wyświetl ekran Upgrade
```

### Use Case #3: EDYCJA I PUBLIKACJA
```
Aktor: Content Manager
Precondition: Artykuł utworzony, w stanie DRAFT

1. Użytkownik otwiera artykuł z Draft
2. Edytuje tekst w WYSIWYG edytorze
3. Zmienia/dodaje grafikę
4. Edytuje meta-tagi SEO (title, description)
5. Przegląda preview artykułu
6. Klika "Opublikuj"
7. Opcjonalnie: Planuje publikację na konkretny czas
8. System publikuje na wybranych kanałach:
   - WWW: Dodaje do bloga
   - Facebook: Tworzy post z imageiem i linkiem
   - LinkedIn: Tworzy post z ułamkiem tekstu
   - X: Tworzy serie tweetów (thread) lub pojedynczy tweet
9. System zapisuje status publikacji dla każdego kanału

Postcondition: Artykuł w status PUBLISHED, historia publikacji dostępna
```

### Use Case #4: ZARZĄDZANIE KANAŁAMI PUBLIKACJI
```
Aktor: Administrator Konta
Precondition: Użytkownik zalogowany

1. Użytkownik wchodzi do ustawień "Kanały Publikacji"
2. Widzi listę połączonych kanałów:
   - Strona (WWW) - URL i kredencjały
   - Facebook - Token dostępu
   - LinkedIn - Token dostępu
   - X (Twitter) - API Keys
3. Może:
   - Dodać nowy kanał (Authorize OAuth)
   - Usunąć kanał (disconnect)
   - Testować połączenie
   - Zmieniać permisje/role
4. Dla każdego kanału może zobaczyć: ostatnia publikacja, status
5. Zapisuje zmiany

Postcondition: Kanały zaktualizowane, kolejne publikacje będą używać nowe ustawienia
```

### Use Case #5: WZNOWIENIE ARTYKUŁU Z ARCHIWUM
```
Aktor: Content Manager (Repurposing Use Case)
Precondition: Artykuł już opublikowany dostępny w archiwum

1. Użytkownik widzi archiwum opublikowanych artykułów
2. Wybiera stary artykuł (np. z 6 miesięcy temu)
3. Klika "Repurpose Article"
4. System oferuje opcje:
   - Zmodyfikuj i republlikuj
   - Stworz variacje (dla różnych kanałów)
   - Aktualizuj dane i republlikuj
5. Użytkownik dokonuje zmian
6. Publkuje jako nową publikację

Postcondition: Artykuł dostępny ponownie, maksymalizacja content asset
```

---

## 3. PRZEPŁYW PŁATNOŚCI

### 3.1 Wybór Planu - Upgrade Flow
```
Aktor: Użytkownik na planie Free
Precondition: Użytkownik zalogowany, osiągnął limit artykułów (3/miesiąc)

1. Użytkownik klika "Nowy Artykuł"
2. System wyświetla modal: "Osiągnąłeś limit. Upgrade!"
3. Wyświetla opcje planów:
   - Basic (500 PLN/miesiąc)
   - Standard (700 PLN/miesiąc)
   - Premium (900 PLN/miesiąc)
4. Zawiera wskaźnik promocji (50% za 3 miesiące)
5. Użytkownik klika "Upgrade do Basic"
6. Zostaje przekierowany do formularza płatności (STRIPE/Przelewy24)
7. Podaje dane karty
8. Płatność jest przetwarzana
9. Po potwierdzeniu: limit artykułów zostaje zmieniony, Feature flags aktualizowane

Postcondition: Użytkownik na nowym planie, może tworzyć więcej artykułów
Error: Jeśli płatność nie powiedzie się → wyświetl opcję retry
```

### 3.2 Billing & Subscription Management
```
Aktor: Administrator Konta
Precondition: Zalogowany, Plan płatny

1. Użytkownik wchodzi do "Ustawienia > Rozliczenia"
2. Widzi:
   - Bieżący plan (np. Standard)
   - Data następnej faktury
   - Historię płatności
   - Szczegóły karty
3. Może:
   - Zmienić plan (Upgrade/Downgrade)
   - Zarządzać kartą
   - Pobrać faktury
   - Anulować subskrypcję
4. Przejścia są obsługiwane z proratą

Postcondition: Subskrypcja zarządzana
```

---

## 4. INTEGRACJE ZEWNĘTRZNE - PRZEPŁYWY

### 4.1 Integracja Facebook
```
1. Administrator klika "Połącz Facebook"
2. Zostaje przekierowany do Facebook OAuth
3. Zaloguje się na Facebook
4. Zatwierdza permisje (publication, page management)
5. Token jest zapisany w systemie (encrypted)
6. Strona Facebook jest wybrana
7. Przy publikacji: System wysyła POST do Facebook Graph API
8. Artykuł pojawia się jako post na stronie

Technical Stack Assumption: Node.js + facebook-sdk
```

### 4.2 Integracja Google Search Console
```
1. Administrator klika "Połącz Google Search Console"
2. OAuth redirect do Google
3. Zatwierdza dostęp
4. Floowe otrzymuje dostęp do Search Console data
5. Dashboard wizualizuje:
   - Searche keywords
   - Click-through rate
   - Average position
6. Sugestie artykułów są oparte na Search Console data

Technical Stack: Google Search Console API v1
```

---

## 5. CORE BUSINESS METRICS & KPIs

### Metryki Śledzenia dla Użytkownika
```
Per Article:
- Publikacja: WWW, Facebook, LinkedIn, X (status dla każdego)
- Views (jeśli dostępne)
- Likes/Shares (zintegrowane z API social)
- Click-through Rate (z link shortener)
- Ranking w Google (z GSC data)

Per User:
- Active articles (published/draft)
- Monthly article quota usage
- Channels connected
- Last publication date
- Churn risk (nie publikował 30 dni)
```

---

## 6. PODSUMOWANIE - MAPOWANIE PROCESÓW

| Proces | Aktor | Czas | Kolumny | Priority |
|--------|-------|------|---------|----------|
| Rejestracja | New User | 2 min | Auth, Profile | P0 |
| Tworzenie Artykułu (AI) | Content Manager | 5-10 min | Editor, Generator | P0 |
| Edycja Artykułu | Content Manager | 3-5 min | Editor, Preview | P0 |
| Publikacja Multikanałowa | Content Manager | 1 min | Publisher, Notifications | P0 |
| Upgrade do Płatnego Planu | User | 3 min | Billing, Payment Gateway | P0 |
| Integacja Kanałów | Admin | 5-10 min | OAuth, Credentials | P1 |
| Analytics & Reporting | Manager | 10 min | Dashboard, Data | P1 |

