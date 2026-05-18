# Repository Guidelines

## Project Structure & Module Organization

GEOFlow is a Laravel 12 application. Backend code lives in `app/`: models in `app/Models`, controllers in `app/Http/Controllers`, jobs in `app/Jobs`, and domain services in `app/Services`. Routes are in `routes/web.php`, `routes/api.php`, `routes/console.php`, and `routes/channels.php`. Blade views and frontend entrypoints live in `resources/`; public assets, themes, previews, and fonts are under `public/`. Database files are in `database/`. Feature tests are in `tests/Feature`, with shared setup in `tests/TestCase.php`. Operational docs and deployment helpers are in `docs/` and `deploy-scripts/`.

## Build, Test, and Development Commands

- `composer setup`: install dependencies, create `.env`, generate the app key, migrate, and build assets.
- `composer dev`: run the Laravel server, queue listener, log tailing, and Vite dev server together.
- `composer test`: clear cached config and run the Laravel test suite.
- `php artisan test --filter=AdminArticlesPageTest`: run one focused PHPUnit test class.
- `npm run dev`: start Vite only.
- `npm run build`: build production frontend assets.
- `docker compose up -d`: start the Docker stack for PostgreSQL/Redis-backed development.

## Coding Style & Naming Conventions

Follow `.editorconfig`: UTF-8, LF line endings, four-space indentation, final newlines, and two-space YAML indentation. Use Laravel and PSR-4 conventions: `StudlyCase` classes, `camelCase` methods/properties, snake_case columns, and plural table names. Keep controllers thin; place business logic in `app/Services`, queued work in `app/Jobs`, and persistence behavior in Eloquent models. Format PHP with Laravel Pint via `./vendor/bin/pint`.

## Testing Guidelines

Tests use PHPUnit through Laravel’s test runner. Add feature coverage in `tests/Feature` for admin pages, API contracts, rendering, queues, and security-sensitive flows. Name tests after the behavior or surface under test, for example `AdminUsersManagementTest` or `KnowledgeChunkEmbeddingSyncTest`. Run `composer test` before opening a PR; use filtered `php artisan test` commands while iterating.

## Commit & Pull Request Guidelines

Recent history uses short imperative subjects, with occasional `fix:` prefixes, such as `Fix embedding knowledge chunk sync` and `fix: report image upload storage failures`. Keep commits focused and describe the user-visible change or bug fixed. Pull requests should include a concise summary, test results, linked issues when applicable, and screenshots for UI changes. Note migration, queue, scheduler, or environment-variable impact explicitly.

## Security & Configuration Tips

Do not commit `.env`, API keys, generated secrets, or private deployment data. Start from `.env.example` or `.env.prod.example`, and document new required variables. Treat admin authentication, AI provider credentials, upload handling, and queue execution paths as security-sensitive; include regression tests when changing them.
