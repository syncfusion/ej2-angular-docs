---
title: "Date Formats"
component: "DatePicker"
description: "Date picker supports to format date object into specific string format to simplify the date representation. It adapts to any culture specific date formats when it is globalized."
---

# Date Format

Date format is a way of representing the date value in different string format in textbox.

By default the DatePicker's format is based on the culture. You can also set the own
custom format by using the
[`format`](../api/datepicker#format)
property.

>Once the date format property has been defined it will be common to all the cultures.

To know more about the date format standards, refer to the
[Internationalization Date Format](http://ej2.syncfusion.com/documentation/base/internationalization#date-formatter-and-parser) section.

The following example demonstrates the DatePicker with the custom format (`yyyy-MM-dd`).

{% tab template="datepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-datepicker format='yyyy-MM-dd' placeholder='Enter date'
    [value]=dateValue></ejs-datepicker>`
})
export class AppComponent {
    public dateValue: Date = new Date("05/17/2017");
    constructor() {
    }
}

```

{% endtab %}