---
title: "How To"
component: "DateRangePicker"
description: "Miscellaneous aspects of customizing the date range picker"
---

# Custom Validation using `FormValidator`

The client side validation takes place in the browser to avoid the waiting time
to receive the response from sever. It validates the
form elements to provide the better feedback messages to correct the every fields before the form submission.

The following sample demonstrate how to achieve the client side validation in DateRangePicker component by using `FormValidator`
function. It provides an option to customize the feedback
error messages to the corresponding fields to take action to resolve the issue.

{% tab template="daterangepicker/how-to", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { DateRangePickerComponent } from '@syncfusion/ej2-angular-calendars';
import { FormValidator, FormValidatorModel } from '@syncfusion/ej2-inputs';

@Component({
    selector: 'app-root',
    template: `<form id="form-element" class="form-vertical">
    <ejs-daterangepicker #ejDateRange id='daterangepicker' placeholder='Enter a date range' width="275px"(blur)="onFocusOut()" (change)= "onChange($event)"></ejs-daterangepicker>
    </form>`
})

export class AppComponent implements OnInit {
    @ViewChild('formElement') element: any;
    @ViewChild('ejDateRange') ejDateRange: DateRangePickerComponent;
    public formObject: FormValidator;
    ngOnInit() {
        let customFn: (args: {
            [key: string]: string
        }) => boolean = (args: {
            [key: string]: string
        }) => {
            return ((this.ejDateRange.value[0]).getFullYear() > 1990 && (this.ejDateRange.value[1]).getFullYear( < 2020);
            };
            let options: FormValidatorModel = {
                rules: {
                    'daterangepicker': {
                        required: [true, "Value is required"]
                    }
                },
                customPlacement: (inputElement: HTMLElement, errorElement: HTMLElement) => {
                    inputElement.parentElement.parentElement.appendChild(errorElement);
                }
            };
            this.formObject = new FormValidator('#form-element', options);
            this.formObject.addRules('daterangepicker', {
                range: [customFn, "Please select a date range between years from 1990 to 2020"]
            });
            this.formObject = new FormValidator('#form-element', options);
        }
        public onFocusOut(): void {
            this.formObject.validate("daterangepicker");
        }

        public onChange(args: any) {
            if (this.ejDateRange.value != null)
                this.formObject.validate("daterangepicker");
        }
    }

```

{% endtab %}
