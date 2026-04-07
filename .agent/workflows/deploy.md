---
description: Faza wdrażania zadania - przygotowanie i wypchnięcie zmian na produkcję.
---

1. Sprawdź, czy konfiguracja w `.github/workflows/main.yml` jest poprawna i czy wszystkie kroki CI przechodzą.
2. Przygotuj listę nowych zmiennych środowiskowych (`.env`), które muszą zostać dodane do DigitalOcean.
3. Wykonaj ostatni build lokalny i upewnij się, że nie ma błędów.
// turbo
4. `cd frontend && yarn build && cd ..`
5. Jeśli wszystko jest gotowe, wypchnij zmiany do gałęzi `master`.
// turbo
6. `git push origin main`
7. Monitoruj akcję w repozytorium na GitHubie i upewnij się, że wdrożenie do DigitalOcean przebiegło pomyślnie.
8. Po wdrożeniu wykonaj migracje bazy danych na serwerze (jeśli nie jest to częścią automatycznego procesu).