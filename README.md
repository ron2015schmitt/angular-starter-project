# Angular Starter Project With Tools 2024: Angular 17.0.8

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
- [Sass](https://sass-lang.com/)
- RxJs: 7.8.1

[SSR](https://angular.io/guide/ssr) is now an option in Angular!

Material Design 3.0 coming later in 2024...

## install


### Clone repo

```bash
git clone https://github.com/ron2015schmitt/angular-starter-project.git
cd angular-starter-project
```

### Package manager setup.

```bash
nvm install 20.10
nvm use 20.10
npm i -g npm@10.2
npm i -g pnpm@8.13
```

**Notes**
1. With nvm, using `-g` is preferred because it only applies to the specific NodeJs version
2. Yes, we use `npm` not `pnpm` in the above to install `npm` and `pnpm`
3. After this step, **always use** `pnpm`
4. `pnpm` uses `pnpm-lock.yaml` instead of `package-lock.json`
5. If by mistake, you run npm to install the project or a project package, execute the following (**with care**) to fix:
```bash
rm package-lock.json
rm -fr node_modules/
```


 

### Install packages

```bash
pnpm install
```

Your `node_modules` will now be populated with the project packages.

### Serve the website

```bash
ng serve
```
point browser to http://localhost:4200/

|  http://localhost:4200/ | 
| ------------- | 
| ![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/b24bdf76-20ca-4a17-8c62-135911f0c1ee)  |


<br>
<br>
<br>



### Run jest

```bash
ng test
```

You should see something like

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/c6f57e1f-4a78-4e58-a6bc-789a5ae76e65)



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

**Note that with nvm, using `-g` is preferred because it only applies to the specific NodeJs version**


### Set up Angular 

The current version of the global Angular CLI determines the version of Angular to be used.  

```bash
npm install @angular/cli@17.0
```

### Create Angular scaffolding 

The following creates `angular.json` and the `src` directory for the sample app.

```bash
ng new angular-starter-project --minimal --skip-tests --skip-git --package-manager=pnpm
```

Answer questions when prompted:

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/d1b5eabc-c2ee-47d2-a39f-d5a23918af7f)


Note that if you would like [SSR](https://angular.io/guide/ssr), then answer yes above.


### Edit `.gitignore`

Add the following to `.gitignore`

```gitignore
.angular/cache/
```


### Add TypeScript

Starting in Angular 17.0, TypeScript is now included by default!


### Change project version in `package.json`

In your project `package.json`, change project version to match Angular version 

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/fca9a8a2-b978-401e-b3e3-e82a71dec17f)

### Add  `bin`  and `engines` sections to the `package.json`

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

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/10faf300-c155-4882-95e9-033b7cc6f866)



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


### Fix schema validation bug in 

Angular 17.0 introduced the following bug:

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/b9c7eb1c-4650-46f3-9eb0-c4a14ee567e6)


To fix this change `"browser"` to `"main"` in `angular.json`

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/a808cdec-6eed-4785-bb87-3c85adf4caf2)



### Set up Jest 

Install jest

```bash
pnpm add jest --save-dev
pnpm add @types/jest --save-dev
pnpm add jest-environment-jsdom --save-dev
pnpm --recursive update
```

Add the following `"test"` section inside the "architect" section of `angular.json`
```json
        "test": {
          "builder": "@angular-devkit/build-angular:jest",
          "options": {
            "tsConfig": "tsconfig.app.json",
            "polyfills": [
              "zone.js",
              "zone.js/testing"
            ]
          }
        }
```

as follows

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/5a2d0514-5e15-44bd-96fe-6d44f6bcdf7d)



Add `"jest"` to the `compilerOptions.types` array in your `tsconfig.app.json`
```json
  "compilerOptions": {
    "outDir": "./out-tsc/spec",
    "types": [
      "jest"  <-- Add this 
    ]
  },
```


