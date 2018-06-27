# Lerna + Project References

This is a "bare minimum" repo that shows one way to configure TypeScript Project References with lerna. There are a lot of different ways you can set things up and this isn't intended to be authoratitive guidance or exclusionary of other ways that might work better in your project.

### General Structure

As with a normal lerna repo, there's a `packages` folder. Inside we have three creatively named packages `pkg1`, `pkg2`, and `pkg3`.

```
packages/
| tsconfig.settings.json
| tsconfig.json
| pkg1/
  | tsconfig.json
  | src/
  | | (typescript files)        
  | lib/
  | | (javascript files)
  | | (.d.ts files)
| pkg2/
  | (same as pkg1)
| pkg3/
  | (same as pkg1)
```

Let's review each file in the repo and explain what's going on

#### `tsconfig.settings.json`
```
{
    "compilerOptions": {
        // Always include these settings
        "composite": true,
        "declaration": true,
        "declarationMap": true,
        "sourceMap": true,

        // These settings are totally up to you        
        "esModuleInterop": true,
        "target": "es5",
        "module": "commonjs",
        "strict": true
    }
}
```
This file contains the "default" settings that all packages will use for compilation. You will definitely want the `composite`, `declaration`, `declarationMap`, and `sourceMap` settings enabled for all projects, so include those in this file. Other settings, like `target` and `strict`, can be specified here if you'd like to enable them by default. You'll also be able to override these settings on a per-package basis if needed.

#### `tsconfig.json`
```
{
    "files": [],
    "references": [
        { "path": "pkg1" },
        { "path": "pkg2" },
        { "path": "pkg3" }
    ]
}
```
This file is pretty simple - simply list the packages that need to be built with `tsc` in the `references` array.
You should also 