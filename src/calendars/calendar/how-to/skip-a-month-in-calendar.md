---
title: "How To"
component: "Calendar"
description: "Miscellaneous aspects of customizing the calendar"
---

# Skip a month in calendar

The following example demonstrates how to skip a month in a Calendar while clicking the previous
and next icon. Here we have used
the [`navigated`](../../api/calendar#navigated)
event to skip a month using
[`NavigateTo`](../../api/calendar#navigateto)
  method.

{% tab template="calendar/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { CalendarComponent } from '@syncfusion/ej2-angular-calendars';

@Component({
    selector: 'app-root',
    template: `
        <ejs-calendar #ejCalendar (navigated)='onNavigate($event)'></ejs-calendar>
        `
})

export class AppComponent {
    @ViewChild('ejCalendar') ejCalendar: CalendarComponent;
   //skips a month while cliking previous and next icon in month view.
   onNavigate(args):void {
    let date: Number;
    if ((<HTMLInputElement>event.currentTarget).classList.contains('e-next')) {
        //incrementing the month while clicking the next icon
        date = new Date(args.date.setMonth(args.date.getMonth() + 1));
    }
    if ((<HTMLInputElement>event.currentTarget).classList.contains('e-prev')) {
        //decrementing the month while clicking the previous icon
        date = new Date(args.date.setMonth(args.date.getMonth() - 1));
    }
    if (args.view == 'month') {
        this.ejCalendar.navigateTo('month', new Date('' + date));
    }
}
}

```

{% endtab %}
