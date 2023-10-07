# Sample Angular Project With Tools 2023

Tools / packages

- [Angular CLI](https://github.com/angular/angular-cli) 16.2.5
- [Angular integrated vite / esbuild](https://angular.io/guide/esbuild) for `ng build` and `ng serve`
- nvm
- nodejs 18.18
- npm 10.2
- pnpm 8.8
- jest 29.7
- TypeScript 5.1

## install

### Package manager setup.

```bash
nvm install 18.18
nvm use 18.18
npm i -g npm@10.2
npm i -g pnpm@8.8
```
 
### Clone repo

```bash
git clone https://github.com/ron2015schmitt/sample-angular-project.git
cd sample-angular-project
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

![image](https://github.com/ron2015schmitt/sample-angular-project/assets/11559541/5cfdf453-d959-402e-8f41-4cd7b1aa6e96)

## How this repo was created

### Compatibility Guides

- [Official Angular Compatibility Guide](https://angular.io/guide/versions)
- [Unofficial Angular Compatibility Guide](https://gist.github.com/LayZeeDK/c822cc812f75bb07b7c55d07ba2719b3)

### Set up package managers: nvm, npm, pnpm

```bash
nvm install 18.18
nvm use 18.18
npm i -g npm@10.2
npm i -g pnpm@8.8
```

### Set up Angular 

The current version of the global Angular CLI determines the version of Angular to be used.  

```bash
npm install -g @angular/cli@16.2.5
```

### Create Angular scaffolding 

The following creates `angular.json` and the `src` directory for the sample app.

```bash
ng new sample-angular-project --minimal --skip-tests --skip-git --package-manager=pnpm
cd sample-angular-project
```

### Add TypeScript

```bash
pnpm add typescript@5.1 -w
```

### Set up integrated vite / esbuild in Angular 16

![image](https://github.com/ron2015schmitt/sample-angular-project/assets/11559541/c91fe9f2-6a4c-4749-86bd-484a964c1d68)


>In ng serve we’re now using Vite for the development server, and esbuild powers both your development and production builds!
>
>We want to emphasize that Angular CLI relies on Vite exclusively as a development server. To support selector matching, the Angular compiler needs to maintain a dependency graph between your components which requires a different compilation model than Vite.

https://blog.angular.io/angular-v16-is-here-4d7a28ec680d


#### Set up vite during `ng build`

In your project `angular.json`, add `-esbuild` to the following line

![image](https://github.com/ron2015schmitt/sample-angular-project/assets/11559541/98e502f5-3677-423d-bc01-05d0c3f46141)



#### Set up vite during `ng serve`

Then (also in `angular.json`) add the text
```json
          "options": {
            "forceEsbuild": true
          },
```

in the following location

![image](https://github.com/ron2015schmitt/sample-angular-project/assets/11559541/f399a464-7c45-4129-a51a-a23d8241a72b)


## Set up Jest 

Install jest

```bash
pnpm add jest --save-dev
pnpm add @types/jest --save-dev
```

Add the following to your `angular.json` in the `"architect"` section
```json
        "test": {
          "builder": "@angular-devkit/build-angular:jest",
          "options": {
            "tsConfig": "tsconfig.spec.json",
            "polyfills": ["zone.js", "zone.js/testing"]
          }
        }
```

Add `"jest"` to the `compilerOptions.types` array in your `tsconfig.spec.json`
```json
  "compilerOptions": {
    "outDir": "./out-tsc/spec",
    "types": [
      "jest"  // <-- Add this 
    ]
  },
```


