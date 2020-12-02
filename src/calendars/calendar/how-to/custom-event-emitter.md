---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Custom event Emitter

The **two-way binding** in Calendar can also be achieved using the custom event binding and property binding in the controls present in two different components. To create custom event, we need to create an instance of `event emitter`.

In the following example, **property binding** is used to share the data from the parent component to the child component using [@input](https://angular.io/api/core/Directive#inputs) directive and **custom event binding** is used to share the data from the child component by using [@output](https://angular.io/api/core/Directive#outputs) directive.

{% tab template="calendar/custom-binding", isDefaultActive = "true",  sourceFiles="app/**/*.ts,styles.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { CalendarComponent } from '@syncfusion/ej2-angular-calendars';

@Component({
    selector: 'app-root',
    template: `
  <div class="parentelement">
  <span><h4>Parent Component</h4></span>
   <div class="datevalue">
   <ejs-calendar id="calendar" #calendar (change)="deposit()" [value]="value" width="200px"></ejs-calendar>
   </div>
   </div>
   <child [xvalue]="value" (valueChange)="valuecheck($event)"> </child>
  `,
})
export class ParentComponent {
    @ViewChild('calendar')
    public calendar: CalendarComponent;
    value: Date;
    constructor() {
        this.value = new Date("2/1/2020");
    }
    deposit() {
        this.value = this.calendar.value;
    }
    valuecheck(args: any) {
        this.value = args;
    }
}

```

{% endtab %}