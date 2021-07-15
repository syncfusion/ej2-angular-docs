---
title: "Forms support"
component: "Uploader"
description: "Explains how to integrate the file upload control in an HTML form (synchronous mode) and submit a form with selected files."
---

# Forms support (synchronous upload)

The uploader component works with HTML form like default file input.
The following configuration is must to make the uploader work inside the form.

    *   `saveUrl` and `removeUrl` must be null.
    *   `autoUpload` must be disabled.
    *   `name` attribute must be added in input element.

The selected or dropped files are received as a collection in form action when the form is submitted.
The form action handles the server-side operations that manage the file upload process.
When you reset the form, the file list and data will be cleared.

{% tab template="uploader/formsupport", sourceFiles="app/**/*.ts, formsupport.css, formsupport.html"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { EmitType } from '@syncfusion/ej2-base';
import { Dialog } from '@syncfusion/ej2-popups';
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';
/**
 * Default Uploader Default Component
 */
@Component({
    selector: 'app-root',
    templateUrl: 'formsupport.html',
    styleUrls: ['formsupport.css']
})
export class AppComponent {
    @ViewChild('Dialog')
    public Dialog: DialogComponent;
     public width: string = '335px';
     public visible: boolean = false;
     public content: string = 'Your details has been updated successfully, Thank you';
     public target: string = '#control_wrapper';
     public isModal: boolean = true;
     public animationSettings: object = {
            effect: 'Zoom'
        }
     public options: object = {
            rules: {
            'name': {
                required: true
            },
            'email': {
                required: true
            },
            'upload': {
                required: true
            }
            }
        }

        @ViewChild('formElement') element: any;

        ngAfterViewInit() {
          let formObject: FormValidator = new FormValidator(this.element.nativeElement, this.options);
        // validate all input elements in the form
            }

     browseClick() {
        document.getElementsByClassName('e-file-select-wrap')[0].querySelector('button').click(); return false;
      }
    Submit() {
            this.onFormSubmit();
    }
    public onFileSelect: EmitType<Object> = (args: any) => {
        let inputElement: HTMLInputElement  = document.getElementById('upload') as HTMLInputElement;
        inputElement.value = args.filesData[0].name;
    }

    // Close the modal Dialog on overlay click
    public overlayClick(): void {
        this.Dialog.hide();
    }

    public onFormSubmit(): void {
    let formObject: FormValidator = new FormValidator("#form1", this.options);
    let formStatus: Boolean = formObject.validate();
    if (formStatus) {
       formObject.element.reset();
        this.Dialog.show();
    }
    }
}

```

{% endtab %}

## Template-driven forms

By using `ngModel` directive, you can bind the model to the uploader in template-driven forms.
For more details, refer to the [Angular Documentation](https://angular.io/guide/forms#template-driven-forms)

The following sample demonstrates how to render uploader component with required validation inside the template-driven forms.

{% tab template="uploader/template-driven", sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  template: `<div class="control-section">
        <div class="col-lg-12">
          <h4 class="form-title">Photo Contest</h4>
        <div class="control_wrapper" id="control_wrapper" style="margin: 10px auto;">
            <form id="template_driven" #userForm="ngForm" novalidate>
                <div class="form-group" style="padding-top: 11px;">
                    <div class="e-float-input">
                        <input type="text" id="name" #nameval='ngModel' name="name" required ngModel>
                        <span class="e-float-line"></span>
                        <label class="e-float-text e-label-top" for="name">Name</label>
                        <div *ngIf="(nameval.invalid && (nameval.dirty || nameval.touched))">
                            <div class="e-error" *ngIf="nameval.errors.required">
                                * Enter your name
                            </div>
                        </div>
                    </div>
                </div>
                  <div class="form-group" style="padding-top: 11px;">
                      <div class="e-float-input upload-area">
                          <input type="text" id="upload" #uploadval='ngModel' [(ngModel)]="uploadInput" readonly name="upload" required ngModel>
                          <button id="browse" class="e-control e-btn e-info" (click)='browseClick()'>Browse...</button>
                          <span class="e-float-line"></span>
                          <label class="e-float-text e-label-top" for="upload">Choose a file</label>
                          <div *ngIf="(uploadval.invalid && (uploadval.dirty || uploadval.touched))">
                              <div class="e-error" *ngIf="uploadval.errors.required">
                                  * Select a file
                              </div>
                          </div>
                      </div>
                      <ejs-uploader #defaultupload id='fileupload' allowedExtensions="image/*" [autoUpload]=false [multiple]='multiple' (selected)='onFileSelect($event)'></ejs-uploader>
                  </div>

                  <div class="form-group" style="padding-top: 11px;">
                    <div class="submitBtn">
                        <button class="submit-btn e-btn" id="submit-btn" [disabled]="userForm.invalid" type="reset" (click)= "Submit()">Submit</button>
                        <div class="desc"><span>*This button is not a submit type and the form submit handled from externally.</span></div>
                    </div>
                  </div>
          </form>
          <ejs-dialog id="confirmationDialog" #Dialog [buttons]='dlgButtons' [animationSettings]='animationSettings' [header]='formHeader' [showCloseIcon]='showCloseIcon' [content]='content'  [target]='target' [width]='width' [visible]="visible" [isModal]="isModal" >
          </ejs-dialog>
    </div>
  </div>
</div>`
})
export class AppComponent  {
  @ViewChild('Dialog')
  public dialogObj: DialogComponent;
  public width: string = '335px';
  public visible: boolean = false;
  public multiple: boolean = false;
  public showCloseIcon: Boolean = true;
  public formHeader: string = 'Success';
  public content: string = 'Your details have been updated successfully, Thank you.';
  public target: string = '#control_wrapper';
  public isModal: boolean = true;
  public animationSettings: object = {
    effect: 'Zoom'
  };
  public uploadInput: string = '';
  public dlgBtnClick: EmitType<object> = () => {
    this.dialogObj.hide();
  }
  public dlgButtons: Object[] = [{ click: this.dlgBtnClick.bind(this), buttonModel: { content: 'Ok', isPrimary: true } }];
    @ViewChild('formElement') element: any;

  public browseClick() {
     document.getElementsByClassName('e-file-select-wrap')[0].querySelector('button').click(); return false;
   }
   public Submit(): void {
    this.onFormSubmit();
  }
 public onFileSelect: EmitType<Object> = (args: any) => {
  this.uploadInput = args.filesData[0].name;
 }

 public onFormSubmit(): void {
   this.dialogObj.show();
 }
}

```

{% endtab %}

## Reactive forms

You can render the uploader component inside the reactive forms.
The reactive forms rendered with the help of `FormGroup`.
For more details, refer to the [Angular Documentation](https://angular.io/guide/reactive-forms)

The following sample demonstrates how to render uploader component with required validation inside the `reactive forms`.

{% tab template="uploader/reactive", sourceFiles="app/**/*.ts,index.css"  %}

```typescript
import { Component, Inject, OnInit, ViewChild } from '@angular/core';
import { FormGroup, FormBuilder, Validators, FormControl } from '@angular/forms';
import { EmitType } from '@syncfusion/ej2-base';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';

@Component({
  selector: 'app-root',
  template: `<div class="control-section">
    <div class="col-lg-12">
      <h4 class="form-title">Photo Contest</h4>
        <div class="control_wrapper" id="control_wrapper" style="margin: 25px auto;">
          <form id="reactive" [formGroup]="form">
              <div class="form-group" style="padding-top: 11px;">
                  <div class="e-float-input">
                      <input type="text" id="name" name="name" class="required" formControlName="name">
                      <span class="e-float-line"></span>
                      <label class="e-float-text e-label-top" for="name">Name</label>
                  </div>
                  <app-field-error-display [displayError]="isFieldValid('name')" errorMsg="* Please Enter your name">
                  </app-field-error-display>
              </div>
              <div class="form-group" style="padding-top: 11px;">
                  <div class="e-float-input upload-area">
                      <input type="text" id="upload" name="upload" [(ngModel)]="uploadInput" readonly formControlName="upload" class="required">
                      <button id="browse" class="e-control e-btn e-info" (click)='browseClick()'>Browse...</button>
                      <span class="e-float-line"></span>
                      <label class="e-float-text e-label-top" for="upload">Choose a file</label>
                  </div>
                  <app-field-error-display [displayError]="isFieldValid('upload')" errorMsg="* Select any file">
                  </app-field-error-display>
                  <ejs-uploader #defaultupload id='fileupload' allowedExtensions="image/*" [autoUpload]=false [multiple]='multiple' (selected)='onFileSelect($event)'></ejs-uploader>
              </div>
              <div class="form-group" style="padding-top: 11px;">
                <div class="submitBtn">
                  <button class="submit-btn e-btn" id="submit-btn" [disabled]="form.invalid" (click)= "Submit()">Submit</button>
                  <div class="desc"><span>*This button is not a submit type and the form submit handled from externally.</span></div>
                </div>
              </div>
          </form>
          <ejs-dialog id="confirmationDialog" #Dialog [buttons]='dlgButtons' [animationSettings]='animationSettings' [header]='formHeader' [showCloseIcon]='showCloseIcon' [content]='content'  [target]='target' [width]='width' [visible]="visible" [isModal]="isModal" >
          </ejs-dialog>
      </div>
    </div>
</div>`
})
export class AppComponent  {
    @ViewChild('Dialog')
    public dialogObj: DialogComponent;
    public form: FormGroup;
    public width: string = '335px';
    public visible: boolean = false;
    public multiple: boolean = false;
    public showCloseIcon: Boolean = true;
    public formHeader: string = 'Success';
    public content: string = 'Your details have been updated successfully, Thank you.';
    public target: string = '#control_wrapper';
    public isModal: boolean = true;
    public animationSettings: any = {
          effect: 'Zoom'
      };
   private formSumitAttempt: boolean;
   public dlgBtnClick: EmitType<object> = () => {
    this.dialogObj.hide();
  }
  public dlgButtons: Object[] = [{ click: this.dlgBtnClick.bind(this), buttonModel: { content: 'Ok', isPrimary: true } }];
  public uploadInput: string = '';
  public browseClick() {
      document.getElementsByClassName('e-file-select-wrap')[0].querySelector('button').click(); return false;
    }
  public Submit(): void {
    this.onFormSubmit();
  }
  public onFileSelect: EmitType<Object> = (args: any) => {
    this.uploadInput = args.filesData[0].name;
  }

  public onFormSubmit(): void {
    this.formSumitAttempt = true;
    if (this.form.valid) {
      this.dialogObj.show();
      this.form.reset();
    } else {
      this.validateAllFormFields(this.form);
    }
  }

  constructor(@Inject(FormBuilder) public formBuilder: FormBuilder) {}

  ngOnInit() {
    this.form = this.formBuilder.group({
      name: [null, Validators.required],
      upload: [null, Validators.required],
    });
  }

  isFieldValid(field: string) {
    return ((!this.form.get(field).valid && this.form.get(field).touched) ||
    (this.form.get(field).untouched && this.formSumitAttempt));
  }

  validateAllFormFields(formGroup: FormGroup) {
    Object.keys(formGroup.controls).forEach(field => {
      const control = formGroup.get(field);
      if (control instanceof FormControl) {
        control.markAsTouched({ onlySelf: true });
      } else if (control instanceof FormGroup) {
        this.validateAllFormFields(control);
      }
    });
  }
}

```

{% endtab %}

> You can also explore [Angular File Upload](https://www.syncfusion.com/angular-ui-components/angular-file-upload) feature tour page for its groundbreaking features. You can also explore our [Angular File Upload example](https://ej2.syncfusion.com/angular/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
