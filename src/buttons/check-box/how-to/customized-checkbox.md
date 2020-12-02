---
title: "Customized CheckBox"
component: "CheckBox"
description: "Angular CheckBox how to section, name and value in form submit, and customization of CheckBox appearance, frame & check icon."
---

# Customized CheckBox

## Customize CheckBox Appearance

You can customize the appearance of the CheckBox module using the CSS rules.
Define own CSS rules according to your requirement and assign the class name to the [`cssClass`](../../api/check-box#cssclass) property.

The background and border color of the CheckBox is customized through the custom classes to create primary, success, warning, danger, and
info type of checkbox.

{% tab template= "check-box/howto", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // To customize CheckBox appearance
    template: `<ul>
               <!-- Refer the 'e-primary' class details in 'style.css'. -->
               <li><ejs-checkbox label="Primary" cssClass="e-primary" [checked]="true"></ejs-checkbox></li>

               <!-- Refer the 'e-success' class details in 'style.css'. -->
               <li><ejs-checkbox label="Success" cssClass="e-success" [checked]="true"></ejs-checkbox></li>

               <!-- Refer the 'e-info' class details in 'style.css'. -->
               <li><ejs-checkbox label="Info" cssClass="e-info" [checked]="true"></ejs-checkbox></li>

               <!-- Refer the 'e-warning' class details in 'style.css'. -->
               <li><ejs-checkbox label="Warning" cssClass="e-warning" [checked]="true"></ejs-checkbox></li>

               <!-- Refer the 'e-danger' class details in 'style.css'. -->
               <li><ejs-checkbox label="Danger" cssClass="e-danger" [checked]="true"></ejs-checkbox></li>

               </ul>`
})

export class AppComponent { }

```

{% endtab %}

## Customize CheckBox frame

CheckBox frame can be customized as per the requirement by adding CSS rules.

In the following example, to-do list is displayed with round checkbox by changing `border-radius` as `100%` by adding `e-custom` class.

{% tab template= "check-box/custom-frame", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // To customize CheckBox appearance
    template: `<ul>
                    <li><ejs-checkbox label="Buy Groceries" cssClass="e-custom" [checked]="true"></ejs-checkbox></li>

                    <li><ejs-checkbox label="Pay Rent" cssClass="e-custom"></ejs-checkbox></li>

                    <li><ejs-checkbox label="Make Dinner" cssClass="e-custom"></ejs-checkbox></li>

                    <li><ejs-checkbox label="Finish To-do List Article" cssClass="e-custom"></ejs-checkbox></li>
                </ul>`
})

export class AppComponent { }

```

{% endtab %}

## Customize check icon

CheckBox check icon can be customized as per the requirement by adding CSS rules.

In the following example, the check icon can be customized by changing check icon content, background and
border color in focus and hovered states by adding `e-checkicon` class.

{% tab template= "check-box/custom-icon", sourceFiles="app/**/*.ts, styles.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // To customize CheckBox appearance
    template: `<ul>
                    <li><ejs-checkbox label="Buy Groceries" cssClass="e-checkicon" [checked]="true"></ejs-checkbox></li>

                    <li><ejs-checkbox label="Pay Rent" cssClass="e-checkicon"></ejs-checkbox></li>

                    <li><ejs-checkbox label="Make Dinner" cssClass="e-checkicon"></ejs-checkbox></li>

                    <li><ejs-checkbox label="Finish To-do List Article" cssClass="e-checkicon"></ejs-checkbox></li>
                </ul>`
})

export class AppComponent { }

```

{% endtab %}

## Customized Checkbox output

CheckBox output can be customized as per the requirement of the user.

In the following example, the checkbox output can be customized by providing the given value as the output instead of boolean value in  the default checkbox.

{% tab template= "check-box/custom-output", sourceFiles="app/**/*.ts, styles.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    templateUrl: 'app.component.html',
    styleUrls: ['app.component.css'],
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  form: FormGroup;
  testData = [
    { value: '1', name: 'test1' },
    { value: '2', name: 'test2' },
    { value: '3', name: 'test3' },
    { value: '4', name: 'test4' }
  ];

  constructor(private formBuilder: FormBuilder) {
    this.form = this.formBuilder.group({
      tests: new FormArray([])
    });
    this.addCheckboxes();
  }

  private addCheckboxes() {
    this.testData.forEach((o, i) => {
      const control = new FormControl(i === 0); // if first item set to true, else false
      (this.form.controls.tests as FormArray).push(control);
    });
  }

  submit() {
    // Filtering the selected value based on the selected checkbox
    const selectedValues: string[] = this.form.value.tests
      .map((v, i) => v ? this.testData[i].value : null)
      .filter(v => v !== null);
    console.log(selectedValues);
  }
}

```

{% endtab %}
