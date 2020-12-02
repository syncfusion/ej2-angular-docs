---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Custom Validation using `FormValidator`

The client side validation takes place in the browser to avoid the waiting time
to receive the response from sever. It validates the
form elements to provide the better feedback messages to correct the every fields before the form submission.

To achieve the client side validation in a DatePicker component by using `FormValidator`
function. It provides an option to customize the feedback
error messages to the corresponding fields to take action to resolve the issue.

{% tab template="datepicker/how-to", isDefaultActive = "true",  sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { DatePickerComponent } from '@syncfusion/ej2-angular-calendars';
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';
@Component({
    selector: 'app-root',
    template: `<form id="form-element" class="form-vertical">
    <ejs-datepicker #ejDate id='datepicker' placeholder='Enter date' width="275px"(blur)="onFocusOut()" (change)= "onChange($event)"></ejs-datepicker>
    </form>`
})
export class AppComponent implements OnInit {
    @ViewChild('formElement') element: any;
    @ViewChild('ejDate') ejDate: DatePickerComponent;
    public formObject: FormValidator;
    ngOnInit() {
        // custom validator function.
        let customFn: (args: {
            [key: string]: string
        }) => boolean = (args: {
            [key: string]: string
        }) => {
            return ((this.ejDate.value).getFullYear() > 1990 && (this.ejDate.value).getFullYear() < 2020);
        };
        let options: FormValidatorModel = {
            rules: {
                'datepicker': {
                    required: [true, "Value is required"]
                }
            },
            customPlacement: (inputElement: HTMLElement, errorElement: HTMLElement) => {
                inputElement.parentElement.parentElement.appendChild(errorElement);
            }
        };
        this.formObject = new FormValidator('#form-element', options);
        this.formObject.addRules('datepicker', {
            range: [customFn, "Please select a date between years from 1990 to 2020"]
        });
        this.formObject = new FormValidator('#form-element', options);
    }
    // Form validation takes place when focus() event of DatePicker is triggered.
    public onFocusOut(): void {
        this.formObject.validate("datepicker");
    }
    // Custom validation takes place when value is changed.
    public onChange(args: any) {
        if (this.ejDate.value != null)
            this.formObject.validate("datepicker");
    }
}

```

{% endtab %}
