---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Change the first day of week

The Calendar provides an option to change the first day of the week by using the

[`firstDayOfWeek`](../../api/calendar#firstdayofweek)
property.
Day of the week starts from 0(Sunday) to 6(Saturday).

> By default, the first day of week will be based on culture.

The following example demonstrates the Calendar with `Tuesday` as first day of the week.

{% tab template="calendar/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <!-- Sets the firstDayOfWeek -->
        <ejs-calendar [value]='dateValue' [firstDayOfWeek]='startWeek'></ejs-calendar>
        `
})

export class AppComponent {
    public dateValue: Date = new Date();
    public startWeek: number = 2;
}

```

{% endtab %}