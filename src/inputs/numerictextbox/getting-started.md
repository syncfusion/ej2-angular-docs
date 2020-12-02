---
title: "Getting Started"
component: "NumericTextBox"
description: "This getting started section briefly explains how to create a numeric text box component in Angular application. It also explains about range validation, precision of numbers, formatting the value in numeric text box and how to integrate the numeric text box in reactive form."
---

# Getting Started

The following section explains the steps required to create
the NumericTextBox component and also it demonstrates the basic usage of the NumericTextBox.

## Dependencies

The following list of dependencies are required to use the NumericTextBox component in your application.

```javascript
|-- @syncfusion/ej2-angular-inputs
    |-- @syncfusion/ej2-angular-base
    |-- @syncfusion/ej2-angular-popups
    |-- @syncfusion/ej2-angular-buttons
    |-- @syncfusion/ej2-angular-splitbuttons
    |-- @syncfusion/ej2-inputs
        |-- @syncfusion/ej2-base
        |-- @syncfusion/ej2-popups
        |-- @syncfusion/ej2-buttons
        |-- @syncfusion/ej2-splitbuttons
```

## Setup angular environment

Angular provides the easiest way to set angular CLI projects using [`Angular CLI`](https://github.com/angular/angular-cli) tool.

Install the CLI application globally to your machine.

```bash
npm install -g @angular/cli
```

## Create a new application

```bash
ng new syncfusion-angular-numerictextbox
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-numerictextbox --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-numerictextbox
```

## Adding NumericTextBox package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install NumericTextBox component, use the following command.

```bash
npm install @syncfusion/ej2-angular-inputs --save
(or)
npm i @syncfusion/ej2-angular-inputs --save
```

> The **--save** will instruct NPM to include the NumericTextBox package inside of the [dependencies](./getting-started#dependencies) section of the `package.json`.

## Registering NumericTextBox module

Import NumericTextBox module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-inputs`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// imports the NumericTextBoxModule for the NumericTextBox component
import { NumericTextBoxModule } from '@syncfusion/ej2-angular-inputs';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-inputs module into NgModule
  imports:      [ BrowserModule , NumericTextBoxModule],
  declarations: [ AppComponent],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder.
This can be referenced in [src/styles.css] using following code.

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
@import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
@import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
@import '../node_modules/@syncfusion/ej2-angular-inputs/styles/material.css';
```

## Adding NumericTextBox component

Modify the template in [src/app/app.component.ts] file to render the NumericTextBox component.
Add the Angular NumericTextBox by using `<ejs-numerictextbox>` selector in `template` section of the app.component.ts file..

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  // specifies the template string for the NumericTextBox component
  template: `<ejs-numerictextbox value='10'></ejs-numerictextbox>`
})
export class AppComponent  { }
```

>Note: If you want to refer the combined component styles, please make use of our [`CRG`](https://ej2crg.azurewebsites.net/) (Custom Resource Generator) in your application.

## Running the application

After completing the configuration required to render a basic NumericTextBox, run the following command to display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser.

{% tab template="numerictextbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the NumericTextBox component
    template: `<ejs-numerictextbox value='10'></ejs-numerictextbox>`,
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}

## Range validation

You can set the minimum and maximum range of values in the NumericTextBox using the [`min`](../api/numerictextbox#min) and
[`max`](../api/numerictextbox#max) properties, so the numeric value should be in the min and max range.

The validation behavior depends on the [`strictMode`](../api/numerictextbox#strictmode) property.

The below example demonstrates range validation.

{% tab template="numerictextbox/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the NumericTextBox component
    // sets the minimum and maximum range values
    // strictMode has been enabled by defualt
    template: `
            <ejs-numerictextbox min='10' max='20' value='16' step='2'></ejs-numerictextbox>
            `
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}

## Formatting the value

User can set the format of the NumericTextBox component using [`format`](../api/numerictextbox#format)
property. The value will be displayed in the specified format, when the component is in focused out state. For more information about
formatting the value, refer to this [link](./formats/).

The below example demonstrates format the value by using currency format value `c2`.

{% tab template="numerictextbox/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the NumericTextBox component
    // sets currency with 2 numbers of decimal places format
    template: `
            <ejs-numerictextbox format='c2' value='10'></ejs-numerictextbox>
            `
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}

## Precision of numbers

You can restrict the number of decimals to be entered in the NumericTextBox by using the [`decimals`](../api/numerictextbox#decimals)
and [`validateDecimalOnType`](../api/numerictextbox#validatedecimalontype) properties.
So, you can't enter the number whose precision is greater than the mentioned decimals.

* If `validateDecimalOnType` is false, number of decimals will not be restricted.
Else, number of decimals will be restricted while typing in the NumericTextBox.

{% tab template="numerictextbox/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the NumericTextBox component
    // restricts number of decimals to be entered in the NumericTextBox by using validateDecimalOnType property
    // sets number of decimal places to be allowed by the NumericTextBox
    template: `
             <div class='wrap'>
               <ejs-numerictextbox [validateDecimalOnType]='true' decimals='3' format='n3' value='10' placeholder='ValidateDecimalOnType Enabled' floatLabelType= 'Auto'></ejs-numerictextbox>
            </div>
            <div class='wrap'>
               <ejs-numerictextbox decimals='3' format='n3' value='10' placeholder='ValidateDecimalOnType Disabled' floatLabelType= 'Auto'></ejs-numerictextbox>
            </div>
            `
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}

## Two way binding

In NumericTextBox, the `value` property supports two-way binding functionality.
The below example demonstrates two-way binding functionality with the NumericTextBox and HTML input element.

{% tab template="numerictextbox/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the NumericTextBox component and
    // input element for checking the two-way binding support using value property
    template: `
     <div class='e-input-group' style='margin-bottom:30px'>
        <input class='e-input' type='text' [(ngModel)]='value' placeholder='Enter a number'  />
     </div>
    <ejs-numerictextbox [(value)]='value'></ejs-numerictextbox>
    `
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## Reactive form

NumericTextBox is a form component and validation is playing vital role in forms to get the valid data.
Here to showcase the NumericTextBox with form validations we have used the reactive form.
For more details about Reactive Forms refer: [`https://angular.io/guide/reactive-forms`](https://angular.io/guide/reactive-forms).

* To use reactive forms, import `ReactiveFormsModule` from the `@angular/forms` package and add it to your NgModule's imports array.
  In addition to this, `FormGroup`, `FormControl` should be imported to the app component.
* The `FormGroup` is used to declare `formGroupName` for the form. The constructor of this `FormGroup` then takes an object,
  that can contain sub-form-groups and `FormControls`.
* The `FormControl` is used to declare `formControlName` for form controls.

The following example demonstrates how to use the reactive forms.

{% tab template="numerictextbox/reactive-forms", sourceFiles="template.html,app/**/*.ts,index.css"  %}

```typescript
import { Component, Inject } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
    selector: 'app-root',
    templateUrl: './app/template.html',
})
export class AppComponent {
    skillForm: FormGroup;
    build: FormBuilder;
    constructor(@Inject(FormBuilder) private builder: FormBuilder) {
        this.build = builder;
        this.createForm();
    }
    createForm() {
        this.skillForm = this.build.group({
          numeric: ['', Validators.required],
          username: ['', Validators.required],
        });
    }
    get username() { return this.skillForm.get('username'); }
    get numeric() { return this.skillForm.get('numeric'); }

    onSubmit() {
       alert("You have entered the value: " + this.numeric.value );
  }
}

```

{% endtab %}

## See Also

* [How to perform custom validation using FormValidator](./how-to/perform-custom-validation-using-form-validator/)
* [How to customize the UI appearance of the control](./how-to/customize-the-ui-appearance-of-the-control/)
* [How to customize the spin button’s up and down arrow](./how-to/customize-the-spin-buttons-up-and-down-arrow/)
* [How to customize the step value and hide spin buttons](./how-to/customize-the-step-value-and-hide-spin-buttons/)
* [How to prevent nullable input in NumericTextBox](./how-to/prevent-nullable-input-in-numerictextbox/)
* [How to maintain trailing zeros in NumericTextBox](./how-to/maintain-trailing-zeros-in-numerictextbox/)