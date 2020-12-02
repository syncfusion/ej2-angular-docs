---
title: "Getting Started"
component: "MaskedTextBox"
description: "This getting started section briefly explains how to create a masked text box component in Angular application. It also explains about how to integrate the masked text box control in reactive form and two way binding functionality."
---

# Getting Started

The following section explains the steps required to create
the MaskedTextBox component and also it demonstrates the basic usage of the MaskedTextBox.

## Dependencies

The following list of dependencies are required to use the MaskedTextBox component in your application.

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
ng new syncfusion-angular-maskedtextbox
```

By default, it install the CSS style base application. To setup with SCSS, pass --style=scss argument on create project.

Example code snippet.

```bash
ng new syncfusion-angular-maskedtextbox --style=scss
```

Navigate to the created project folder.

```bash
cd syncfusion-angular-maskedtextbox
```

## Adding MaskedTextBox package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install MaskedTextBox component, use the following command.

```bash
npm install @syncfusion/ej2-angular-inputs --save
(or)
npm i @syncfusion/ej2-angular-inputs --save
```

> The **--save** will instruct NPM to include the MaskedTextBox package inside of the [dependencies](./getting-started#dependencies) section of the `package.json`.

## Registering MaskedTextBox module

Import MaskedTextBox module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-inputs`.

```javascript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// imports the MaskedTextBoxModule for the MaskedTextBox component
import { MaskedTextBoxModule } from '@syncfusion/ej2-angular-inputs';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-inputs module into NgModule
  imports:      [ BrowserModule,  MaskedTextBoxModule ],
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

## Adding MaskedTextBox component

Modify the template in [src/app/app.component.ts] file to render the MaskedTextBox component.
Add the Angular MaskedTextBox by using `<ejs-maskedtextbox>` selector in `template` section of the app.component.ts file..

```javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `<ejs-maskedtextbox></ejs-maskedtextbox>`
})
export class AppComponent  { }
```

>Note: If you want to refer the combined component styles, please make use of our [`CRG`](https://ej2crg.azurewebsites.net/) (Custom Resource Generator) in your application.

## Set the mask

You can set the mask to the MaskedTextBox to validate the user input by using the [`mask`](../api/maskedtextbox#mask) property.
For more information about the usage of mask and configuration, refer to this [link](./mask-configuration/).

The following example demonstrates the usage of mask element `0` that allows any single digit from `0` to `9`.

```typescript
import { Component} from '@angular/core';

@Component({
    selector: 'app-root',
    // sets mask format to the MaskedTextBox
    template: `
            <ejs-maskedtextbox mask='000-000-0000'></ejs-maskedtextbox>
            `
})
export class AppComponent {
    constructor() {
    }
}
```

## Running the application

After completing the configuration required to render a basic MaskedTextBox, run the following command to display the output in your default browser.

```cmd
ng serve
```

The following example illustrates the output in your browser.

{% tab template="maskedtextbox/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // sets mask format to the MaskedTextBox
    template: `<label class='label'>Enter the mobile number</label>`+
              `<ejs-maskedtextbox mask='000-000-0000'></ejs-maskedtextbox>`
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}

## Two way binding

In MaskedTextBox, the `value` property supports two-way binding functionality.
The following example demonstrates two-way binding functionality with the MaskedTextBox and HTML input element.

{% tab template="maskedtextbox/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // input element for checking the two-way binding support using value property
    template: `
     <div class='e-input-group' style='margin-bottom:30px'>
        <input class='e-input' type='text' [(ngModel)]='value' placeholder='Mobile Number' />
     </div>
     <ejs-maskedtextbox mask='000-000-0000' [(value)]='value'></ejs-maskedtextbox>
    `
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## Reactive form

MaskedTextBox is a form component and validation is playing vital role in forms to get the valid data.
Here to showcase the MaskedTextBox with form validations we have used the reactive form.
For more details about Reactive Forms refer: [`https://angular.io/guide/reactive-forms`](https://angular.io/guide/reactive-forms).

* To use reactive forms, import `ReactiveFormsModule` from the `@angular/forms` package and add it to your NgModule's imports array.
  In addition to this, `FormGroup`, `FormControl` should be imported to the app component.
* The `FormGroup` is used to declare `formGroupName` for the form. The constructor of this `FormGroup` then takes an object,
  that can contain sub-form-groups and `FormControls`.
* The `FormControl` is used to declare `formControlName` for form controls.

The following example demonstrates how to use the reactive forms.

{% tab template="maskedtextbox/reactive-forms", sourceFiles="template.html,app/**/*.ts"  %}

```typescript
import { Component, Inject } from '@angular/core';
import {MaskedTextBoxComponent  } from '@syncfusion/ej2-angular-inputs';
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
          mask: ['', Validators.required],
          username: ['', Validators.required],
        });
    }
    get username() { return this.skillForm.get('username'); }
    get mask() { return this.skillForm.get('mask'); }

    onSubmit() {
      alert("You have entered the value: " + this.mask.value );
  }
}

```

{% endtab %}

## See Also

* [How to perform custom validation using FormValidator](./how-to/perform-custom-validation-using-form-validator/)
* [How to customize the UI appearance of the control](./how-to/customize-the-ui-appearance-of-the-control/)
* [How to set cursor position while focus on the input textbox](./how-to/set-cursor-position-while-focus-on-the-input-textbox/)
* [How to display numeric keypad when focus on mobile devices](./how-to/display-numeric-keypad-when-focus-on-mobile-devices/)