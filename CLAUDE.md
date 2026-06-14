# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Spendly** is a personal expense tracking web application built as a step-by-step tutorial scaffold. The frontend design is complete; most backend logic is intentionally left as stubs for implementation.

**Stack:** Python 3 + Flask 3.1 | SQLite | Jinja2 templates | Vanilla CSS + JS

## Commands

```bash
# Run the development server (port 5001)
python app.py

# Install dependencies
pip install -r requirements.txt

# Run tests
pytest

# Run a single test file
pytest tests/test_auth.py

# Run a single test by name
pytest -k "test_login"
```

## Architecture

### Entry Point & Routing (`app.py`)
All Flask routes live in `app.py`. Fully implemented routes: `/`, `/login`, `/register`, `/terms`, `/privacy`. Stub routes awaiting implementation: `/logout` (Step 3), `/profile` (Step 4), `/expenses/add` (Step 7), `/expenses/<id>/edit` (Step 8), `/expenses/<id>/delete` (Step 9).

### Database (`database/db.py`)
SQLite database module. Must implement three functions:
- `get_db()` — returns a connection with `row_factory` and foreign keys enabled
- `init_db()` — creates tables with `CREATE TABLE IF NOT EXISTS`
- `seed_db()` — inserts sample development data

### Templates (`templates/`)
Jinja2 templates extend `base.html`. Available blocks: `title`, `head`, `content`, `scripts`. The base layout includes the navbar, footer, Google Fonts (DM Serif Display + DM Sans), `style.css`, and `main.js`.

### Styling (`static/css/style.css`)
Vanilla CSS using custom properties defined on `:root`. Key variables: `--accent` (forest green `#1a472a`), `--accent-2` (gold `#c17f24`), `--ink`, `--paper`, `--danger`. Responsive breakpoints at 900px and 600px.

## Coding Standards

### CSS & JS Namespacing
All application-specific CSS classes must use the `ody_` prefix to avoid conflicts. All JS functions must use the `ody_` prefix.

### Multi-language / Dictionary System
All user-visible text must use dictionary keys — never hard-code display strings in templates or JS. Key naming conventions:
- `LBL_SPENDLY_*` — labels (e.g., `LBL_SPENDLY_EMAIL`)
- `ERR_SPENDLY_*` — error messages (e.g., `ERR_SPENDLY_INVALID_EMAIL`)
- `MSG_SPENDLY_*` / `TXT_SPENDLY_*` — informational text
- `*_BTN` — action button labels (e.g., `LBL_SPENDLY_LOGIN_BTN`)

The dictionary is a key + languageID → display value lookup. Templates should render values resolved from this system, not inline text.

### Styles Must Be Customer-Configurable
CSS variable values (colors, fonts, sizing) must be overridable per customer. Avoid hardcoding design tokens inline; always reference CSS custom properties so customer themes can be applied by overriding `:root` values.
