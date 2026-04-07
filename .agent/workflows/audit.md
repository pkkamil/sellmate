---
description: Rygorystyczny audyt i automatyczna poprawa kodu pod kątem .cursorrules.
---

// turbo-all
Ten workflow wykonuje kompletny audyt bazy kodu i automatycznie poprawia błędy niezgodne z `.cursorrules`.

1. **Wybór zakresu (Interakcja)**: Zapytaj użytkownika: „Czy audyt ma objąć cały workspace, czy tylko ostatnio zmienione i niezatwierdzone pliki (git diff + untracked)?”.
    - Jeśli użytkownik wybierze **niezatwierdzone zmiany**:
        - Użyj `git status --short` oraz `git diff --name-only`, aby zidentyfikować pliki do audytu.
        - Ogranicz skanowanie w kolejnych krokach TYLKO do tych plików.
    - Jeśli użytkownik wybierze **cały workspace**:
        - Postępuj zgodnie z pełnym audytem poniżej.

2. **Analiza reguł**: Przeczytaj aktualną treść `.cursorrules`, aby upewnić się, że znasz wszystkie aktywne zasady (zwróć szczególną uwagę na zakaz FQCN dla klas globalnych jak `\Exception`).

3. **Audyt Backend (PHP)**:
    - Przeskanuj pliki (w wybranym zakresie) w `backend/app` pod kątem użycia w pełni kwalifikowanych nazw klas (FQN). Zwróć szczególną uwagę na klasy z globalnej przestrzeni nazw (np. `\Exception`, `\DateTime`, `\stdClass`) – muszą one zostać zamienione na import `use` i krótką nazwę.
    - Upewnij się, że każdy plik PHP zaczyna się od `declare(strict_types=1);`.
    - Sprawdź kontrolery API (`backend/app/Http/Controllers/Api`) pod kątem hardkodowanych odpowiedzi `response()->json()`. Zamień je na ustandaryzowane metody z trait-a `ApiResponse` korzystając z Enuma `ApiResponseMessage`.
    - Zweryfikuj, czy wszystkie wiadomości (messages) w odpowiedziach API pochodzą z Enuma/tłumaczeń, a nie są surowymi stringami.

4. **Audyt Frontend (React)**:
    - Przeskanuj komponenty (w wybranym zakresie) w `frontend/src/components` pod kątem hardkodowanych stringów w UI. Wszystkie teksty (poza nazwami własnymi jak "SellMate") muszą być wywołaniami `t()`.
    - Sprawdź importy w `frontend/src`. Wszystkie importy muszą być absolutne (zaczynające się od `@/`), a nie relatywne (`../../`).

5. **Automatyczna poprawa**: Napraw każde znalezione naruszenie rygorystycznie i bez pytania o potwierzenie dla oczywistych poprawek (zgodnie z `.cursorrules` i nową zasadą dotyczącą klas globalnych).

6. **Raport**: Po zakończeniu przygotuj krótkie podsumowanie wykonanych poprawek w formie `walkthrough.md`.
