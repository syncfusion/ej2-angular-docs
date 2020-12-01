# Getting Started for Ionic with Angular

This document helps you to create a simple Angular application with `Ionic Framework` and `Syncfusion Angular UI components`.

## Prerequisites

Before getting started with Syncfusion Angular Components in Ionic with Angular project, check whether the following have been installed in the developer's machine.

* Angular Versions supported - 4+
* Typescript Versions supported - 2.6+
* ionic CLI 3.9.0+

>Note: If the `ionic CLI` is not installed, refer to the [`Getting Started with ionic`](https://ionicframework.com/getting-started/#cli) document to install it.

## Create an application

Create a new project with the following command using the command prompt.

```bash
npm install -g ionic
```

>Note: Here, we are using ionic version 4.6.0 to support Angular 6.

Run the following command line to create a new Ionic template application. The new application will be placed under ej2-ionic folder after the command completes its process, and it will install the default npm dependent packages when creating the application.

```bash
ionic start ej2-ionic blank --type=angular 
```

>Note: Refer to this [getting started](https://ionicframework.com/getting-started/#cli) document to install ionic framework.

## Installing Syncfusion button package

Syncfusion packages are distributed in npm as `@syncfusion` scoped packages. You can get all the Angular syncfusion package from [npm]( https://www.npmjs.com/search?q=%40syncfusion%2Fej2-angular- ).

Add the `@syncfusion/ej2-angular-buttons` package to the application.

```bash
npm install @syncfusion/ej2-angular-buttons --save
(or)
npm i @syncfusion/ej2-angular-buttons --save
```

## Adding button module

After installing the package, the component modules are available to configure your application from Syncfusion installed package. Syncfusion Angular package provides two different types of ng-Modules.

Refer to [`Ng Module`](https://ej2.syncfusion.com/angular/documentation/common/ng-module.html) to learn about `ngModules`.

Refer to the following code snippet to import the button module in `app/src/home/home.module.ts` from the `@syncfusion/ej2-angular-buttons`.

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { IonicModule } from '@ionic/angular';
import { FormsModule } from '@angular/forms';
import { HomePage } from './home.page';
import { ButtonModule } from '@syncfusion/ej2-angular-buttons';
import { HomePageRoutingModule } from './home-routing.module';


@NgModule({
  imports: [
    CommonModule,
    FormsModule,
    IonicModule,
    HomePageRoutingModule,
    ButtonModule 
  ],
  declarations: [HomePage]
})
export class HomePageModule {}


```

## Adding Syncfusion component

Add the button component snippet in `src/home/home.page.ts` as follows.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-home',
  template: `<button ejs-button cssClass="”e-primary”">Button</button>`,
  styleUrls: ['home.page.scss'],
})
export class HomePage {

  constructor() {}

}

```

## Adding CSS reference

Add button component styles as given in the `angular-cli.json` file within the app > styles section.

>Note: If you are using Angular 6 project, add the changes in `angular.json` file.

```typescript

{
"apps": [
    {
         "styles": [
              {
                "input": "./node_modules/@syncfusion/ej2-angular-buttons/styles/material.css"
              },
              {
                "input": "src/global.scss"
              }
            ]
     }
   ]
}

```

## Running the application

Finally, run the following command line to start the application. The Syncfusion Essential JS 2 button component will be rendered in the ionic framework. 

 ```bash
ionic serve 
```

>Note: For your convenience, we have prepared an [Angular sample with ionic framework](https://github.com/SyncfusionExamples/ej2-angular-ionic).

