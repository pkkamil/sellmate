---
description: Faza tworzenia Pull Requestów dla projektów z submodułami (backend, frontend, root).
---

// turbo-all
1. Sprawdź, które komponenty mają zmiany:
   - Root: `git status --short`
   - Backend: `cd backend && git status --short && cd ..`
   - Frontend: `cd frontend && git status --short && cd ..`
2. Wygeneruj jedną, spójną nazwę gałęzi dla całego zadania (np. `feat/auth-v2`) i poproś o akceptację.
3. Dla każdego komponentu z wykrytymi zmianami (Backend, Frontend, Root):
   - Przejdź do katalogu komponentu.
   - Utwórz nową gałąź (lub przełącz się na istniejącą, jeśli już na niej jesteś): `git checkout -b <nazwa-gałęzi>`.
   - Przygotuj podsumowanie zmian specyficzne dla tego komponentu.
   - Zacommituj zmiany: `git add . && git commit -m "<prefix>(<komponent>): <opis-zmian>"`.
   - Wypchnij gałąź: `git push origin <nazwa-gałęzi>`.
   - Utwórz Draft Pull Request:
// turbo
   - `gh pr create --draft --assignee "@me" --title "<Tytul>" --body "<Opis>" --label "enhancement"`
   - Zapamiętaj link do PR.
4. Jeśli zmiany w submodułach zostały wypchnięte (Backend/Frontend), zaktualizuj ich piny w repozytorium głównym (Root):
   - W katalogu głównym: `git add backend frontend`.
   - Zacommituj piny: `git commit -m "chore: update submodule pins"`.
   - Wypchnij nową gałąź i stwórz Draft PR w repozytorium `pkkamil/sellmate`, dodając linki do pozostałych PR-ów w opisie.
5. Poinformuj użytkownika o wszystkich utworzonych PR-ach wraz z linkami.
