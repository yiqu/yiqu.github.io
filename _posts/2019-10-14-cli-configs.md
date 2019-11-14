---
layout: post
title: Angular CLI Configurations
readTime: 5
tags:
  - angular
  - cli
  - configurations
---

If you have not upgraded your Angular application to version 6+, you should really take the time and make the switch. There are some major changes
in the version 6 release. You can read it [here](https://github.com/angular/angular/blob/master/CHANGELOG.md#600-2018-05-03).
One major change is the Angular CLI. In version 6+, you will noticed that Angular has replaced the file <code>angular-cli.json</code> with
<code>angular.json</code>. In version 6+, each CLI workspace has projects, each project has targets, and each target can have configurations.

<br/>

#### Building Configurations

In the old CLI, you would build different versions of your application by supplying the <code>environment</code> flag, like: 
```bash
ng build --environment=development
``` 

In the new CLI, it is now like:
```bash
ng build --configuration=development
``` 

This is because in Angular 6, each target now has a **configuration** where you can configur how your application will be built. In the Production configuration, which comes with Angular with you create a new project by <code>ng new..</code>, you can see it has the following configurations:

```javascript
"configurations": {
            "production": {
              "fileReplacements": [
                {
                  "replace": "src/environments/environment.ts",
                  "with": "src/environments/environment.prod.ts"
                }
              ],
              "optimization": true,
              "outputHashing": "all",
              "sourceMap": false,
              "extractCss": true,
              "namedChunks": false,
              "aot": true,
              "extractLicenses": true,
              "vendorChunk": false,
              "buildOptimizer": true,
              "budgets": [
                {
                  "type": "initial",
                  "maximumWarning": "2mb",
                  "maximumError": "5mb"
                },
                {
                  "type": "anyComponentStyle",
                  "maximumWarning": "6kb",
                  "maximumError": "10kb"
                }
              ]
}
```

This config will be used if you built your application with the <code>--prod</code> flag. The flag is just a shorthand for 
<code>ng build --configuration=prod</code>. 

What if you have a custom configuration called **Staging**? You would have to add a new config in your <code>configuration</code>
property. Like:

```javascript
"configurations": {
            "production": {
            ...
             }
            "staging": {
              "someProperty": blah,
              "someProperty": blah
              "fileReplacements": [
                {
                  "replace": "src/environments/environment.ts",
                  "with": "src/environments/environment.staging.ts"
                }
              ],
            }
```

Now you can build your **Staging** with <code>ng build --configuration=staging</code>. 

Let's go one step further, what if you want to build Staging with all the options that Production have? For example, having
<code>aot</code>, and tree shaking? Well you could either add those options into your **Staging** configuration, or you could create
a new configuration called <code>Staging-Prod</code> like the following:

```javascript
"configurations": {
            "production": {
            ...
             }
            "staging": {
              ...
            }
            "staging-prod": {
              "optimization": true,
              "outputHashing": "all",
              "sourceMap": false,
              "extractCss": true,
              "namedChunks": false,
              "aot": true,
              "extractLicenses": true,
              "vendorChunk": false,
              "buildOptimizer": true,
              "budgets": [
                {
                  "type": "initial",
                  "maximumWarning": "2mb",
                  "maximumError": "5mb"
                },
                {
                  "type": "anyComponentStyle",
                  "maximumWarning": "6kb",
                  "maximumError": "10kb"
                }
              ]
              "fileReplacements": [
                {
                  "replace": "src/environments/environment.ts",
                  "with": "src/environments/environment.staging.ts"
                }
              ],
            }
```
Now you can build **Staging-Prod** by <code>ng build --configuration=staging-prod</code>. You will have all your Staging
environment properties with the Prodution options.

<br/>

#### Serve Configurations

When you run <code>ng serve</code>, CLI is running the default <code>build</code> configurations. If you want to <code>ng serve</code>
a custom configuration like the **Staging** configuration we have created earlier, you will have to add a section called <code>staging</code> like:

```javascript
"serve": {
          "builder": "@angular-devkit/build-angular:dev-server",
          "options": {
            "browserTarget": "myApp:build"
          },
          "configurations": {
            "production": {
              "browserTarget": "myApp:build:production"
            }
            "staging": {
              "browserTarget": "myApp:build:staging"
            }
          }
        },
```

Notice that in the staging property, I decalred the browserTarget to be <code>"myApp:build:staging"</code>, which means it will go try 
to find in the <code>build</code>, for a property named <code>staging</code>. Earlier, we have created just that. We added a new build called <code>staging</code>, and now Angular will run <code>serve</code> with those configurations.

Now when you run <code> ng serve --configuration=staging</code>, you will get all the staging environment feel with <code>serve</code>.

That's about all the basics of Angular configurations. Make sure to check out the detailed docs at [here](https://angular.io/cli/build).
        
