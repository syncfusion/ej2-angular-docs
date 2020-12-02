---
title: "Multi Selection"
component: Calendar
description: "Calendar supports multiple date selection to allow users to select more than one date."
---

# Multi Selection

Calendar provides an option to select **single** or **multiple dates** or **sequence of dates** by using [`isMultiSelection`](../api/calendar#ismultiselection) and [`values`](../api/calendar#values) properties. By default, [`isMultiSelection`](../api/calendar#ismultiselection) property will be in disabled state.

The following example demonstrates the functionality of  `isMultiSelection` property and `values` properties in the Calendar control.

{% tab template="calendar/getting-started",isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
              <!-- Sets the isMultiSelection and values properties-->
              <ejs-calendar [values]='dateValues' [isMultiSelection]='multiSelect'></ejs-calendar>
        `
})
export class AppComponent {
    public dateValues: Date[] = [new Date('1/1/2020'), new Date('1/15/2020'), new Date('1/3/2020'), new Date('1/25/2020')];
    public multiSelect: Boolean = true;
    constructor() {
    }
}

```

{% endtab %}