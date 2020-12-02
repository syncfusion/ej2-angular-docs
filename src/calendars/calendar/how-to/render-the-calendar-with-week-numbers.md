---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Render Calendar with week number

You can enable the `weekNumber` in Calendar by using the
[`weekNumber`](../../api/calendar#weeknumber)
property.

{% tab template="calendar/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <!-- Sets the weekNumber -->
        <ejs-calendar [value]='dateValue' weekNumber='true'></ejs-calendar>
        `
})

export class AppComponent {
    public dateValue: Date = new Date();
}

```

{% endtab %}
