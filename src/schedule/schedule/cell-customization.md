---
title: "Customizing Scheduler Cells"
component: "Scheduler"
description: "This topic demonstrates how to customize the cells of Scheduler using template option, methods and events available in Scheduler."
---

# Customization

The cells of the Scheduler can be easily customized either using the cell template or `RenderCell` event.

## Setting cell dimensions in all views

The height and width of the Scheduler cells can be customized either to increase or reduce its size through the `cssClass` property, which overrides the default CSS applied on cells.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px"  sourceFiles="index.css" %}

```typescript
import { Component, ViewChild, ViewEncapsulation } from '@angular/core';
import { ScheduleComponent, EventSettingsModel, ActionEventArgs, DayService, WeekService, WorkWeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule #scheduleObj width='100%' height='550px' cssClass='schedule-cell-dimension' [selectedDate]="selectedDate" [eventSettings]="eventSettings"> </ejs-schedule>`,
  styles: [`
  .schedule-cell-dimension.e-schedule .e-vertical-view .e-date-header-wrap table col,
.schedule-cell-dimension.e-schedule .e-vertical-view .e-content-wrap table col {
    width: 200px;
}

.schedule-cell-dimension.e-schedule .e-vertical-view .e-time-cells-wrap table td,
.schedule-cell-dimension.e-schedule .e-vertical-view .e-work-cells {
    height: 100px;
}

.schedule-cell-dimension.e-schedule .e-month-view .e-work-cells,
.schedule-cell-dimension.e-schedule .e-month-view .e-date-header-wrap table col {
    width: 200px;
}

.schedule-cell-dimension.e-schedule .e-month-view .e-work-cells {
    height: 200px;
}
`],
encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild('scheduleObj', { static: true })
    public scheduleObj: ScheduleComponent;
    public selectedDate: Date = new Date(2018, 1, 15);
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Check for cell availability

You can check whether the given time range slots are available for event creation or already occupied by other events using the `isSlotAvailable` method. In the following code example, if a specific time slot already contains an appointment, then no more appointments can be added to that cell.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ScheduleComponent, EventSettingsModel, ActionEventArgs, DayService, WeekService, WorkWeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule #scheduleObj width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" (actionBegin)="onActionBegin($event)" >
   <e-views> <e-view option="Day"></e-view> <e-view option="Week"></e-view> <e-view option="WorkWeek"></e-view> <e-view option="Month"></e-view></e-views> </ejs-schedule>`,
   styles: [`
#container {
  visibility: hidden;
}

#loader {
  color: #008cff;
  height: 40px;
  width: 30%;
  position: absolute;
  top: 45%;
  left: 45%;
}

.templatewrap {
  text-align: center;
  width: 100%;
}

.templatewrap img {
  width: 20px;
  height: 20px;
}

/* csslint ignore:start */
.schedule-cell-dimension.e-schedule .e-vertical-view .e-date-header-wrap table col,
.schedule-cell-dimension.e-schedule .e-vertical-view .e-content-wrap table col {
    width: 200px;
}

.schedule-cell-dimension.e-schedule .e-vertical-view .e-time-cells-wrap table th,
.schedule-cell-dimension.e-schedule .e-vertical-view .e-work-cells {
    height: 100px;
}

.schedule-cell-dimension.e-schedule .e-month-view .e-work-cells,
.schedule-cell-dimension.e-schedule .e-month-view .e-date-header-wrap table col {
    width: 200px;
}

.schedule-cell-dimension.e-schedule .e-month-view .e-work-cells {
    height: 200px;
}
/* csslint ignore:end */
`],
})
export class AppComponent {
  @ViewChild('scheduleObj')
  public scheduleObj: ScheduleComponent;
  public selectedDate: Date = new Date(2018, 1, 15);
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
  public onActionBegin(args: ActionEventArgs): void {
    if (args.requestType === 'eventCreate' && (<Object[]>args.data).length > 0) {
    let eventData: { [key: string]: Object } = (<Object[]>args.data)[0] as { [key: string]: Object };
    let eventField: EventFieldsMapping = this.scheduleObj.eventFields;
    let startDate: Date = eventData[eventField.startTime] as Date;
    let endDate: Date = eventData[eventField.endTime] as Date;
    args.cancel = !this.scheduleObj.isSlotAvailable(startDate, endDate); }
  }
}
```

{% endtab %}

## Customizing cells in all the views

It is possible to customize the appearance of the cells using both template options and `renderCell` event on all the views.

### Using template

The `cellTemplate` option accepts the template string and is used to customize the cell background with specific images or appropriate text on the given date values.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { View, DayService, WeekService, TimelineViewsService, MonthService } from '@syncfusion/ej2-angular-schedule';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, TimelineViewsService, MonthService],
  // specifies the template string for the Schedule component
   template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [(currentView)]="currentView" cssClass="schedule-cell-template">
    <ng-template #cellTemplate let-data>
      <div class="templatewrap" *ngIf="data.type == 'workCells'" [innerHTML]="getWorkCellText(data.date)"></div>
      <div class="templatewrap" *ngIf="data.type == 'monthCells'" [innerHTML]="getMonthCellText(data.date)"></div>
    </ng-template>
  </ejs-schedule>`,
  styles: [`
  .schedule-cell-template.e-schedule .e-month-view .e-work-cells {
    position: relative;
  }
  .templatewrap {
  text-align: center;
  /* In MONTH view the cell template is a SIBLING of event templates. So which is necessary to set the parent position relative and the child position absolute with 100% width */
  position: absolute;
  width: 100%;
}

.templatewrap img {
  width: 20px;
  height: 20px;
}
`],
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public selectedDate: Date = new Date(2017, 11, 16);
    public currentView: View = 'Week';
    getMonthCellText(date: Date): string {
      if (date.getMonth() === 10 && date.getDate() === 23) {
        return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/birthday.svg" />';
      } else if (date.getMonth() === 11 && date.getDate() === 9) {
          return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/get-together.svg" />';
      } else if (date.getMonth() === 11 && date.getDate() === 13) {
          return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/birthday.svg" />';
      } else if (date.getMonth() === 11 && date.getDate() === 22) {
          return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/thanksgiving-day.svg" />';
      } else if (date.getMonth() === 11 && date.getDate() === 24) {
          return '<img src="https://ej2.syncfusion.com/demos/src/schedule/images/christmas-eve.svg" />';
      } else if (date.getMonth() === 11 && date.getDate() === 25) {
          return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/christmas.svg" />';
      } else if (date.getMonth() === 0 && date.getDate() === 1) {
          return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/newyear.svg" />';
      } else if (date.getMonth() === 0 && date.getDate() === 14) {
          return '<img src= "https://ej2.syncfusion.com/demos/src/schedule/images/birthday.svg" />';
      }
      return '';
    }
    getWorkCellText(date: Date): string {
        let weekEnds: number[] = [0, 6];
        if (weekEnds.indexOf(date.getDay()) >= 0) {
            return "<img src='https://ej2.syncfusion.com/demos/src/schedule/images/newyear.svg' />";
        }
        return '';
    }
 }
```

{% endtab %}

### Using renderCell event

An alternative to `cellTemplate` is the `renderCell` event, which can also be used to customize the cells with appropriate images or formatted text values.

{% tab template="schedule/default", sourceFiles="app/**/*.ts,app/index.css", iframeHeight="588px" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { EventSettingsModel, RenderCellEventArgs, DayService, WeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';
import { createElement } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' currentView='Month' [selectedDate]="selectedDate" [eventSettings]="eventSettings" (renderCell)="onRenderCell($event)">
  <e-views> <e-view option="Day"></e-view> <e-view option="Week"></e-view> <e-view option="Month"></e-view> </e-views> </ejs-schedule>`,
  styleUrls: ['app/index.css'],
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 14);
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
  onRenderCell(args: RenderCellEventArgs): void {
    if (args.elementType == 'workCells' || args.elementType == 'monthCells') {
      let weekEnds: number[] = [0, 6];
      if (weekEnds.indexOf((args.date).getDay()) >= 0) {
        let ele: HTMLElement = createElement('div', {
          innerHTML: "<img src='https://ej2.syncfusion.com/demos/src/schedule/images/newyear.svg' />",
          className: 'templatewrap'
        });
        (args.element).appendChild(ele);
      }
    }
  }
}
```

{% endtab %}

You can customize cells such as work cells, month cells, all-day cells, header cells, resource header cells using `renderCell` event by checking the `elementType` option within the event. You can check elementType with any of the following.

| Element type | Description |
|-------|---------|
| dateHeader | triggers on header cell rendering.|
| monthDay | triggers on header cell in month view rendering.|
| resourceHeader | triggers on resource header cell rendering.|
| alldayCells | triggers on all day cell rendering.|
| emptyCells | triggers on empty cell rendering on header bar.|
| resourceGroupCells | triggers on rendering of work cells for parent resource.|
| workCells | triggers on work cell rendering.|
| monthCells | triggers on month cell rendering.|
| majorSlot | triggers on major time slot cell rendering.|
| minorSlot | triggers on minor time slot cell rendering.|
| weekNumberCell | triggers on cell displaying week number.|

## Customizing cell header in month view

The month header of each date cell in the month view can be customized using the `cellHeaderTemplate` option which accepts the string or HTMLElement. The corresponding date can be accessed with the template.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { Internationalization } from '@syncfusion/ej2-base';
import { View, MonthService } from '@syncfusion/ej2-angular-schedule';

@Component({
  selector: 'app-root',
  providers: [MonthService],
  // specifies the template string for the Schedule component
   template: `<ejs-schedule width='100%' height='550px' cssClass="schedule-cell-header-template">
    <ng-template #cellHeaderTemplate let-data>
      <div class="date-text">{{getDateHeaderText(data.date)}}</div>
    </ng-template>
    <e-views>
      <e-view option='Month'></e-view>
    </e-views>
  </ejs-schedule>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  public instance: Internationalization = new Internationalization();
  getDateHeaderText: Function = (value: Date) => {
    return this.instance.formatDate(value, { skeleton: "Ed" });
  };
}
```

{% endtab %}

## Customizing the minimum and maximum date values

Providing the `minDate` and `maxDate` property with some date values, allows the Scheduler to set the minimum and maximum date range. The Scheduler date that lies beyond this minimum and maximum date range will be in a disabled state so that the date navigation will be blocked beyond the specified date range.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { DayService, WeekService, WorkWeekService, MonthService, AgendaService, View } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [minDate]='minDate' [maxDate]='maxDate' [currentView]='currentView' [eventSettings]='eventSettings'></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 17);
  public minDate: Date = new Date(2017, 4, 17);
  public maxDate: Date = new Date(2018, 8, 17);
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
  public currentView: View = 'Month';
}

```

{% endtab %}

>By default, the `minDate` property value is set to new Date(1900, 0, 1) and `maxDate` property value is set to new Date(2099, 11, 31). The user can also set the customized `minDate` and `maxDate` property values.

## How to disable multiple cell and row selection in Schedule

By default, the `allowMultiCellSelection` and `allowMultiRowSelection` properties of the Schedule are set to `true`. So, the Schedule allows user to select multiple cells and rows. If the user want to disable this multiple cell and row selection. The user can disable this feature by setting up `false` to these properties.