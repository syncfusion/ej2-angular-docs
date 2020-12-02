---
title: "Rich Text Editor Validation"
component: "Rich Text Editor"
description: "This section shows how to validate the Syncfusion's Angular Rich Text Editor component's value by applying validationRules and validationMessage."
---

# Form Validation

The Rich Text Editor supports both the reactive and template-driven form-building technologies.

## Template driven forms

The template-drive forms use the `angular` directives in view to handle the forms controls.
To enable the template-driven, import the FormsModule into corresponding app component.

For more details about template-driven
forms, refer to:<https://angular.io/guide/forms#template-driven-forms>.

Mention the `name` attribute to Rich Text Editor element that can be used to identify the form element. To register a Rich Text Editor element to ngForm, give the ngModel to it.
So, the FormsModule will automatically detect the Rich Text Editor as a form element.
After that, the Rich Text Editor value will be selected based on the ngModel value.

The following example demonstrates how to achieve a two-way data binding.

{% tab template="rich-text-editor/form-support", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, RichTextEditorComponent  } from '@syncfusion/ej2-angular-richtexteditor';
  @Component({
      selector: 'app-root',
      template: `<form #rteForm="ngForm">
              <div class="form-group">
                  <ejs-richtexteditor #templateRTE id="name" #name='ngModel' [(value)]='value' required name="name" [(ngModel)]="value" (created)="rteCreated()"></ejs-richtexteditor>
                  <div *ngIf="(name.invalid && (name.dirty || name.touched))" class="alert alert-danger">
                      <div *ngIf="name.errors.required">
                          Value is required.
                      </div>
                  </div>
              </div>
              <div>
                  <button type="submit" ejs-button [disabled]="!rteForm.valid">Submit</button>
                  <button type="reset" ejs-button style="margin-left: 20px">Reset</button>
              </div>
          </form>`,
      providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
  })
  export class AppComponent  {
    public value: any = null;
  @ViewChild('templateRTE') rteEle: RichTextEditorComponent;

  rteCreated(): void {
      this.rteEle.element.focus();
  }

 onCreate(): void {
    document.querySelector().style.display='inline';
  }
  }

```

{% endtab %}

## Reactive forms

The reactive forms use the reactive model-driven technique to handle form data between the component and view. So, it is called as `model-driven` forms. It listens the form data changes between App component and view also returns the valid states and values of form elements.

For more details about Reactive Forms, refer to: <https://angular.io/guide/reactive-forms>.

For the reactive forms, import a ReactiveFormsModule into app module as well as the FormGroup,FormControl should be imported to app component. The FormGroup is used to declare `formGroupName` for the form group and the FormControl is used to declare `formControlName` for form controls. You can declare the formControlName to Rich Text Editor a value object must be created to the FormGroup and each value will be the default value of the form control.

The following example demonstrates how to use the reactive forms.

{% tab template="rich-text-editor/form-support", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, RichTextEditorComponent } from '@syncfusion/ej2-angular-richtexteditor';
import { FormBuilder, FormControl, FormGroup, Validators } from '@angular/forms';
@Component({
    selector: 'app-root',
    template: '<div class="control-section">    <div class="content-wrapper">        <div id="content" class="box-form" style="margin: 0 auto; max-width:750px; padding:25px">            <form [formGroup]="rteForm" (ngSubmit)="onSubmit()">                <div class="form-group">                    <ejs-richtexteditor #fromRTE formControlName="name" (created)="rteCreated()">                    </ejs-richtexteditor>                    <div *ngIf="rteForm.invalid && rteForm.controls.name.touched" class="alert alert-danger">                        <div *ngIf="rteForm.controls.name.errors.required">                            Value is required.                        </div>                    </div>                </div>                <div class="form-group">                    <button type="submit" ejs-button [disabled]="!rteForm.valid">Submit</button>                    <button type="reset" ejs-button (click)="rteForm.reset()" style="margin-left: 20px">Reset</button>                </div>            </form>        </div>    </div></div>',
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
})
export class AppComponent {

    rteForm: FormGroup;

    @ViewChild('fromRTE')
    private rteEle: RichTextEditorComponent;

    constructor() {
        // <--- inject FormBuilder
    }

    ngOnInit(): void {
        this.rteForm = new FormGroup({
            'name': new FormControl(null, Validators.required)
        });
    }

    rteCreated(): void {
        this.rteEle.element.focus();
    }

    onSubmit(): void {
        alert('Form submitted successfully');
    }
}

```

{% endtab %}