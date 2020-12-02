# Perform custom validation using FormValidator

This section explains how to perform custom validation on the NumericTextBox using FormValidator. The NumericTextBox will be validated when the value changes or the user clicks the submit button.
Validation can be performed by adding custom validation in the rules collection of the FormValidator.

{% tab template="numerictextbox/custom-validation", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { NumericTextBoxComponent  } from '@syncfusion/ej2-angular-inputs';
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';

@Component({
    selector: 'app-root',
    // Initializes the NumericTextBox
    //Renders submit button for validating the NumericTextBox
    template: `
    <form #formElement class="form-horizontal">
        <div class="form-group">
            <div class="col-sm-6">
                <ejs-numerictextbox #numeric="" id="numeric"  [strictMode]='false'  min='10' max='100' name="numeric" placeholder= 'NumericTextbox' floatLabelType= 'Always'  (created)="onCreate($event)" (change)= "onChange($event)"></ejs-numerictextbox>
            </div>
                <button type="button" id="submit_btn" (click)="btnClick()" style="margin-top: 10px">Submit</button>
        </div>
    </form>
    `
})

export class AppComponent {
    @ViewChild('formElement') element;
    @ViewChild('numeric') numeric: NumericTextBoxComponent;
    public formObject: FormValidator;
    ngAfterViewInit() {
        let customFn: (args: { [key: string]: string }) => boolean = (args: { [key: string]: string }) => {
            if(numeric.value>=10 && numeric.value<=100) {
                return true;
            }
            else {
                return false;
            }
        };
        // sets required property in the FormValidator rules collection
        let options: FormValidatorModel = {
            rules: {
               'numericRange': { required: [true, "Number is required"] },
            },
            //to place the error message in custom position
            customPlacement: (inputElement: HTMLElement, errorElement: HTMLElement) => {
                inputElement.parentNode.parentNode.parentNode.appendChild(errorElement);
            }
        };
        this.formObject = new FormValidator(this.element.nativeElement, options);

        this.formObject.addRules('numericRange', { range: [customFn, "Please enter a number between 10 to 100"] });
        var proxy = this;
    }
    // validates NumericTextBox while value changes
    public onChange(args){
        if (numeric.value != null)
            this.formObject.validate("numericRange");
    }
    public onCreate(){
          document.getElementById("numeric").setAttribute("name", "numericRange");
    }
    public btnClick(): void {
        // validates the NumericTextBox
        this.formObject.validate("numericRange");
        // checks for incomplete value and alerts the form
        let ele: HTMLInputElement = <HTMLInputElement>document.getElementById('numeric');
            if (ele.value !== "" && ele.value >=10 && ele.value<=100) {
                alert("Submitted");
            }
    }
}

```

{% endtab %}