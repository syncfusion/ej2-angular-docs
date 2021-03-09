---
title: "In-place Editor Getting Started"
component: "In-place Editor"
description: "This section briefly explains how to create an Essential JS2 In-place Editor component with its basic features."
---

# Getting started

This section explains the steps to create a simple **In-place Editor** component and configure its available functionalities in Angular.

## Getting Started with Angular CLI

The following section explains the steps required to create a simple `angular-cli` application and how to configure `In-place Editor` component.

### Prerequisites

To get started with Syncfusion Angular UI Components, make sure that you have compatible versions of Angular and TypeScript.

* Angular : 4+
* TypeScript : 2.6+

### Setting up an Angular project

Angular provides an easiest way to setup project using Angular CLI [Angular CLI](https://github.com/angular/angular-cli) tool.

Install the CLI application globally in your machine.

```javascript

  npm install -g @angular/cli

```

### Create a new application

```javascript

  ng new syncfusion-angular-app

```

Once you have executed the above command you may ask for following options,
* Would you like to add Angular routing?
* Which stylesheet format would you like to use?

By default it install the CSS style base application. To setup with SCSS, pass --style=SCSS argument on create project.

Example code snippet.

```javascript

  ng new syncfusion-angular-app --style=SCSS

```

Navigate to the created project folder.

```javascript

  cd syncfusion-angular-app

```

## Install Syncfusion In-place Editor package

Syncfusion packages are distributed in npm as `@syncfusion` scoped packages. You can get all the Angular Syncfusion package from npm [link](https://www.npmjs.com/search?q=%40syncfusion%2Fej2-angular-).

Add Syncfusion Angular In-place Editor package in your application by using following Command,

```javascript

npm install @syncfusion/ej2-angular-inplace-editor --save
(or)
npm i @syncfusion/ej2-angular-inplace-editor --save

```

## Adding In-place Editor module

Once you have successfully installed the package, the component modules are ready to configure in your application from the installed location. Syncfusion Angular package provides two different types of ngModules.

Refer to [Ng-Module](https://ej2.syncfusion.com/angular/documentation/common/ng-module/) to learn about `ngModules`.

Refer the following snippet to import the `InPlaceEditorAllModule` in `app.module.ts` from the `@syncfusion/ej2-angular-inplace-editor`.

```javascript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
// Imported syncfusion InPlaceEditorAllModule from ej2-angular-inplace-editor package
import { InPlaceEditorAllModule } from '@syncfusion/ej2-angular-inplace-editor';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    // Registering EJ2 In-place Editor Module
    InPlaceEditorAllModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

## Adding In-place Editor component

Add the In-place Editor component snippet in `app.component.ts` as follows.

```typescript

import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<ejs-inplaceeditor id="element" type="Text" value="Andrew" [model]="modelObj"></ejs-inplaceeditor>`
})

export class AppComponent {
  public modelObj: Object = { placeholder: 'Enter employee name' };
}

```

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder. This can be referenced in [src/styles.css] using following code.

```css

      @import '../node_modules/@syncfusion/ej2-base/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-dropdowns/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-lists/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-richtexteditor/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-calendars/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-angular-inplace-editor/styles/material.css';

```

> The [Custom Resource Generator (CRG)](https://crg.syncfusion.com/) is an online web tool, which can be used to generate the custom script and styles for a set of specific components.
> This web tool is useful to combine the required component scripts and styles in a single file.

## Running the application

Run the `ng serve` command in command window, it will serve your application and you can open the browser window. Output will appear as follows.

{% tab template="in-place-editor/getting-started-form", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div id='container'>
    <div class="control-group">
        <div class="e-heading">
        <h3> Modify Basic Details </h3>
        </div>
        <table>
            <tr>
                <td>Name</td>
                <td class='left'>
                    <ejs-inplaceeditor id="element" mode="Inline" value="Andrew" [model]="elementModel"></ejs-inplaceeditor>
                </td>
            </tr>
            <tr>
                <td>Date of Birth</td>
                <td class='left'>
                    <ejs-inplaceeditor id="dateofbirth" type="Date" mode="Inline" [value]="dateValue" [model]="dateModel"></ejs-inplaceeditor>
                </td>
            </tr>
            <tr>
                <td>Gender</td>
                <td class='left'>
                    <ejs-inplaceeditor id="gender" type="DropDownList" mode="Inline" value="Male" [model]="genderModel"></ejs-inplaceeditor>
                </td>
            </tr>
        </table>
        </div>
        </div>`
})

export class AppComponent {
  public genderData: string[] = ['Male', 'Female'];
  public dateModel: Object = { showTodayButton: true, placeholder: 'Select date of birth' };
  public dateValue: Date = new Date('04/12/2018');
  public elementModel: Object = { placeholder: 'Enter your name' };
  public genderModel: Object = {  dataSource: this.genderData, placeholder: 'Select gender' };
}

```

{% endtab %}

## Add the In-place Editor with Textbox

By default, the Essential JS2 TextBox component is rendered in **In-place Editor** with [`type`](../api/inplace-editor/inputType/) property sets as Text.

Modify the template in `src/app/app.component.ts` file to render the `ej2-angular-inplace-editor` component.

```javascript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-inplaceeditor id="element" type="Text" value="Andrew" [model]="modelObj"></ejs-inplaceeditor>`
})

export class AppComponent {
    public modelObj: Object = { placeholder: 'Enter employee name' };
}
```

## Configuring DropDownList

You can render the Essential JS2 DropDownList by changing the [`type`](../api/inplace-editor/inputType/) property as [`DropDownList`](../api/drop-down-list) and configure its properties and methods using the `model` property.

In the following sample, [`type`](../api/inplace-editor/inputType/) and model values are configured to render the [`DropDownList`](../api/drop-down-list) component.

```javascript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-inplaceeditor id="element" type="DropDownList" mode="Inline" [model]="modelObj"></ejs-inplaceeditor>`
})

export class AppComponent {
    public genderData : string[] = ['Male', 'Female'];
    public modelObj: Object = { placeholder: 'Select gender', dataSource: this.genderData };
}
```

## Integrate DatePicker

You can render the Essential JS2 [DatePicker](../api/datepicker/) by changing the [`type`](../api/inplace-editor/inputType/) property as [`Date`](../api/inplace-editor/inputType/) and also configure its properties and methods using the [`model`](../api/inplace-editor#model) property.

```javascript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-inplaceeditor id="element" type="Date" [value]="value" [model]="modelObj"></ejs-inplaceeditor>`
})

export class AppComponent {
    public modelObj: Object = { showTodayButton: true };
    public value: Date = new Date('04/12/2018');
}
```

Once you have configured Textbox, DatePicker and DropDownList you will get following output as shown in below,

{% tab template="in-place-editor/getting-started-form", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div id='container'>
    <div class="control-group">
            <div class="e-heading">
            <h3> Modify Basic Details </h3>
            </div>
            <table>
                <tr>
                    <td>Name</td>
                    <td class='left'>
                        <ejs-inplaceeditor id="element" mode="Inline" value="Andrew" [model]="elementModel"></ejs-inplaceeditor>
                    </td>
                </tr>
                <tr>
                    <td>Date of Birth</td>
                    <td class='left'>
                        <ejs-inplaceeditor id="dateofbirth" type="Date" mode="Inline" [value]="dateValue" [model]="dateModel"></ejs-inplaceeditor>
                    </td>
                </tr>
                <tr>
                    <td>Gender</td>
                    <td class='left'>
                        <ejs-inplaceeditor id="gender" type="DropDownList" mode="Inline" value="Male" [model]="genderModel"></ejs-inplaceeditor>
                    </td>
                </tr>
            </table>
        </div>
        </div>
               `
})

export class AppComponent {
  public genderData: string[] = ['Male', 'Female'];
  public dateModel: Object = { showTodayButton: true, placeholder: 'Select date of birth' };
  public dateValue: Date = new Date('04/12/2018');
  public elementModel: Object = { placeholder: 'Enter your name' };
  public genderModel: Object = {  dataSource: this.genderData, placeholder: 'Select gender' };
}

```

{% endtab %}

## Two-way binding

In In-place Editor, the `value` property supports two-way binding functionality. The following example demonstrates how to achieve two-way binding, by using property binding to bind the value to the first In-place Editor component and `ngModel` to bind the model data to the second In-place Editor. The value of the In-place Editor will get changed, when there is any change in the property value or model value.

{% tab template="in-place-editor/two-way", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div id='container'>
    <div class="control-group">
    <table>
        <tr>
            <td><b>TextBox :</b></td>
            <td><ejs-inplaceeditor id="texteditor1" type="Text" mode="Inline" [(value)]="value" [model]="modelObj"></ejs-inplaceeditor></td>
            <td><ejs-inplaceeditor id="texteditor2" type="Text" mode="Inline" [(ngModel)]="value" [model]="modelObj"></ejs-inplaceeditor></td>
        </tr>
        <tr>
            <td><b>Datepicker :</b></td>
            <td><ejs-inplaceeditor id="dateeditor1" type="Date" mode="Inline" [(value)]="dateValue" [model]="dateModel"></ejs-inplaceeditor></td>
            <td><ejs-inplaceeditor id="dateeditor2" type="Date" mode="Inline" [(ngModel)]="dateValue" [model]="dateModel"></ejs-inplaceeditor></td>
        </tr>
        <tr>
            <td><b>DropDownList :</b></td>
            <td><ejs-inplaceeditor id="dropDowneditor1" type="DropDownList" mode="Inline" [(value)]="dropdownValue" [model]="dropDownmodelObj"></ejs-inplaceeditor></td>
            <td><ejs-inplaceeditor id="dropDowneditor2" type="DropDownList" mode="Inline" [(ngModel)]="dropdownValue" [model]="dropDownmodelObj"></ejs-inplaceeditor></td>
        </tr>
    </table>
</div>
</div>`
})

export class AppComponent {
  public value: string = 'Andrew';
  public modelObj: Object = { placeholder: 'Enter employee name' };
  public dateModel: Object = { showTodayButton: true, placeholder: 'Select date of birth' };
  public dateValue: Date = new Date('04/12/2018');
  public dropdownValue: string = 'Android';
  public frameWorkList : string[] = ['Android', 'JavaScript', 'jQuery', 'TypeScript', 'Angular', 'React', 'Vue','Ionic'];
  public dropDownmodelObj: Object = { placeholder: 'Select frameWorks', dataSource: this.frameWorkList };
}

```

{% endtab %}

## Submitting data to the server (save)

You can submit editor value to the server by configuring the [`url`](../api/inplace-editor#url), [`adaptor`](../api/inplace-editor/adaptorType/) and [`primaryKey`](../api/inplace-editor#primarykey) property.

| Property   | Usage                                           |
|------------|---------------------------------------------------------|
| **`url`**        | Gets the URL for server submit action.        |
| **`adaptor`**    | Specifies the adaptor type that is used by DataManager to communicate with DataSource.  |
| **`primaryKey`** | Defines the unique primary key of editable field which can be used for saving data in the data-base. |

> The [`primaryKey`](../api/inplace-editor#primarykey) property is mandatory. If it's not set, edited data are not sent to the server.

## Refresh with modified value

The edited data is submitted to the server and you can see the new values getting reflected in the **In-place Editor**.

{% tab template="in-place-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
        <div className='control-group' style="text-align: center; margin: 100px auto;">
            Best Employee of the year: <ejs-inplaceeditor id="element" type="DropDownList" mode="Inline" value="Andrew Fuller" name='Employee' [url]="url" primaryKey="Employee" adaptor="UrlAdaptor" [model]="model" (actionSuccess)='actionSuccess($event)'></ejs-inplaceeditor>
          </div>
         <table style='margin:auto;width:50%'>
        <tr>
            <td style="text-align: left">
               Old Value :
            </td>
            <td id="oldValue" style="text-align: left">
            </td>
        </tr>
        <tr>
            <td style="text-align: left">
               New Value :
            </td>
            <td id="newValue" style="text-align: left">
                Andrew Fuller
            </td>
        </tr>
       </table>
     </div>
    `
})

export class AppComponent {
  public frameWorkList: string[] = ['Andrew Fuller', 'Janet Leverling', 'Laura Callahan', 'TypeScript', 'Margaret Hamilt', 'Michael Suyama', 'Nancy Davloio', 'Robert King'];
  public model: Object = {  dataSource: this.frameWorkList, placeholder: 'Select employee',  popupHeight: '200px' };
  public url: String = "https://ej2services.syncfusion.com/development/web-services/api/Editor/UpdateData";
  public actionSuccess(e: any): void {
      let newEle: HTMLElement = document.getElementById('newValue');
      let oldEle: HTMLElement = document.getElementById('oldValue');
      oldEle.textContent = newEle.textContent;
      newEle.textContent = e.value;
    }
}

```

{% endtab %}

## See Also

* [Types of rendering the editor](./integration/)