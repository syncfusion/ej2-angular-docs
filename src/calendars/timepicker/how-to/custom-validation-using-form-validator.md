---
title: "How To"
component: "TimePicker"
description: "Miscellaneous aspects of customizing the time picker"
---

# Custom Validation using `FormValidator`

The client side validation takes place in the browser to avoid the waiting time
to receive the response from sever. It validates the
form elements to provide the better feedback messages to correct the every fields before the form submission.

To achieve the client side validation in a TimePicker component by using `FormValidator`
function. It provides an option to customize the feedback
error messages to the corresponding fields to take action to resolve the issue.

{% tab template="timepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { TimePickerComponent } from '@syncfusion/ej2-angular-calendars';
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';

@Component({
    selector: 'app-root',
    template: `<form id="form-element" class="form-vertical">
    <ejs-timepicker #ejTime id='timepicker' placeholder='Select a time' width="275px"(blur)="onFocusOut()" (change)= "onChange($event)"></ejs-timepicker>
    </form>`
})

export class AppComponent implements OnInit {
    @ViewChild('formElement') element: any;
    @ViewChild('ejTime') ejTime: TimePickerComponent;
    public formObject: FormValidator;
    ngOnInit() {
        // custom validator function.
        let customFn: (args: {
            [key: string]: string
        }) => boolean = (args: {
            [key: string]: string
        }) => {
            return ((this.ejTime.value).getHours() < 10);
        };
        let options: FormValidatorModel = {
            rules: {
                'timepicker': {
                    required: [true, "Value is required"]
                }
            },
            customPlacement: (inputElement: HTMLElement, errorElement: HTMLElement) => {
                inputElement.parentElement.parentElement.appendChild(errorElement);
            }
        };
        this.formObject = new FormValidator('#form-element', options);
        this.formObject.addRules('timepicker', {
            range: [customFn, "Please select a time between 12:00 AM to 10:00 AM"]
        });
        this.formObject = new FormValidator('#form-element', options);
    }
    // Form validation takes place when focus() event of timepicker is triggered.
    public onFocusOut(): void {
        this.formObject.validate("timepicker");
    }
    // Custom validation takes place when value is changed.
    public onChange(args: any) {
        if (this.ejTime.value != null)
            this.formObject.validate("timepicker");
    }
}

```

{% endtab %}