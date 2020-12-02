---
title: "How To"
component: "TimePicker"
description: "Miscellaneous aspects of customizing the time picker"
---

# Two-way binding

The following example demonstrates how to achieve **two-way binding** by binding the **value** to the first TimePicker component by using property binding and binding the model data using **ngModel** to the second TimePicker component. The **value** of the TimePicker will get change, when their is any change in the property value or model value.

> The two-way binding can also be achieved only by using **property binding** or **model binding** in the TimePicker component.

{% tab template="timepicker/two-way", isDefaultActive = "true", sourceFiles="app/**/*.ts,styles.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { TimePickerComponent } from '@syncfusion/ej2-angular-calendars';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template: `
        <!-- two-way binding using the value binding and model binding in the TimePicker --->
        <ejs-timepicker id="firsttime" #ejTimePicker [(value)]='value' width="230px"></ejs-timepicker>
        <ejs-timepicker id="secondtime" #ejTimePickers [(ngModel)]='value' width="230px"></ejs-timepicker>
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
