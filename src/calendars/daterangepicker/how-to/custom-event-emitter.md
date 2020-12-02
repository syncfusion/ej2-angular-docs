---
title: "How To"
component: "DateRangePicker"
description: "Miscellaneous aspects of customizing the date range picker"
---

# Custom event Emitter

The **two-way binding** in DateRangePicker can also be achieved using the custom event binding and property binding in the controls present in two different components. To create custom event, we need to create an instance of `event emitter`.

In the following example, **property binding** is used to share the data from the parent component to the child component using [@input](https://angular.io/api/core/Directive#inputs) directive and **custom event binding** is used to share the data from the child component to the parent component by using [@output](https://angular.io/api/core/Directive#outputs) directive.

{% tab template="daterangepicker/custom-binding", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { DateRangePickerComponent } from '@syncfusion/ej2-angular-calendars';

@Component({
    selector: 'app-root',
    template: `
  <div class="parentelement">
   <div class="rangevalue">
   <ejs-daterangepicker id="daterangepicker" #range (change)="deposit()" [value]="value" placeholder="Parent component" floatLabelType="Always" width="200px"></ejs-daterangepicker>
   </div>
   </div>
   <child [xvalue]="value" (valueChange)="valuecheck($event)"> </child>
  `,
})
export class ParentComponent {
    @ViewChild('range')
    public DateRange: DateRangePickerComponent;
    value: Date[];
    constructor() {
        this.value = [new Date("1/1/2019"), new Date("2/1/2020")]
    }
    deposit() {
        this.value = this.DateRange.value;
    }
    valuecheck(args: any) {
        this.value = args;
    }
}

```

{% endtab %}
