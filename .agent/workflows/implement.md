---
description: Faza implementacji zadania - pisanie kodu i realizacja planu.
---

1. Stwórz artefakt `task.md`, aby śledzić postępy w zadaniu.
2. Zaimplementuj logikę biznesową w `backend/app/Services` oraz akcje, jeśli to konieczne.
3. Jeśli wprowadzasz zmiany na backendzie:
    - Używaj `declare(strict_types=1);`.
    - Pamiętaj o typowaniu parametrów i zwracanych wartości.
    - Twórz lub aktualizuj migracje bazy danych w `backend/database/migrations`.
4. Jeśli wprowadzasz zmiany na frontendzie:
    - Utrzymuj architekturę feature-based w `frontend/src/`.
    - Wszystkie teksty w UI muszą być przetłumaczone (użyj `useTranslation`).
    - Zadbaj o responsywność i styl SellMate (szkło, gradienty, nowoczesność).
5. Aktualizuj artefakt `task.md` po każdym ukończonym etapie.
