# Copilot instructions

## Project structure and behavior

The app is a standalone browser quiz in `index.html`: semantic markup, CSS, quiz data, and vanilla JavaScript all live in that file. There is no build step, server, package manager, or runtime dependency; opening the file directly in a browser is the normal way to run it.

The `questions` array is the source of truth for question text, category, answers, correct-answer index, and feedback fact. `renderQuestion()` builds the answer buttons from that data; `chooseAnswer()` owns scoring and feedback; `advance()` moves through the quiz; `showResults()` renders the final screen; and `restart()` reconstructs the quiz markup. Keep question counts, progress values, results, and replay behavior consistent with the array rather than hard-coding a different count.

## Code conventions

- Keep the app dependency-free and self-contained in `index.html`; use native DOM APIs and browser features rather than introducing a framework or build tooling.
- Keep presentation in the embedded stylesheet and behavior in the embedded script. Reuse the CSS custom properties in `:root` and `@media (prefers-color-scheme: dark)` for theme-sensitive colors, including any new states or components.
- The question screen has live DOM updates: when changing its markup, update both the initial HTML and the template in `restart()`. `rebindNodes()` refreshes references to replaced elements and reconnects the next-question handler; keep it in sync with those templates.
- Answers and primary actions are native buttons. Preserve their keyboard focus behavior, visible focus styles, and live announcements when changing interaction or feedback behavior.
- Respect `prefers-reduced-motion` for animations and transitions; keep the light/dark palettes legible and correct/incorrect states distinguishable in both.

## Build, test, and lint

There are no configured build, automated test, or lint commands, and no single-test command. To run the app, open `index.html` directly in a browser. For a browser smoke check, answer questions with both correct and incorrect choices, check score and progress, finish the quiz, and use Play again to verify the reset path.
