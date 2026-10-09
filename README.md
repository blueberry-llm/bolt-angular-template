# Angular Starter Template

A starter template for [bolt.diy](https://github.com/stackblitz-labs/bolt.diy).

## Purpose

This template is designed for use with **<https://github.com/stackblitz-labs/bolt.diy>**. bolt.diy fetches
these files at runtime and imports them into a fresh WebContainer project when you ask for an Angular app,
so everything here needs to install and build with no extra setup.

Modified by [Dustin Loring](https://github.com/Dustinwloring1988) (Dustinwloring1988) in October 2026.

## Stack

| Package | Version |
| --- | --- |
| Angular | 22.2.2 |
| TypeScript | ~6.0.3 |
| zone.js | ^0.16.3 |
| rxjs | ^7.8.1 |

Node 20 or newer is required.

## Commands

```bash
npm install   # install dependencies
npm start     # ng serve — dev server on port 4200
npm run build # ng build — production build to dist/demo/browser
```

## About this template

The app is a single standalone component bootstrapped from `src/main.ts`, with no NgModule wrapper, so the
generated project stays small and easy to modify.

## Upgraded to Angular 22 (October 2026)

Moved from Angular 18.1. Each major was upgraded separately with Angular's own migration tool rather than
edited by hand, so the migrations ran one step at a time and were verified with a build after each step.
The branch history has one commit per major.

Notable changes made by the migrations:

- `src/main.ts` now passes `{ providers: [provideZoneChangeDetection()] }` to `bootstrapApplication`, replacing
  the deprecated bootstrap options object
- `src/main.ts` sets `changeDetection: ChangeDetectionStrategy.Eager` explicitly, which Angular 22 now applies
  to components during migration
- `tsconfig.json` switched `moduleResolution` from `node` to `bundler`, and the `lib` array was dropped
  (TypeScript derives it from `target: ES2022`)
- `tsconfig.json` no longer sets `downlevelIteration`. It is redundant at `target: ES2022` and TypeScript 6
  now reports it as an error that halts the build, so it was removed rather than silenced with
  `ignoreDeprecations`
- `tsconfig.app.json` suppresses the `nullishCoalescingNotNullable` and `optionalChainNotNullable` extended
  diagnostics, which Angular 22 adds by default during migration
- `angular.json` gained `schematics` defaults for generated file naming

TypeScript is on 6.x rather than 7: `@angular/compiler-cli@22` declares a peer range of `>=6.0 <6.1`.

A `.gitignore` was added. The template previously had none, so `node_modules` and `dist` were not excluded —
`ng update` also refuses to run on a dirty working tree, which blocked the upgrade.

## Verification

- `npm run build` passes, producing `index.html`, `main.js`, `polyfills.js` and `styles.css`
- Confirmed the component template (`Hello from {{ name }}!`) is present in the emitted `main.js`
- `ng build` runs the Angular AOT compiler, which type-checks the whole app