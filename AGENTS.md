# Repository Guidelines

## Project Structure & Module Organization

ReNoKu is a dependency-free, single-page Sudoku PWA. `index.html` contains the markup, CSS, and all game logic, including puzzle generation, profiles, timers, notes, and victory handling. `sw.js` provides offline caching, while `manifest.json` defines installable-app metadata. Static assets live at the repository root (`renoku.png`) and in `fonts/` (`comfortaa*.woff2`). Keep paths relative so the app continues to work when hosted below a domain root.

## Build, Test, and Development Commands

There is no compilation or package-install step. Serve the repository over HTTP because service workers do not run reliably from `file://` URLs:

```sh
python3 -m http.server 8000
```

Open `http://localhost:8000`. Use `git diff --check` before committing to catch whitespace errors, and `git status --short` to verify that only intended files changed.

## Coding Style & Naming Conventions

Follow the existing vanilla HTML, CSS, and JavaScript style. Use four-space indentation inside blocks in `index.html`, double quotes for HTML attributes and JavaScript strings, semicolons, and braces on the same line as declarations. Use `camelCase` for JavaScript variables and functions (`startGame`, `removeNumbers`), `UPPER_SNAKE_CASE` for constants (`PROFILE_KEY`), and kebab-case for CSS classes and element IDs (`pause-overlay`, `profile-btn`). Prefer small functions and avoid introducing dependencies for simple browser-native behavior. Preserve the current Portuguese UI language unless a change explicitly includes localization.

## Testing Guidelines

No automated test framework or coverage target is configured. Manually test easy, medium, and hard games; number entry and error highlighting; notes mode; pause/resume; victory and profile updates; and responsive layout. In browser developer tools, confirm that `manifest.json`, fonts, and icons load without errors. Test offline behavior after one online load. When changing cached assets, update `CACHE_NAME` in `sw.js` so existing installations receive the new files.

## Commit & Pull Request Guidelines

Recent commits use short, descriptive subjects such as `updating sw` and `Making renoku PWA`. Keep commits focused and write concise imperative subjects, for example `Fix note highlighting`. Pull requests should explain the user-visible change, list manual test cases, and link any related issue. Include screenshots for layout or styling changes, ideally at desktop and mobile widths. Call out manifest or cache changes explicitly because they affect installed PWA clients.
