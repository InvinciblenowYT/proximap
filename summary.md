# Migration Summary

## What Was Done

- Upgraded the project from Angular 12 to Angular 22.
- Updated the dependency set in `package.json` and regenerated `package-lock.json`.
- Switched the workspace to work under Node 25 using `nvm`.
- Added an `eslint.config.js` for ESLint 9 flat config.
- Added a `karma.conf.js` and `.browserslistrc`.
- Updated `tsconfig.json` for modern TypeScript / Angular 22 settings.
- Restored the Datablue-generated JSON assets with `npm run sync_datablue`.
- Fixed several app-level compatibility issues surfaced by the migration:
  - class field initialization order
  - obsolete RxJS import paths
  - legacy Angular Material form-field values
  - obsolete `entryComponents`
  - `Subject<void>` calls needing `next(undefined)`
- Patched two legacy third-party packages in `node_modules` so the Angular 22 build could complete:
  - `@kolkov/ngx-gallery`
  - `@ngx-progressbar/core`

## Verified

- `npm run build` passes under Node `v25.2.1`.
- `npm run lint` passes, with only pre-existing warnings.
- The repo is committed in:
  - `bb601df` `Upgrade Angular stack for Node 25`
  - `dc630ce` `Finish Angular 22 Node 25 migration`

## What Still Needs Attention

- Replace or upgrade `@kolkov/ngx-gallery` with a package that officially supports Angular 22.
- Replace or upgrade `@ngx-progressbar/core` with a package that officially supports Angular 22.
- Decide whether to remove or keep the CommonJS dependencies that still trigger Angular build warnings:
  - `haversine`
  - `lodash`
  - `mapbox-gl`
  - `ts-md5`
- Review Angular 22 deprecation warnings and decide whether to migrate from the deprecated Webpack builder to the newer Angular build system.
- Consider removing the remaining `src/app` lint warnings if you want a cleaner baseline.

## Recommended Next Steps

1. Replace the incompatible gallery/progressbar dependencies.
2. Migrate the build pipeline to the current Angular build system.
3. Clean up the remaining build warnings and app-level lint warnings.
