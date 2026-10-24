# Copilot instructions

## Project shape and architecture

- The project is a standalone Spanish-language web app in `index.html`. Markup, styles, quiz data, and interaction logic live together in that file; the page runs directly in a browser with no server, package manager, or runtime dependencies.
- The inline script owns the question list and the attempt state (`current`, `score`, `answered`). `renderQuestion()` updates the active question and progress, `chooseAnswer()` locks the answers and shows feedback, and `showResult()` / `restart()` handle the end and restart states. Keep these UI and state transitions in sync when changing quiz behavior.
- Questions are static objects with four answer strings, a zero-based `correct` index, and an explanation. Keep the question count, progress maximum, and result calculations derived from the question list rather than maintaining separate totals.

## Commands

- There are no configured build, test, or lint commands: the repository has no package manifest or test runner.
- Run the app by opening `index.html` directly in a browser. No development server is required.
- For interaction changes, exercise an answer, next-question flow, final results, and restart in a browser; also check both color schemes and keyboard focus behavior.

## Code conventions

- Keep the app dependency-free and self-contained in `index.html` unless the project requirements explicitly change.
- User-facing copy is in Spanish, and the document language is `es`.
- Theme colors are CSS custom properties declared in `:root`; update the corresponding values in `@media (prefers-color-scheme: light)` when adding or changing themed colors. Use the existing success, error, accent, and mission-control tokens instead of adding unrelated one-off colors.
- Preserve accessible controls and feedback: answers and actions are native buttons, feedback and question updates use live regions, and progress exposes its value through `role="progressbar"` and ARIA value attributes. Keep visible keyboard focus and move focus when the question or result screen changes.
- Respect `prefers-reduced-motion` for animation and transition changes; the page already provides a reduced-motion override.
- The question bank is the source of truth for the quiz length. When changing its structure or answer count, update rendering and validation assumptions together.
