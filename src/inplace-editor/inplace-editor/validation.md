---
title: "Validation"
component: "In-place Editor"
description: "Learn how to add rules and to use validation, and then customize the error message in the Essential JS2 In-place Editor component."
---

# Validation

**In-place Editor** component supports validation and it can be achieved by adding rules to the [validationRules](../api/inplace-editor/#validationrules) property, its child property `key` must be same as [name](../api/inplace-editor/#name) property, otherwise validation not performed. Submitting data to the server or calling the [validate](../api/inplace-editor/#validate) method validation executed.

## Validation Rules

In-place Editor has following validation rules, which are used to perform validation.

| Rules | Description | Example |
|------|------|------|
| `required` | The input element must have any input values | a or 1 or - |
| `email` | The input element must have valid `email` format values | <inplace@syncfusion.com> |
| `url` | The  input element must have valid `url` format values| <http://syncfusion.com/> |
| `date` | The  input element must have valid `date` format values | 12/25/2019 |
| `dateIso` | The  input element must have valid `dateIso` format values | 2019-12-25 |
| `number` | The  input element must have valid `number` format values | 1.0 or 1 |
| `maxLength` | Input value must have less than or equal to `maxLength` character length | if `maxLength: 5`, [check] is valid and [checking] is invalid |
| `minLength` | Input value must have less than or equal to `minLength` character length | if `minLength: 5`, [testing] is valid and [test] is invalid |
| `rangeLength` | Input value must have value between `rangeLength` character length | if `rangeLength: [4,5]`, [test] is valid and [key] is invalid
| `range` | Input value must have value between `range` number | if `range: [4,5]`, [4] is valid and [6] is invalid |
| `max` | Input value must have less than or equal to `max` number | if `max: 3`, [3] is valid and [4] is invalid |
| `min` | Input value must have less than or equal to `min` number | if `min: 4`, [5] is valid and [2] is invalid |
| `regex` | Input value must have valid `regex` format | if `regex: '^[A-z]+$'`, [a] is valid and [1] is invalid |

## Step by Step validation configuration

The following steps are used to configure validation in In-place Editor.

Step 1: To perform default validation in In-place Editor the `name` property is mandatory. And the specified name must be the same as the key name.

Step 2:  The corresponding name specified in the name property should bind with the `validationRules` property. For example, in the below code snippet, the `Number`  in the name property is bind with the `maxLength`  of validationRules.  Likewise, you can bind with the in-build validation configurations in the above table.

{% tab template="in-place-editor/validation-sample", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from "@angular/core";

@Component({
  selector: "app-root",
  template: `
    <div id="container">
      <table class="table-section">
        <tr>
          <td class="col-lg-6 col-md-6 col-sm-6 col-xs-6">
            <ejs-inplaceeditor
              type="Numeric"
              name="Number"
              mode="Inline"
              [validationRules]="validationRules"
            ></ejs-inplaceeditor>
          </td>
        </tr>
      </table>
    </div>
  `
})
export class AppComponent {
  public name: string = "Number";

  public validationRules = {
    Number: { maxLength: 5 }
  };
}

```

{% endtab %}

In the following sample, first editor value submitted without select any date, so the default error message will be displayed below the `DatePicker` element. Second editor configured with the [validating](../api/inplace-editor/#validating) event with the handler. In handler event [errorMessage](../api/inplace-editor/validateEventArgs/#errormessage) argument value modified and it will show below the `DatePicker` element.

{% tab template="in-place-editor/validation", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';
import { ValidateEventArgs } from '@syncfusion/ej2-angular-inplace-editor';


@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
    <table class="table-section">
        <tr>
            <td class="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> Default Error Message </td>
            <td class="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                <ejs-inplaceeditor #textBox id="textBox" type="Date" name="Today" emptyText="dd/mm/yyyy" mode="Inline" [model]="model" [validationRules]="validation"></ejs-inplaceeditor>
            </td>
        </tr>
        <tr>
            <td class="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> Customized Error Message </td>
            <td class="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                <ejs-inplaceeditor #date id="date" type="Date" mode="Inline" emptyText="dd/mm/yyyy" [model]="model" name="TodayCustom" [validationRules]="rules" (validating)="validating($event)"></ejs-inplaceeditor>
            </td>
        </tr>
    </table>
</div>
    `
})

export class AppComponent {
    public model: object = { placeholder: 'Select date' };
    public validation: object = { Today: { required: true}};
    public rules: object = { TodayCustom: { required: true } };

    public validating(e: ValidateEventArgs): void {
        e.errorMessage = 'Field should not be empty';
    }
}
```

{% endtab %}

* For more details about validation configuration, refer this documentation [section](../api/inplace-editor/#validating).

* For custom validation except specifying validationRules, specify errorMessage at validating event, message will be shown when the value is `Empty`.