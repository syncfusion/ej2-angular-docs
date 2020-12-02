---
title: "Height and Width of Scheduler"
component: "Scheduler"
description: "This article demonstrates how to set the height and width of Scheduler in pixels, percentage or auto values."
---

# Scheduler dimensions

The Scheduler dimensions refers to both height and width of the entire layout and it accepts 3 types of values.

* auto
* pixel
* percentage

## Auto Height and Width

When height and width of the Scheduler are set to `auto`, it will try as hard as possible to keep an element the same width as its parent container. In other words, the parent container that holds Scheduler, it's width/height will be the sum of its children. By default, Scheduler is assigned with `auto` values for both height and width properties.

{% tab template="schedule/dimension", sourceFiles="app/**/*.ts", iframeHeight="1875px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData} from './datasource.ts';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='auto' height='auto' [selectedDate]='selectedDate' [eventSettings]='eventSettings'></ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
 }
```

{% endtab %}

## Height and Width in pixel

The Scheduler height and width will be rendered exactly as per the given pixel values. It accepts both string and number values.

{% tab template="schedule/dimension", sourceFiles="app/**/*.ts", iframeHeight="605px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, WeekService, WorkWeekService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData} from './datasource.ts';

@Component({
  selector: 'app-root',
  providers: [WeekService, WorkWeekService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='650px' height='550px' [selectedDate]='selectedDate' [eventSettings]='eventSettings'></ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
 }
```

{% endtab %}

## Height and Width in percentage

When height and width of the Scheduler are given as percentage, it will make the Scheduler as wide as the parent container.

{% tab template="schedule/dimension", sourceFiles="app/**/*.ts", iframeHeight="1875px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, WeekService, WorkWeekService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData} from './datasource.ts';

@Component({
  selector: 'app-root',
  providers: [WeekService, WorkWeekService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='100%' [selectedDate]='selectedDate' [eventSettings]='eventSettings'></ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public eventSettings: EventSettingsModel = {
        dataSource: scheduleData
    };
 }
```

{% endtab %}

## See Also

* [How to Change Scheduler Cell Dimensions](./cell-customization/#setting-cell-dimensions-in-all-views)