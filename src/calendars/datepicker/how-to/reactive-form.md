---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Reactive Form

DatePicker is a form component and validation is playing vital role in forms to get the valid data.
Here to showcase the DatePicker with form validations we have used the reactive form.

* The reactive forms uses the reactive model-driven technique to handle form data between component and view,
 due to that we also call it as the model-driven forms.
 It's listen the form data changes between App component and view, also it returns the valid states and values of form elements.

For more details about Reactive Forms refer: [`https://angular.io/guide/reactive-forms`](https://angular.io/guide/reactive-forms).

* For the reactive forms, import a `ReactiveFormsModule` into app module as well as the `FormGroup`,
`FormControl` should be imported to app component.
 The `FormGroup` is used to declare `formGroupName` for the form and the `FormControl` is used to declare `formControlName` for form controls. Declare the `formControlName` to DatePicker component as usual.
 Then, create a value object to the `FormGroup` and each value will be the default value of the form control.

The following example demonstrates how to use the reactive forms.

{% tab template="datepicker/reactive-validator", isDefaultActive = "true",  sourceFiles="app/**/*.ts,app/**/template.html,styles.css" %}

```typescript
import { Component, ViewChild, OnInit, ElementRef, Inject } from '@angular/core';
import { DatePickerComponent } from '@syncfusion/ej2-angular-calendars';
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { ButtonComponent } from '@syncfusion/ej2-ng-buttons';
import { FormsModule } from '@angular/forms';


@Component({
    selector: 'app-root',
    templateUrl: './app/template.html'
})
export class AppComponent implements OnInit {
    @ViewChild('ejDatePicker') ejDatePicker: DatePickerComponent;
    public targetElement: HTMLElement;
    public placeholder: String = 'Date of Birth';
    skillForm: FormGroup;
    build: FormBuilder;
    constructor(@Inject(FormBuilder) private builder: FormBuilder) {
        this.build = builder;
        this.createForm();
    }
    createForm() {
        this.skillForm = this.build.group({
            datepicker: ['', Validators.required],
            username: ['', Validators.required],
            usermail: ['', Validators.email],
        });
    }
    get username() {
        return this.skillForm.get('username');
    }
    get datepicker() {
        return this.skillForm.get('datepicker');
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