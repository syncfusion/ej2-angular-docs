---
title: "How To"
component: "DateRangePicker"
description: "Miscellaneous aspects of customizing the date range picker"
---

# Reactive form

DateRangePicker is a form component and validation is playing vital role in forms to get the valid data.
 Here to showcase the DateRangePicker with form validations we have used the reactive form.

The reactive forms uses the reactive model-driven technique to handle form data between component and view,
 due to that we also call it as the model-driven forms.
 It's listen the form data changes between App component and view, also returns the valid states and values of form elements.

For more details about Reactive Forms refer: [`https://angular.io/guide/reactive-forms`](https://angular.io/guide/reactive-forms).

For the reactive forms, import a `ReactiveFormsModule` into app module as well as the `FormGroup`,
`FormControl` should be imported to app component.
 The `FormGroup` is used to declare `formGroupName` for the form and the `FormControl` is used to declare `formControlName` for form controls. Declare the `formControlName` to DateRangePicker component as usual.
 Then, create a value object to the `FormGroup` and each value will be the default value of the form control.

The following example demonstrates how to use the reactive forms.

{% tab template="daterangepicker/reactive-validator", isDefaultActive = "true",  sourceFiles="app/**/*.ts,app/**/template.html,styles.css" %}

```typescript
import { Component, OnInit, Inject } from '@angular/core';
import { DateRangePickerComponent } from '@syncfusion/ej2-angular-calendars';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';
import { FormsModule } from '@angular/forms';


@Component({
    selector: 'app-root',
    templateUrl: './app/template.html'
})
export class AppComponent implements OnInit {
    skillForm: FormGroup;
    build: FormBuilder;
    constructor(@Inject(FormBuilder) private builder: FormBuilder) {
        this.build = builder;
        this.createForm();
    }
    createForm() {
        this.skillForm = this.build.group({
            daterangepicker: ['', Validators.required],
            username: ['', Validators.required],
            usermail: ['', Validators.email],
        });
    }
    get username() {
        return this.skillForm.get('username');
    }
    get daterangepicker() {
        return this.skillForm.get('daterangepicker');
    }
    get usermail() {
        return this.skillForm.get('usermail');
    }

    onSubmit() {
        alert("Form Submitted!");
    }
}

```

{% endtab %}