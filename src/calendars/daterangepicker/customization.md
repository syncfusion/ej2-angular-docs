---
title: "Customization"
component: "DateRangePicker"
description: "Date range picker gives complete control to the user to customize overall appearance of the date range picker in their application."
---

# Customization

DateRangePicker makes available for the UI customization which can be achieved with properties, events that are available with this component.

## Day cell format

[`renderDayCell`](../api/daterangepicker/renderDayCellEventArgs#renderdaycelleventargs) is a
 event which provides the option to customize each day cell while rendering itself.
The following example disables the weekends of every month using `renderDayCell` event.

{% tab template="daterangepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-daterangepicker (renderDayCell)='disableDate($event)' placeholder='Select a range'></ejs-daterangepicker>`
})
export class AppComponent {
    constructor() {
    }
    disableDate(args): void {
         if (args.date.getDay() == 0 || args.date.getDay() == 6) {
        //sets isDisabled to true to disable the date.
        args.isDisabled = true;
    }
    }
}

```

{% endtab %}

## First day of week

Start day in a week will differ based on culture and it can be customized based on application needs.
For this customization, you can make use of `firstDayOfWeek` property.
By default, first day of week in en-US is Sunday.

In below example, first day of the week in the pop-up calendar is customized to Monday with help of the `firstDayOfWeek` property.

{% tab template="daterangepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['index.css'],
    template: `<ejs-daterangepicker [firstDayOfWeek]='startDay'  placeholder='Select a range'></ejs-daterangepicker>`
})
export class AppComponent {
    public startDay:Number = 1;
    constructor() {
    }
}

```

{% endtab %}

## Preset Ranges

DateRangePicker has an option to set the pre-defined ranges with label using `presets` property.
With help of this, we can set the frequently used ranges as preset ranges for quick selection in a DateRangePicker popup.
Here in following sample, you can choose the mostly using options from pre-defined ranges easily.

{% tab template="daterangepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['index.css'],
    template: `<ejs-daterangepicker placeholder='Select a range'>
            <e-presets>
                <e-preset label="This Week" [start]='weekStart' [end]='weekEnd'></e-preset>
                <e-preset label="This Month" [start]='monthStart' [end]='monthEnd'></e-preset>
                <e-preset label="Last Month" [start]='lastStart' [end]='lastEnd'></e-preset>
                <e-preset label="Last Year" [start]='yearStart' [end]='yearEnd'></e-preset>
            </e-presets>
        </ejs-daterangepicker>`
})
export class AppComponent {
public today: Date = new Date(new Date().toDateString());
    public weekStart: Date = new Date(new Date(new Date().setDate(new Date().getDate() - (new Date().getDay() + 7) % 7)).toDateString());
    public weekEnd: Date = new Date(new Date(new Date().setDate(new Date(new Date().setDate((new Date().getDate()
        - (new Date().getDay() + 7) % 7))).getDate() + 6)).toDateString())
        ;
    public monthStart: Date = new Date(new Date(new Date().setDate(1)).toDateString());
    public monthEnd: Date = this.today;
    public lastStart: Date = new Date(new Date(new Date(new Date().setMonth(new Date().getMonth() - 1)).setDate(1)).toDateString());
    public lastEnd: Date = this.today;
    public yearStart: Date = new Date(new Date(new Date().setDate(new Date().getDate() - 365)).toDateString());
    public yearEnd: Date = this.today;

    constructor() {
    }
}

```

{% endtab %}

## See Also

* [How to customize DateRangePicker using cssClass](./how-to/customization-using-cssclass)
* [How to disable DateRangePicker component](./how-to/disable-placeholder-readonly)
* [How to customize the DateRangePicker day header](./how-to/customize-the-daterangepicker-day-header)