---
description: Faza końcowa - audyt zmienionego kodu oraz automatyczne utworzenie Pull Requestów.
---

// turbo-all
Ten workflow wykonuje rygorystyczny audyt tylko zmienionych plików, automatycznie je naprawia, a następnie tworzy gotowe Pull Requesty (nie drafty) dla wszystkich komponentów.

### 1. Audyt Zmian
1. **Identyfikacja plików**: Użyj `git status --short` oraz `git diff --name-only`, aby zidentyfikować pliki do audytu (untracked + modified).
2. **Analiza reguł**: Przeczytaj aktualną treść `.cursorrules`.
3. **Audyt Backend (PHP)**:
    - Przeskanuj zmienione pliki PHP pod kątem:
        - `declare(strict_types=1);` na początku.
        - Zakazu FQN (używaj `use` dla wszystkich klas, w tym globalnych jak `Exception`, `DateTime`).
        - Użycia Enuma `ApiResponseMessage` i trait-a `ApiResponse` zamiast hardkodowanych `response()->json()`.
        - Braku surowych stringów w wiadomościach API (używaj tłumaczeń/enumów).
4. **Audyt Frontend (React)**:
    - Przeskanuj zmienione komponenty pod kątem:
        - Hardkodowanych stringów (używaj `t()`).
        - Absolutnych importów (`@/` zamiast `../../`).
5. **Automatyczna poprawa**: Napraw wszystkie naruszenia rygorystycznie i bez pytania o potwierdzenie.

### 2. Przygotowanie PR
1. **Sprawdź komponenty**: Zidentyfikuj, które komponenty mają zmiany po audycie:
   - Root: `git status --short`
   - Backend: `cd backend && git status --short && cd ..`
   - Frontend: `cd frontend && git status --short && cd ..`
2. **Nazwa gałęzi**: Wygeneruj jedną, spójną nazwę gałęzi dla całego zadania (np. `feat/feature-name`) i poproś o akceptację.
3. **Tworzenie PR dla Submodułów (Backend/Frontend)**:
   Dla każdego komponentu (Backend, Frontend) z wykrytymi zmianami:
   - Przejdź do katalogu komponentu.
   - Utwórz/przełącz gałąź: `git checkout -b <nazwa-gałęzi>`.
   - Przygotuj szczegółowe podsumowanie zmian w `/tmp/pr_body.md` (Opis, Zmiany, Weryfikacja).
   - Zacommituj: `git add . && git commit -m "<prefix>(<komponent>): <opis-zmian>"`.
   - Wypchnij: `git push origin <nazwa-gałęzi>`.
   - Utwórz Pull Request (GOTOWY, nie draft):
     `gh pr create --assignee "@me" --title "<Tytul>" --body-file /tmp/pr_body.md --label "enhancement"`
   - Zapamiętaj link do PR.

### 3. Finalizacja (Root)
1. **Aktualizacja pinów**: Jeśli submoduły zostały wypchnięte, w katalogu głównym:
   - `git add backend frontend`.
   - `git commit -m "chore: update submodule pins"`.
2. **Utwórz Root PR**:
   - Przygotuj opis w `/tmp/root_body.md` zawierający linki do PR-ów submodułów.
   - Wypchnij gałąź root i stwórz Pull Request (READY):
     `gh pr create --assignee "@me" --title "<Tytul>" --body-file /tmp/root_body.md --label "enhancement"`
3. **Raport**: Poinformuj użytkownika o wszystkich utworzonych PR-ach wraz z linkami oraz podsumuj wykonane poprawki audytowe.
