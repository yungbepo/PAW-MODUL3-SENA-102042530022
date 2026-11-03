# Copilot instructions

## Project overview

- This is a Laravel 12 application (PHP 8.2+) for managing a book-lending system.
- The main request flow is defined in `routes/web.php`: routes call controllers, controllers validate requests and use Eloquent models, and controllers return Blade views under `resources/views`.
- `Buku`, `Anggota`, and `Peminjaman` use the explicitly named `buku`, `anggota`, and `peminjaman` tables. Their schemas and foreign keys are defined in `database/migrations`.
- A loan belongs to one book and one member; books and members each have many loans. Keep relationship method names consistent with their use in controllers and Blade views.
- Routes for the application are grouped behind `auth` and `role:admin`; login routes use the `guest` middleware.
- `PANDUAN_PRAKTIKUM.md` defines an ordered sequence of TODOs. Later tasks may depend on earlier ones; use it together with the inline TODO comments when changing tutorial code.

## Commands

- Run the test suite: `php artisan test` (or `composer test`).
- Run one test file: `php artisan test tests/Feature/SistemPeminjamanBukuTest.php`.
- Run one test method: `php artisan test --filter=test_admin_can_create_book`.
- Check PHP formatting without changing files: `vendor/bin/pint --test`.
- Format PHP files: `vendor/bin/pint`.
- Build frontend assets: `npm run build`.

Feature tests use `RefreshDatabase` and the in-memory SQLite database configured in `phpunit.xml`.

## Repository-specific conventions

- When adding or changing persisted fields, keep the model's `$fillable`, migration columns, controller validation, and form field names aligned. The models explicitly set table names because the Indonesian table names do not follow Eloquent's default pluralization reliably.
- Store and update actions validate request data before passing the validated array to Eloquent `create()` or `update()`. Do not pass the entire request payload to mass assignment.
- Keep authorization consistent with the existing route middleware groups; application CRUD routes are admin-only.
- Preserve the Indonesian labels and messages used by the UI and controllers.
- For model relationships, specify foreign-key names explicitly where the schema uses keys such as `anggota_id` and `buku_id`.
