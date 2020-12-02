---
title: "Calendar Views"
component: "Calendar"
description: "Pre-defined views in calendar allows to perform easy navigation to select any date."
---

# Calendar Views

The Calendar has the following pre-defined views
that provides a flexible way to navigate back and forth to select the date.
Use the
[`start`](../api/calendar#start)
property to change the default view of the Calendar.

| **View** | **Description** |
| --- | --- |
| month (default) | Displays the days in a month |
| year | Displays the months in a year |
| decade | Displays the years in a decade |

The following example demonstrates how to set the `year` as the start view of the Calendar.

{% tab template="calendar/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <!-- Sets the value, start-->
        <ejs-calendar  [value]='dateValue' start='Year'></ejs-calendar>
        `
})

export class AppComponent {
    public dateValue: Object = new Date();
    constructor() {
    }
}

```

{% endtab %}

## View Restriction

Calendar view navigation can be restricted by defining the  [`start`](../api/calendar#start)
and [`depth`](../api/calendar#depth)
property that allows you to select the date from that view.

By defining the start and depth property with the different view, drill-
down and drill-up views navigation can be limited to the user. Calendar views will be drill-down up to the
view which is set in `depth` property and drill-up up to the view which is set in `start` property.

> Always the depth view has to be smaller than the start view.

{% tab template="calendar/getting-started", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <!-- Sets the value, start and depth-->
        <ejs-calendar #ejCalendar [value]='dateValue' start='Decade' depth='Year'></ejs-calendar>
        `
})

export class AppComponent {
    public dateValue: Object = new Date();
    constructor() {
    }
}
```

{% endtab %}

You can restrict the calendar's drill down navigation by defining the
[`start`](../api/calendar#start)
  and
  [`depth`](../api/calendar#depth)
  property
with same view that allows to select the date on that view itself.

The following example demonstrates how to select the dates in `year` view.

{% tab template="calendar/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <!-- Sets the value, start and depth"-->
        <ejs-calendar #ejCalendar [value]='dateValue' start='Year' depth='Year'></ejs-calendar>
        `
})

export class AppComponent {
    public dateValue: Object = new Date();
    constructor() {
    }
}
```

{% endtab %}
