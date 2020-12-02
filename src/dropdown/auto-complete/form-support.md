---
title: "Autocomplete Form Support"
component: "AutoComplete"
description: "This section for Syncfusion angular autocomplete component demonstrates HTML forms support, template-driven forms (angular) support, and reactive forms support."
---

# Form Support

The AutoComplete supports both the reactive and template-driven form-building technologies.

## Template-Driven Forms

The template-drive forms uses the `ng` directives in view to handle the forms controls.
To enable the template-driven,  import the FormsModule into corresponding app component.

For more details about template-driven Forms refer to:<https://angular.io/guide/forms#template-driven-forms>.

 Mention the `name` attribute to Autocomplete element which will be used to identify the
  form element. To register an Autocomplete element to ngForm,  give the ngModel  to it
  so the FormsModule will  automatically detect the AutoComplete as a form element.
  After that, the AutoComplete value will be selected based on the ngModel value.

The following example  demonstrates how to achieve a two-way data binding.

{% tab template="autocomplete/form-support", sourceFiles="app/**/*.ts,form-support.html" %}

```typescript

import { Component, OnInit } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { BrowserModule } from '@angular/platform-browser';
@Component({
    selector: 'app-root',
    templateUrl: './form-support.html'
})
export class AppComponent {
    // defined the array of data
    public skillset: string[] = [
                                      'ASP.NET', 'ActionScript', 'Basic',
                                      'C++' , 'C#' , 'dBase' , 'Delphi' ,
                                      'ESPOL' , 'F#' , 'FoxPro' , 'Java',
                                      'J#' , 'Lisp' , 'Logo' , 'PHP'
                                  ];
    public placeholder: String = 'e.g: ActionScript';

    constructor() {
    }
        skillForm = {
            skillname: null,
            sname: '',
            smail: ''
        };
}

```

{% endtab %}

## Reactive Forms

The reactive forms uses the reactive model-driven technique to handle
 form data between component and view, due to that we also call it as
 the `model-driven` forms. It's listen the form data changes between
 App component and view also returns the valid states and values of form elements.

For more details about Reactive Forms refer: <https://angular.io/guide/reactive-forms>.

For the reactive forms you should import a ReactiveFormsModule
 into app module as well as the FormGroup,FormControl should be
 imported to app component. The FormGroup is used to declare
 `formGroupName` for the form and the FormControl is used to
 declare `formControlName` for form controls.
 You can declare the formControlName to AutoComplete as usual.
 then,you must create a value object to the FormGroup and
 each value will be the default value of the form control.

The following example demonstrates  how to use the reactive forms.

{% tab template="autocomplete/reactive-form", sourceFiles="app/**/*.ts,reactive-form.html" %}

```typescript

import { Component, OnInit, Inject } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { BrowserModule } from '@angular/platform-browser';
@Component({
    selector: 'app-root',
    templateUrl: './reactive-form.html'
})
export class AppComponent {
    // defined the array of data
    public skillset: string[] = [
                                      'ASP.NET', 'ActionScript', 'Basic',
                                      'C++' , 'C#' , 'dBase' , 'Delphi' ,
                                      'ESPOL' , 'F#' , 'FoxPro' , 'Java',
                                      'J#' , 'Lisp' , 'Logo' , 'PHP'
                                  ];
    public placeholder: String = 'e.g: ActionScript';
    skillForm: FormGroup;
    fb: FormBuilder;

    constructor(@Inject(FormBuilder) private builder: FormBuilder) {
        this.fb = builder;
        this.createForm();
    }
    createForm() {
        this.skillForm = this.fb.group({
            skillname: ['', Validators.required],
            sname: ['', Validators.required],
            smail: ['', Validators.required]
        });
    }
}


```

{% endtab %}