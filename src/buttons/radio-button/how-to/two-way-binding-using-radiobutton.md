---
title: "Two way binding using RadioButton"
component: "RadioButton"
description: "Angular RadioButton how to section, two way binding using RadioButton and DropDownList"
---

# Two way binding using RadioButton

In the following example, two-way binding for RadioButton is illustrated with DropDownList component. The steps to achieve two-way binding in RadioButton are as follows,

* Initialize RadioButton component and bind the checked value using ngModel as in the below code using "banana in a box" syntax,

```typescript

<ejs-radiobutton [label]='payment' [value]="payment" name="payment" [(ngModel)]="value"></ejs-radiobutton>

```

* Initialize DropDownList component and assign the [`value`](https://ej2.syncfusion.com/angular/documentation/api/drop-down-list#value) property value like the below code,

```typescript
<ejs-dropdownlist [dataSource]='paymentMethod' [(value)]="value" ></ejs-dropdownlist>
```

* Now, the changes made in RadioButton will reflect in DropDownList (i.e. Selected option in radio button will be reflected in DropDownList  ) and vice versa.

{% tab template= "radio-button/binding", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // To customize RadioButton appearance
    template: ` <div class="radioButton-control">
                    <h4>Select a payment method</h4>
                    <div class="row" *ngFor='let payment of paymentMethod'>
                        <ejs-radiobutton [label]='payment' [value]="payment" name="payment" [(ngModel)]="value"></ejs-radiobutton>
                    </div>
                </div>
                <div class="dropDownList-control">
                    <h4>Payment Method</h4>
                    <ejs-dropdownlist [dataSource]='paymentMethod' [(value)]="value" ></ejs-dropdownlist>
                </div>`
})

export class AppComponent {
    public paymentMethod: string[] = ['Credit card', 'Debit card', 'Net Banking', 'Other Wallets' ];
    public value:string = "Credit card";
}

```

{% endtab %}