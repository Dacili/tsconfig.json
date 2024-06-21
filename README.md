# tsconfig.json
Usually, when working with **FE frameworks**, you use the **CLI** provided by the framework to generate the initial state of the app. There are some files, that we, in most cases *ignore, until we need them*.  
One example of that is the **Angular** framework, which uses **angular-cli** for creating app.  
My focus, for now, is the file **tsconfig.json.** TS stands for typescript.

## What is tsconfig.json file?
The presence of a tsconfig.json file in a directory indicates that the directory is the *root of a TypeScript project*.  
The file specifies the root files and the *compiler options required to compile the project*.

## Example of tsconfig.json file
```
{
  "compileOnSave": false,
  "compilerOptions": {
    "baseUrl": "./",
    "outDir": "./dist/out-tsc",
    "sourceMap": true,
    "declaration": false,
    "downlevelIteration": true,
    "experimentalDecorators": true,
    "moduleResolution": "node",
    "importHelpers": true,
    "target": "es2020",
    "module": "es2020",
    "lib": [
      "es2018",
      "dom"
    ],
    "paths": {
      "@models/*": ["src/app/_models/*"],
      "@services/*": ["src/app/_services/*"],
      "@core/*": ["src/app/core/*"],
      "@environments/*": ["src/environments/*"],
      "@shared/*": ["src/app/shared/*"],
      "@state/*": ["src/app/_store/*"]
    },
    "noImplicitAny": false
  },
  "angularCompilerOptions": {
    "enableI18nLegacyMessageIdFormat": false,
    "strictTemplates": true,
  }
}

```

## In my app I have 3 types of tsconfig.json, what's the purpose for all of them?
![image](https://github.com/Dacili/tsconfig.json/assets/37112852/b4492e1c-24a9-4ada-b77c-6318d9a63242)  
Yes, in the Angular app there are several tsconfig.json files:  
**1. tsconfig.json** - general file that contains general typescript configuration.  
**2. tsconfig.app.json**  - is a file that is related to the Angular App in particular (angular-cli also).    
Notice, that this file usually includes tsconfig.json file in itself,  
```
 "extends": "./tsconfig.json",
```
 **but if some configuration is repeated in tsconfig.app.json, it will override the values from tsconfig.json!!!**  
 Example of tsconfig.app.json:  
```
/* To learn more about this file see: https://angular.io/config/tsconfig. */
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "outDir": "./out-tsc/app",
    "types": []
  },
  "files": [
    "src/main.ts",
    "src/polyfills.ts"
  ],
  "include": [
    "src/**/*.d.ts"
  ]
}

```
**3. tsconfig.spec.json**  - this one is used for the purposes of tests in Angular apps. The tests have .spec extensions.

## Purpose of paths property
The purpose of paths property, is to avoid relative paths in imports. This way you could always use defined values from paths, instead of relative paths (which can be very long, for example multiple ../../../). Paths are relative to baseUrl property.  
 
 ```
"paths": {
      "@models/*": ["src/app/_models/*"],
      "@services/*": ["src/app/_services/*"],
      "@core/*": ["src/app/core/*"],
      "@environments/*": ["src/environments/*"],
      "@shared/*": ["src/app/shared/*"],
      "@state/*": ["src/app/_store/*"]
    }
```
Instead of this:  
![image](https://github.com/Dacili/tsconfig.json/assets/37112852/9fee6539-1703-46a0-bd49-3e2e3a3712fe)  
You would have this:
![image](https://github.com/Dacili/tsconfig.json/assets/37112852/eba9187a-4f57-4343-bcbb-95c0800a8ff6)  
Note: Currently the Visual studio is always suggesting relative path, it seems like bug. But in Visual Studio Code it suggests paths.  
#### Why is beneficial to have paths?
Code readability, less length in import lines, maintainability - *if the structure of the app is changed, you don't have to modify moved files, everything stays the same* (except maybe paths to be updated in tsconfig json if needed)



