---
title: "How To"
component: "DateRangePicker"
description: "Miscellaneous aspects of customizing the date range picker"
---

# Two-way binding

The following example demonstrates how to achieve **two-way binding** by binding the **value** to the first DateRangePicker component by using property binding and binding the model data using **ngModel** to the second DateRangePicker component. The **value** of the DateRangePicker will get change, when their is any change in the property value or model value.

> The two-way binding can also be achieved only by using **property binding** or **model binding** in the DateRangePicker component.

{% tab template="daterangepicker/two-way", isDefaultActive = "true", sourceFiles="app/**/*.ts,styles.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { DateRangePickerComponent } from '@syncfusion/ej2-angular-calendars';

@Component({
    selector: 'app-root',
    template: `
        <!-- two-way binding using the value binding and model binding in the DateRangePicker --->
        <ejs-daterangepicker #ejDateRangePicker [(value)]='value'  width="230px"></ejs-daterangepicker>
        <ejs-daterangepicker #ejDateRangePickers [(ngModel)]='value'  width="230px"></ejs-daterangepicker>
        `
})
export class AppComponent {
    value: Date;
    constructor() {
        this.value = [new Date('1/1/2020'), new Date('2/1/2023')];
    }
}
```

{% endtab %}
