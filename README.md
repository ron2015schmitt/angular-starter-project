# Angular Starter Project With Tools 2024: Angular 17.0.8


[Angular 17](https://blog.angular.io/introducing-angular-v17-4d7033312e4b)


## Tools / packages included

|  Tool | Version |
| ------------- | ------------- | 
| [Angular](https://github.com/angular/angular) | 17.0 |
| [Angular CLI](https://github.com/angular/angular-cli) | 17.0 |
| [Angular integrated vite / esbuild](https://angular.io/guide/esbuild) for `ng build` and `ng serve` | -- | 
| nvm | (v0.39) |
| NodeJs | 20.10 |
| npm | 10.2 |
| pnpm | 8.13 |
| jest | 29.7 |
| JavaScript | [ECMA2022](https://dev.to/brayanarrieta/new-javascript-features-ecmascript-2022-with-examples-4nhg) |
| TypeScript | [5.2](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-5-2.html) |
| [Sass](https://sass-lang.com/) | -- |
| RxJs | 7.8.1 |


Material Design 3.0 support coming later in 2024...

[SSR](https://angular.io/guide/ssr) is now an option in Angular!  SSR is not included in this starter project, but refer to section [How this Repo was Created](#repo-create) on how to enable SSR. 



## Angular compatibility Guides

- [Official Angular Compatibility Guide](https://angular.io/guide/versions)
- [Unofficial Angular Compatibility Guide](https://gist.github.com/LayZeeDK/c822cc812f75bb07b7c55d07ba2719b3)




## Installation

The installation must be run from a linux terminal, or in Windows you can use a [git bash](https://gitforwindows.org/) terminal.


### Clone repo

```bash
git clone https://github.com/ron2015schmitt/angular-starter-project.git
cd angular-starter-project
```

### Install `nvm`

If you do not already have nvm installed,  execute the following to install [nvm](https://github.com/nvm-sh/nvm)

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

Notes:
1. After the command executes close out your terminal and open a new terminal to ensure everything was installed correctly
2. You can check the [nvm git repo](https://github.com/nvm-sh/nvm) to find the latest version number instead of 0.39.7.
3. To upgrade `nvm`, you use the same command as given above.

Check the verison of `nvm`

```bash
nvm -v
```


### Package manager setup.

The project utilizes the [pnpm](https://pnpm.io/) package manager.  However `npm` is needed to install `pnpm`.

```bash
cd angular-starter-project
nvm install 20.10
nvm use 20.10
npm i -g npm@10.2
npm i -g pnpm@8.13
```

**Notes**
1. With nvm, using the global option `-g` is preferred because it only applies to the specific NodeJs version.
2. Yes, we use `npm` not `pnpm` in the above to install `npm` and `pnpm`.
3. After this step, **always use** `pnpm`.
4. `pnpm` uses `pnpm-lock.yaml` instead of `package-lock.json`
5. If by mistake, you run `npm` to install the project or a project package, execute the following (**with care**) to fix:
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


### Run jest

```bash
ng test
```

You should see something like

![image](https://github.com/ron2015schmitt/angular-starter-project/assets/11559541/c6f57e1f-4a78-4e58-a6bc-789a5ae76e65)



<br>
<br>
<br>





## <a name="repo-create"></a> How this repo was created


### Set up package managers: nvm, npm, pnpm

```bash
nvm install 20.10
nvm use 20.10
npm i -g npm@10.2
npm i -g pnpm@8.13
```

**Note that with nvm, using `-g` is preferred because it only applies to the specific NodeJs version**


### Set up Angular 

The current version of the global Angular CLI determines the version of Angular to be used, installed via `npm` (not `pnpm`) because we are not in a project yet.

```bash
npm i -g @angular/cli@17.0
```

### Create Angular scaffolding 

The following creates `angular.json` and the `src` directory for the sample app.

```bash
ng new angular-starter-project --minimal --skip-tests --skip-git --package-manager=pnpm
cd angular-starter-project
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

### Set up integrated vite / esbuild 

Starting in Angular 17.0, Vite / esbuild are now the default for new projects!

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


