# Show tooltip with delay

In default, the Schedule tooltip is showed without any delay. We can set up the delay to the Schedule tooltip with the help of the Tooltip `openDelay` property.

The preview demonstrates setting up the delay to the Schedule tooltip. You can check the Schedule tooltip with delay here.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="616px" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { EventSettingsModel, ScheduleComponent, DayService, WeekService, WorkWeekService, MonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService, WorkWeekService, MonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule #scheduleObj width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" (created)="onCreated($event)">
</ejs-schedule>`
})

export class AppComponent {
  @ViewChild('scheduleObj') public scheduleObj: ScheduleComponent;
  public selectedDate: Date = new Date(2018, 1, 15);
  public eventSettings: EventSettingsModel = { dataSource: scheduleData, enableTooltip: true };

  public onCreated(): void {
    // Assigning the tooltip object to the tooltipObj variable.
    let tooltipObj = this.scheduleObj.element.ej2_instances[2];
    // Disable the tooltip to follow the mouse pointer position
    tooltipObj.mouseTrail = false;
    // Setting tooltip open delay
    tooltipObj.openDelay = 1000;
    // Setting the position to the tooltip
    tooltipObj.position = "TopCenter";
  }
}
```

{% endtab %}