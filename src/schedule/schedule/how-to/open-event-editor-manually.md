# Open Editor Window Manually

## Open Editor Window externally

Schedule allows user to manually open the event editor on specific time or on certain events using `openEditor` method as shown below.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="616px" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { EventSettingsModel, ScheduleComponent, DayService, WeekService, WorkWeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<button ejs-button cssClass='e-info' (click)='editor()'> Click to open Editor </button>
  <button ejs-button cssClass='e-info' (click)='eventEditor()'> Click to open Event Editor </button>
  <ejs-schedule #scheduleObj width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" > <e-views> <e-view option="Week"></e-view> <e-view option="WorkWeek"></e-view> <e-view option="Month"></e-view> <e-view option="Day"></e-view> </e-views> </ejs-schedule>`
})
export class AppComponent {
    @ViewChild('scheduleObj')
    public scheduleObj: ScheduleComponent;
    public selectedDate: Date = new Date(2018, 1, 15);
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
    editor(): void {
    let cellData: Object = {
        startTime: new Date(2018, 1, 15, 10, 0),
        endTime: new Date(2018, 1, 15, 11, 0),
    };
    this.scheduleObj.openEditor(cellData,'Add');
    }
    eventEditor(): void {
    let eventData: Object ={
        Id: 4,
        Subject: 'Meteor Showers in 2018',
        StartTime: new Date(2018, 1, 14, 13, 0),
        EndTime: new Date(2018, 1, 14, 14, 30)
    };
    this.scheduleObj.openEditor(eventData,'Save');
    }
}
```

{% endtab %}

## Open editor window on single click

By default, Scheduler Editor window will open when double clicking the cells or appointments. You can also open the editor window with single click by using `openEditor` method in `eventClick` and `cellClick` events of scheduler and setting false to `showQuickInfo`. The following example shows how to open editor window on single click of cells and appointments.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="616px" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { EventSettingsModel, ScheduleComponent, DayService, WeekService, WorkWeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { schedulerData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule #scheduleObj width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" [showQuickInfo]="showQuickInfo" (cellClick)="onCellClick($event)" (eventClick)="onEventClick($event)" > <e-views> <e-view option="Week"></e-view> <e-view option="WorkWeek"></e-view> <e-view option="Month"></e-view> <e-view option="Day"></e-view> </e-views> </ejs-schedule>`
})
export class AppComponent {
    @ViewChild('scheduleObj')
    public scheduleObj: ScheduleComponent;
    public selectedDate: Date = new Date(2021, 7, 15);
    public eventSettings: EventSettingsModel = { dataSource: schedulerData };
    public showQuickInfo: Boolean = false;
    onCellClick(args: CellClickEventArgs): void {
        this.scheduleObj.openEditor(args, 'Add');
    }
    onEventClick(args: EventClickArgs): void {
        if (!(args.event as any).RecurrenceRule) {
        this.scheduleObj.openEditor(args.event, 'Save');
        }
        else {
        this.scheduleObj.quickPopup.openRecurrenceAlert();
        }
    }
}
```

{% endtab %}
