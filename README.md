
<span style="background-color: #FFFF00">Marked text</span>

# Angular Starter Project With Tools 2024 (Angular 17.0)

Tools / packages

- [Angular](https://github.com/angular/angular) 17.0
- [Angular CLI](https://github.com/angular/angular-cli) 17.0
- [Angular integrated vite / esbuild](https://angular.io/guide/esbuild) for `ng build` and `ng serve`
- nvm
- nodejs 20.10
- npm 10.2
- pnpm 8.13
- jest 29.7
- [Javascript ECMA2022](https://dev.to/brayanarrieta/new-javascript-features-ecmascript-2022-with-examples-4nhg)
- [TypeScript 5.2](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-5-2.html)

Material Design 3.0 coming later in 2024...

## install

### Package manager setup.

```bash
nvm install 20.10
nvm use 20.10
npm i -g npm@10.2
npm i -g pnpm@8.13
```
 
### Clone repo

```bash
git clone https://github.com/ron2015schmitt/angular-starter-project.git
cd angular-starter-project
```

### Install packages

```bash
pnpm install
```

### Run

```bash
ng serve
```
point browser to http://localhost:4200/

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/5cfdf453-d959-402e-8f41-4cd7b1aa6e96)

## How this repo was created

### Compatibility Guides

- [Official Angular Compatibility Guide](https://angular.io/guide/versions)
- [Unofficial Angular Compatibility Guide](https://gist.github.com/LayZeeDK/c822cc812f75bb07b7c55d07ba2719b3)

### Set up package managers: nvm, npm, pnpm

```bash
nvm install 20.10
nvm use 20.10
npm i -g npm@10.2
npm i -g pnpm@8.13
```

### Set up Angular 

The current version of the global Angular CLI determines the version of Angular to be used.  

```bash
npm install -g @angular/cli@17.0
```

### Create Angular scaffolding 

The following creates `angular.json` and the `src` directory for the sample app.

```bash
ng new angular-starter-project --minimal --skip-tests --skip-git --package-manager=pnpm
```

Answer questions when prompted:

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/d1b5eabc-c2ee-47d2-a39f-d5a23918af7f)


### Add TypeScript

Starting in Angular 17.0, TypeScript is now included by default!

### Set up integrated vite / esbuild 

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/c91fe9f2-6a4c-4749-86bd-484a964c1d68)


>In ng serve we’re now using Vite for the development server, and esbuild powers both your development and production builds!
>
>We want to emphasize that Angular CLI relies on Vite exclusively as a development server. To support selector matching, the Angular compiler needs to maintain a dependency graph between your components which requires a different compilation model than Vite.

https://blog.angular.io/angular-v16-is-here-4d7a28ec680d


#### Set up vite during `ng build`

In your project `angular.json`, add `-esbuild` to the following line

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/98e502f5-3677-423d-bc01-05d0c3f46141)



#### Set up vite during `ng serve`

Then (also in `angular.json`) add the text
```json
          "options": {
            "forceEsbuild": true
          },
```

in the following location

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/f399a464-7c45-4129-a51a-a23d8241a72b)


### Add `engines` and `bin` sections to the `package.json`

Add the tool versions to `package.json`

```json
  "bin": {
    "myng": "./node_modules/@angular/cli/bin/ng"
  },
  "engines": {
    "node": "20.10",
    "npm": "10.2",
    "pnpm": "8.13"
  },
```

Check the versions

```bash
ng version
```

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/b9473add-10b3-4f66-b00e-310bdb3b6b1e)



### Set up Jest 

Install jest

```bash
pnpm add jest --save-dev
pnpm add @types/jest --save-dev
pnpm --recursive update
```

Add the text `, "zone.js/testing"` to your `angular.json` in the `"architect"` section

```json
      "architect": {
        "build": {
          "builder": "@angular-devkit/build-angular:browser-esbuild",
          "options": {
            "outputPath": "dist/sample-angular-project",
            "index": "src/index.html",
            "browser": "src/main.ts",
            "polyfills": [
              "zone.js",
              "zone.js/testing"  <-- add this
            ],
```

Add `"jest"` to the `compilerOptions.types` array in your `tsconfig.app.json`
```json
  "compilerOptions": {
    "outDir": "./out-tsc/spec",
    "types": [
      "jest"  <-- Add this 
    ]
  },
```


