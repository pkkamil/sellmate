---
description: Faza testowania zadania - weryfikacja poprawności kodu i UI.
---

1. Uruchom testy automatyczne na backendzie i frontendzie.
// turbo
2. `./vendor/bin/sail artisan test`
// turbo
3. `./vendor/bin/sail pint`
// turbo
4. `./vendor/bin/sail phpstan`
// turbo
5. `cd frontend && yarn test && cd ..`
// turbo
6. `cd frontend && yarn lint && cd ..`

**Opcjonalnie: Testy AI UI**
7. Użyj narzędzia `browser_subagent`, aby:
    - Otworzyć aplikację lokalnie (`http://localhost:3000`).
    - Sprawdzić, czy nowe funkcjonalności są poprawnie wyświetlane.
    - Zrobić zrzuty ekranu i nagrania w celu weryfikacji estetyki (glassmorphism, gradienty).
    - Jeśli zauważysz błędy wizualne, automatycznie przejdź do fazy naprawy i powtórz testy.
8. Potwierdź, że wszystkie testy przeszły pomyślnie.
