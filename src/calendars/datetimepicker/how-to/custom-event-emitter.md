---
title: "How To"
component: "DateTimePicker"
description: "Miscellaneous aspects of customizing the date time picker"
---

# Custom event Emitter

The **two-way binding** in DateTimePicker can also be achieved using the custom event binding and property binding in the controls present in two different components. To create custom event, we need to create an instance of `event emitter`.

In the following example, **property binding** is used to share the data from the parent component to the child component using [@input](https://angular.io/api/core/Directive#inputs) directive and **custom event binding** is used to share the data from the child component to the parent component by using [@output](https://angular.io/api/core/Directive#outputs) directive.

{% tab template="datetimepicker/custom-binding", isDefaultActive = "true",  sourceFiles="app/**/*.ts,styles.css" %}

```typescript
import { Component } from '@angular/core';


@Component({
    selector: 'app-root',
    template: `
  <div class="parentelement">
   <div class="datevalue">
   <ejs-datetimepicker id="datetime" #datetime (change)="deposit()" placeholder="Parent component" floatLabelType="Always" [value]="value" width="200px"></ejs-datetimepicker>
   </div>
   </div>
   <child [xvalue]="value" (valueChange)="valuecheck($event)"> </child>
  `,
})
export class ParentComponent {
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