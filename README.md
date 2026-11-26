# playwrightDemo

A minimal [Playwright](https://playwright.dev/) end-to-end testing demo written in TypeScript. It runs the same smoke tests against Chromium, Firefox and WebKit using the official Playwright Test runner.

## What it tests

`tests/example.spec.ts` targets <https://playwright.dev/>:

| Test | Checks |
|------|--------|
| `has title` | The home page title contains "Playwright" |
| `get started link` | Clicking **Get started** lands on a page with an "Installation" heading |

Each test runs on 3 browser projects (chromium, firefox, webkit), so a full run executes 6 tests.

## Prerequisites

- Node.js 18 or newer
- npm

## Setup

```bash
git clone git@github.com:fsspark/playwrightDemo.git
cd playwrightDemo
npm install
npx playwright install --with-deps
```

## Running the tests

| Command | Description |
|---------|-------------|
| `npm test` | Run all tests on all browsers (headless) |
| `npm run test:chromium` | Run on Chromium only |
| `npm run test:ui` | Open Playwright UI mode |
| `npm run test:debug` | Debug on Chromium with the inspector |
| `npm run report` | Open the last HTML report |
| `npm run typecheck` | Type-check the TypeScript sources |

Run a single file or test by title:

```bash
npx playwright test tests/example.spec.ts
npx playwright test -g "has title"
```

## Project structure

```
playwrightDemo/
├── tests/
│   └── example.spec.ts      # Test specs
├── playwright.config.ts     # Runner configuration (projects, retries, reporter)
├── tsconfig.json            # TypeScript settings (type-checking only)
├── package.json
└── package-lock.json
```

## Configuration highlights

- `fullyParallel: true`: tests run in parallel locally
- On CI (`CI` env var set): 2 retries, 1 worker, and `test.only` fails the build
- Trace is collected on the first retry (view with `npx playwright show-trace <trace.zip>`)
- Reporter: HTML (output in `playwright-report/`)

## Useful tips

- `test.skip(...)` skips a test; `test.only(...)` runs only that test (the CI guard prevents committing it by accident).
- Generate selectors and tests interactively with `npx playwright codegen https://playwright.dev/`.

## License

ISC
