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

In the old CLI, you would build different version of your application by supplying the <code>environment</code> flag, like: 
```bash
ng build --environment=development
``` 

In the new CLI, it is now like:
```bash
ng build --configuration=development
``` 

This is because in Angular 6, each target now has a **configuration** where you can configur how your application will be built. In the Production configuration, which comes with Angular with you create a new project by <code>ng new..</code>, you can see it has the following configurations:

```json
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

```json
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

```json
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
