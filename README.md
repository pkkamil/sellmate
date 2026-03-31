# SellMate

SellMate is a premium AI-powered tool for analyzing items from photos to provide optimal selling prices and category suggestions.

## Project Structure

- **`/backend`**: Laravel 13 API (running via Docker/Sail).
- **`/frontend`**: Next.js 16 application (running locally).

## Tech Stack

- **Backend**: PHP 8.3, Laravel 13, PostgreSQL, Redis, Gemini AI.
- **Frontend**: React 19, Next.js 16, Tailwind CSS 4, Lucide React.
- **Infrastructure**: Docker, Laravel Sail.

## Getting Started

### 1. Clone the Project
To clone the repository along with all submodules, use:

```bash
git clone --recursive <repository-url>
```

If you have already cloned the repository without submodules, run:

```bash
git submodule update --init --recursive
```

### 2. Setup (Root-level Orchestration)
The project is orchestrated using a root-level `docker-compose.yml`.

```bash
# Start all services (Frontend + Backend)
docker-compose up -d

# Initial backend setup
docker exec -it sellmate_api php artisan key:generate
docker exec -it sellmate_api php artisan migrate --seed
```

The frontend will be available at [http://localhost:3000](http://localhost:3000) and the backend API at [http://localhost:8000](http://localhost:8000).

## Architecture & Code Standards

We follow a strict **Service-Action** pattern on the backend and a **Feature-based** structure on the frontend. See the inner `README.md` files for more details.
