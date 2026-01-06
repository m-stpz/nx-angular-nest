# NX, Nest, and Angular

## Initialize

Official video: https://www.youtube.com/watch?v=hWvRzo51YAc&t

```bash
# initial setup
npx create-nx-workspace@latest app --preset=ts --workspaces=false --packageManager=pnpm
cd app

# nestjs
pnpm nx add @nx/nest # add plugin
pnpm nx g @nx/nest:app apps/<nest-app-name> # generate nest app
pnpm nx serve <nest-app-name> # run nest app

# angular
pnpm nx add @nx/angular
pnpm nx g @nx/angular:app apps/<ng-app-name>
pnpm nx serve <ng-app-name>
```

### Debugging

- For some reason, the angular 22 build wasn't working correctly with the vite build.
  - I needed to run the following commands to have angular working on the setup
    - Downgrade angular from v22/21 to 20
    - Remove @angular/build

```bash
rm -rf node_modules pnpm-lock.yaml

pnpm add -D \
  @angular-devkit/core@~20.2.0 \
  @angular-devkit/schematics@~20.2.0 \
  @angular-devkit/build-angular@~20.2.0 \
  @angular/cli@~20.2.0 \
  @angular/compiler-cli@~20.2.0 \
  @angular/language-service@~20.2.0 \
  @schematics/angular@~20.2.0

pnpm add \
  @angular/core@~20.2.0 \
  @angular/common@~20.2.0 \
  @angular/compiler@~20.2.0 \
  @angular/forms@~20.2.0 \
  @angular/platform-browser@~20.2.0 \
  @angular/router@~20.2.0

pnpm install
pnpm nx serve client
# it now threw a new error with

#➜  app git:(main) ✗ pnpm nx serve client --verbose
# > nx run client:serve:development

 # NX   require() of ES Module /Users/matt_fonto/Local.nosync/code_studies/nx_nest_angular_setup/app/node_modules/.pnpm/vite@7.2.2_@types+node@20.19.9_jiti@2.6.1_less@4.5.1_sass-embedded@1.97.2_sass@1.93.2_terser@5.43.1_yaml@2.8.2/node_modules/vite/dist/node/index.js from /Users/matt_fonto/Local.nosync/code_studies/nx_nest_angular_setup/app/node_modules/.pnpm/@angular+build@21.0.4_@angular+compiler-cli@20.2.4_@angular+compiler@20.2.4_typescript@_b027dac20ff2169030cfed04c6674eac/node_modules/@angular/build/src/builders/dev-server/vite/index.js not supported.

# then, I needed to
pnpm remove @angular/build vite

pnpm add -D \
  @angular-devkit/build-angular@~20.2.0 \
  @angular-devkit/core@~20.2.0 \
  @angular-devkit/schematics@~20.2.0 \
  @angular/cli@~20.2.0 \
  @schematics/angular@~20.2.0

rm -rf node_modules pnpm-lock.yaml
pnpm install
pnpm nx serve client
# then it worked
```
