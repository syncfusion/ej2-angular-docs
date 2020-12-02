---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Two-way binding

The following example demonstrates how to achieve **two-way binding** by binding the **value** to the first DatePicker component by using property binding and binding the model data using **ngModel** to the second DatePicker component. The **value** of the DatePicker will get change, when their is any change in the property value or model value.

> The two-way binding can also be achieved only by using **property binding** or **model binding** in the DatePicker component.

{% tab template="datepicker/two-way", isDefaultActive = "true", sourceFiles="app/**/*.ts,styles.css" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template: `
        <!-- two-way binding using the value binding and model binding in the DatePicker --->
        <ejs-datepicker id="fisrtdatepicker" #ejDatePicker [(value)]='value' width="230px"></ejs-datepicker>
        <ejs-datepicker id="seconddatepicker" #ejDatePickers [(ngModel)]='value' width="230px"></ejs-datepicker>
        `
})
export class AppComponent {
    value: Date;
    constructor() {
        this.value = new Date('1/1/2020');
    }
}
```

{% endtab %}
