---
title: "How To"
component: "DatePicker"
description: "Explains how to open the DatePicker popup when the input is focused"
---

# Open the DatePicker popup upon focusing input of DatePicker

You can open the DatePicker popup on input focus by calling the `show` method in the input `focus` event.

The following example demonstrates how to open the DatePicker popup when the input is focused.

{% tab template="datepicker/open-popup", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { CalendarComponent, FocusEventArgs } from '@syncfusion/ej2-angular-calendars';

@Component({
    selector: 'app-root',
    template: `<ejs-datepicker #default (focus)='onFocus($event)' placeholder='Choose a date'></ejs-datepicker>`
})
export class AppComponent {
    @ViewChild('default')
    public datepickerObj: CalendarComponent;

    onFocus(args: FocusEventArgs): void {
        this.datepickerObj.show();
    }
}

```

{% endtab %}
