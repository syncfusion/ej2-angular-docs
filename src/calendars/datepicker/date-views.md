---
title: "Date Views"
component: "DatePicker"
description: "Pre-defined views in date picker allows to perform easy navigation to select any date."
---

# Start View and Depth Restriction

The DatePicker has the following predefined views
that provides a flexible way to navigate back and forth to select the date.

| **View** | **Description** |
| --- | --- |
| month(default) | Displays the days in a month |
| year | Displays the months in a year |
| decade | Displays the years in a decade |

## Start view

You can use the
[`start`](../api/datepicker#start)
 property to define the initial rendering view.

The following example demonstrates how to create a DatePicker with `decade` as initial rendering view.

{% tab template="datepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-datepicker start='Decade' placeholder='Enter date'></ejs-datepicker>`
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## Depth view restriction

Define the [`depth`](../api/datepicker#depth) property to control the view navigation.

> Always the depth view has to be smaller than the start view, otherwise the view restriction
will be not restricted.

The following example demonstrates how to create a DatePicker that allows users to select a month.

{% tab template="datepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-datepicker start='Decade' depth='Year' placeholder='Enter date'></ejs-datepicker>`
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

> To know more about Calendar views refer the Calendar's
[Calendar Views](../calendar/calendar-views/)
section.