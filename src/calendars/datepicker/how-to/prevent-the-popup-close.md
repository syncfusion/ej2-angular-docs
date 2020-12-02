---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Prevent the popup close

The following examples demonstrates how to prevent the popup from closing.

{% tab template="datepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { PreventableEventArgs } from '@syncfusion/ej2-angular-calendars';

@Component({
    selector: 'app-root',
    template: `<ejs-datepicker (close)='onClose($event)' placeholder='Enter date'></ejs-datepicker>`
})
export class AppComponent {
    onClose(args: PreventableEventArgs): void {
        args.preventDefault();
    }
}

```

{% endtab %}
