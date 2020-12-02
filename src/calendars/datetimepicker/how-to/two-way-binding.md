---
title: "How To"
component: "DateTimePicker"
description: "Miscellaneous aspects of customizing the date time picker"
---

# Two-way binding

The following example demonstrates how to achieve **two-way binding** by binding the **value** to the first DateTimePicker component by using property binding and binding the model data using **ngModel** by using model binding to the DateTimePicker component. The **value** of the DateTimePicker will get change, when their is any change in the property value or model value.

> The two-way binding can also be achieved only by using **property binding** or **model binding** in the DateTimePicker component.

{% tab template="datetimepicker/two-way", isDefaultActive = "true", sourceFiles="app/**/*.ts,styles.css" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <!-- two-way binding using the value binding and model binding in the DateTimePicker --->
        <ejs-datetimepicker id="fisrtdatetime" #ejDateTimePicker [(value)]='value' width="230px"></ejs-datetimepicker>
        <ejs-datetimepicker id="seconddatetime" #ejDateTimePickers [(ngModel)]='value' width="230px"></ejs-datetimepicker>
        `
})
export class AppComponent {
    value: Date;
    constructor() {
        this.value = new Date("1/1/2019 1:30 PM");
    }
}
```

{% endtab %}