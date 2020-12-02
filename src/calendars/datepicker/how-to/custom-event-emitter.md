---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Custom event Emitter

The **two-way binding** in DatePicker can also be achieved using the custom event binding and property binding in the controls present in two different components. To create custom event, we need to create an instance of `event emitter`.

In the following example, **property binding** is used to share the data from the parent component to the child component using [@input](https://angular.io/api/core/Directive#inputs) directive and **custom event binding** is used to share the data from the child component to the parent component by using [@output](https://angular.io/api/core/Directive#outputs) directive.

{% tab template="datepicker/custom-binding", isDefaultActive = "true",  ssourceFiles="app/**/*.ts,app/**/*.html,styles.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { DatePickerComponent } from '@syncfusion/ej2-angular-calendars';


@Component({
    selector: 'app-root',
    template: `
  <div class="parentelement">
   <div class="datevalue">
   <ejs-datepicker id="datepicker" #date (change)="deposit()" placeholder="Parent component" floatLabelType="Always" [value]="value" width="200px"></ejs-datepicker>
   </div>
   </div>
   <child [xvalue]="value" (valueChange)="valuecheck($event)"> </child>
  `,
})
export class ParentComponent {
    @ViewChild('date')
    public Date: DatePickerComponent;
    value: Date;
    constructor() {
        this.value = new Date("2/1/2020");
    }
    deposit() {
        this.value = this.Date.value;
    }
    valuecheck(args: any) {
        this.value = args;
    }
}

```

{% endtab %}
