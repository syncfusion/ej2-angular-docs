---
title: "Scheduler Views"
component: "Scheduler"
description: "This article demonstrates the types of views available in Scheduler, and explains the way to customize and configure each view with different options."
---

# Views

The Scheduler includes wide variety of view modes with unique configuration options for each view. The available view modes are Day, Week, Work Week, Month, Year, Agenda, Month Agenda, Timeline Day, Timeline Week, Timeline Work Week and Timeline Month, Timeline Year, out of which the `Week` view is set as active.

To navigate between different views and dates, the navigation options are available at the Scheduler header bar. The active view option is usually highlighted by default. The date range of the active view will also be displayed at the left corner of the header bar, clicking on which will open a calendar popup for the ease of desired date selection.

Learn how to customize each individual view of Angular Scheduler with different settings by watching this video:

`youtube:FRwDcpJLWOo`

> By default, Scheduler displays the calendar views such as day, week, work week, month and agenda.

## Setting specific view on scheduler

As the Scheduler displays `week` view by default, therefore to change the active view, set `currentView` property with the desired view name. The applicable view names that the Scheduler accepts are as follows,

* Day
* Week
* WorkWeek
* Month
* Year
* Agenda
* MonthAgenda
* TimelineDay
* TimelineWeek
* TimelineWorkWeek
* TimelineMonth
* TimelineYear

It is necessary to import and inject the appropriate view modules into the application to make use of these view modes on the Scheduler. Also, it is possible to display only the desired views on the Scheduler. To define and configure specific views, use the [`views`](../api/schedule/views) property.

In the following example, the Scheduler displays 4 views namely, Week, Month, TimelineWeek and Timeline Month. The appropriate view modules are imported and injected properly to display those views on the Scheduler.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, WeekService, TimelineViewsService, MonthService, TimelineMonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [WeekService, TimelineViewsService, MonthService, TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='TimelineDay'></e-view>
        <e-view option='Week'></e-view>
        <e-view option='Month'></e-view>
        <e-view option='TimelineMonth'></e-view>
      </e-views>
  </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

To configure Scheduler with simply 2 views, but with different configurations on each view, refer the following code example. Here, the Week view displays the dates in `dd-MM-yyyy` format whereas the Month view hides the weekend days and also displays it in readonly mode.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, WeekService, MonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [WeekService, MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='Week' dateFormat='dd-MMM-yyyy'></e-view>
        <e-view option='Month' [showWeekend]="showWeekend" [readonly]="isReadOnly"></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public showWeekend: Boolean = true;
    public isReadOnly: number = 3;
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

## View specific configuration

There are scenarios where each view may need to have different configurations. For such cases, you can define the applicable scheduler properties within the `views` Property for each view option as depicted in the following examples. The fields available to be used within each view options are as follows.

| Property | Type | Description | Applicable views |
|----------|------|-------------|------------------|
| `option` | View | It accepts the Scheduler view name, based on which we can define its related properties. The view names can be `Day`, `Week` and so on. | All views.|
| `isSelected` | Boolean | It acts similar to the `currentView` property and defines the active view of the Scheduler.| All views. |
| `dateFormat` | Date | By default, Scheduler follows the date format as per the default culture assigned to it. When it is defined under specific view, only those assigned views follows this date format. | All views. |
| `readonly` | Boolean | When set to `true`, prevents the CRUD actions on the respective view under where it is defined. | All views. |
| `resourceHeaderTemplate` | String | The template option which is used to customize the resource header cells on the Scheduler. It gets applied only on the views, wherever it is defined.| All views. |
| `dateHeaderTemplate` | String | The template option which is used to customize the date header cells and is applied only on the views, wherever it is defined. | All views. |
| `eventTemplate` | String | The template option to customize the events background. It will get applied to the events of the view to which it is currently being defined. | All views. |
| `showWeekend` | Boolean | When set to `false`, it hides the weekend days of a week from the views on which it is defined.| All views. |
| `group` | [GroupModel](../api/schedule/groupModel) | Allows to set different resource grouping options on all available Scheduler view modes. | All views. |
| `cellTemplate` | String | The template option to customize the work cells of the Scheduler and is applied only on the views, on which it is defined. | Applicable on all views except Agenda view. |
| `workDays` | Number[] | It is used to set the working days on the Scheduler views. | Applicable on all views except Agenda view. |
| `displayName` | String | When a particular view is customized to display with different intervals, this property allows the user to set different display name for each of the views. | Applicable on all views except Agenda and Month Agenda. |
| `interval` | Number | It allows to customize the default Scheduler views with different set of days, weeks, work weeks or months on the applicable view type. | Applicable on all views except Agenda and Month Agenda. |
| `startHour` | String | It is used to specify the start hour, from which the Scheduler should be displayed. It accepts the time string in a short skeleton format and also, hides the time beyond the specified start time. | Applicable on Day, Week, Work Week, Timeline Day, Timeline Week and Timeline Work Week views. |
| `endHour` | String | It is used to specify the end hour, at which the Scheduler ends. It accepts the time string in a short skeleton format. | Applicable on Day, Week, Work Week, Timeline Day, Timeline Week, and Timeline Work Week views. |
| `timeScale` | [TimeScaleModel](../api/schedule/timeScaleModel) | Allows to set different timescale configuration on each applicable view modes. | Applicable on Day, Week, Work Week, Timeline Day, Timeline Week, and Timeline Work Week views. |
| `showWeekNumber` | Boolean | When set to `true`, shows the week number on the respective weeks.| Applicable on Day, Week, Work Week, and Month views. |
| `allowVirtualScrolling` | Boolean | It is used to enable or disable the virtual scrolling functionality. | Applicable on Agenda and Timeline views. |
| `headerRows` | [HeaderRowsModel](../api/schedule/headerRowsModel) | Allows defining the custom header rows on timeline views of the Scheduler to display the year, month, week, date and hour label as an individual row. | Applicable only on all timeline views. |

### Day view

Usually a day view displays a single day with all its related appointments. It is possible to customize the day view to display more number of days by extending the `views` property with `interval` option. You can also define any of the above defined properties within the `views` object definition as depicted in the following code example.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, TimeScaleModel } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' currentView="Day" [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='Day' startHour='09:30' endHour='18:00' [timeScale]="timeScaleOptions"></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public timeScaleOptions: TimeScaleModel = { enable: true, slotCount: 5 };
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

> All the above defined properties can be accessed within Day view except `allowVirtualScrolling` and `headerRows`.

### Week view

The Week view displays a count of 7 days (from Sunday to Saturday) with all its related appointments. The first day of the week can be changed using the `firstDayOfWeek` which accepts the integer (Sunday=0, Monday=1, Tuesday=2 and so on) value. You can navigate to a particular date in day view from the week view by clicking on the appropriate dates on the date header bar.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService, TimeScaleModel } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' currentView="Week" [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='Day' [interval]="viewInterval" displayName='2 Days' startHour='09:30' endHour='18:00' [timeScale]="timeScaleOptions"></e-view>
        <e-view option='Week' [interval]="viewInterval" displayName='2 Weeks' [showWeekend]="showWeekend" [isSelected]="isSelected"></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public viewInterval: number= 2;
    public showWeekend: boolean = false;
    public isSelected: boolean = true;
    public timeScaleOptions: TimeScaleModel = { enable: true, slotCount: 5 };
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

> All the above defined properties in the table can be accessed within Week and Work week views except `allowVirtualScrolling` and `headerRows`.

### Work Week view

The Work week view displays only the working days of a week (count of 5 days) and its associated appointments. It is possible to customize the working days on the work week view by using the `workDays` property which accepts an array of integer values (such as Sunday=0, Monday=1, Tuesday=2 and so on). By default, it displays from Monday to Friday (5 days). You can also navigate to a particular date in the day view from the work week view by clicking on the appropriate dates in the date header bar.

The following code example depicts how to change the working days only on the `Work Week` view of the Scheduler.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, WorkWeekService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [WorkWeekService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='WorkWeek' [workDays]="workWeekDays"></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public workWeekDays: number[]= [2, 3, 5];
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

> The Week, Work week and Day views can display the all-day row appointments in a separate all-day row with an expand/collapse option to view it.

### Month view

A Month view displays the entire days of a particular month and all its related appointments. You can navigate to a particular date in the day view by clicking on the appropriate date text on the month cells.

By default, when you try to create an appointment through Month view, it is considered as created for an entire day. You can explicitly change this behavior by unchecking the `All-day` option from editor window, so that it defaults to the start time duration as 9.00 AM and end time as 9.30 AM.

You can also have the `+ more` text indicator on each day cell of a Month view, clicking on which will allows you to view the hidden appointments of a day.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, MonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='Month' [showWeekNumber]="showWeekNumber" [readonly]="isReadOnly"></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public showWeekNumber: boolean = true;
    public isReadOnly: boolean = true;
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

### Year view

A Year view displays all the days of a particular year with months and all its related appointments. You can navigate to a particular date in the day view by clicking on the appropriate date text on the year cells.

Year view is available in both the `Horizontal` and `Vertical` orientations. You can manage the orientation of year view through `views` property.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, YearService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [YearService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='Year' [showWeekNumber]="showWeekNumber" [readonly]="isReadOnly"></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public showWeekNumber: boolean = true;
    public isReadOnly: boolean = true;
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

> The year view also has module support. In that, you can get all the months of a particular year in a calendar view format. In that calendar view, appointment contained dates are highlighted with dots placed under the individual date. When you click on the date, the event popup will be displayed and the events will be listed.

### Agenda view

The Agenda view lists out the appointments in a grid-like view for the next 7 days by default from the current date. The count of the days can be changed using the API `agendaDaysCount`. It allows virtual scrolling of dates by enabling the `allowVirtualScrolling` property. Also, you can enable or disable the display of days on Scheduler that has no appointments by setting true or false to the `hideEmptyAgendaDays` property.

The following code example depicts how to customize the display of events within Agenda view alone.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { Internationalization } from '@syncfusion/ej2-base';
import { EventSettingsModel, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='Agenda' [allowVirtualScrolling]="allowVirtualScroll">
        <ng-template #eventTemplate let-data>
          <div class="template-wrap">
            <div class="subject">{{data.Subject}}</div>
            <div class="time">{{getTimeString(data.StartTime)}} - {{getTimeString(data.EndTime)}}</div>
          </div>
        </ng-template>
        </e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
  public allowVirtualScroll: boolean = true;
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
  private instance: Internationalization = new Internationalization();
  getTimeString(value: Date): string {
    return this.instance.formatDate(value, { skeleton: 'hm' });
  };
}
```

{% endtab %}

### Month Agenda view

A Month-Agenda view shows a month calendar, where clicking on a particular day will display the appointments present on that date below the calendar. The day with appointments are differentiated with a circular dot below the date of the calendar.

The following code example shows how to hide the weekend days on `MonthAgenda` view as well as the working days list is modified on Month Agenda view alone.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, MonthAgendaService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [MonthAgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='MonthAgenda' [showWeekend]="showWeekend" [workDays]="workDays"></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 14);
    public showWeekend: boolean = false;
    public workDays: number[] = [1, 2, 3];
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

### Timeline views – Day, Week, Work Week

Similar to the day view, it shows a single day with all its appointments where the time slots are displayed horizontally. By default, the cell height adjusts as per the height set to Scheduler. When the number of appointments exceeds the visible area of the cells, the `+ more` text indicator will be displayed at the bottom to denote the presence of few more appointments in that time range.

To make use of the timeline views (Timeline Day, Timeline Week and Timeline Work Week) on Scheduler, import and inject the module `TimelineViews` from the `ej2-schedule` package.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineViewsService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineViewsService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='TimelineDay' startHour='10:00' endHour='15:30'></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

Similar to the Week view, the timeline week view shows 7 days with its associated appointments with the time slots displayed horizontally.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineViewsService, TimeScaleModel } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineViewsService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='TimelineWeek' timeScale="timeScaleOptions"></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public timeScaleOptions: TimeScaleModel = { enable: false };
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

The following code example depicts how to display the timeline work week view on Scheduler,

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineViewsService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineViewsService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='TimelineWorkWeek' dateFormat='dd-MMM-yyyy' [interval]="viewInterval" [workDays]="workweekDays"></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 14);
    public viewInterval: number = 3;
    public workweekDays: number[] = [1, 3, 5];
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

> Clicking on the dates in the date header bar of Timeline day, Timeline week and Timeline work week will allow you to navigate to the Agenda view.

### Timeline Month view

A Timeline Month view displays the current month days along with its appointments. To make use of the timeline Month view on Scheduler, import and inject `TimelineMonth` module from the `ej2-schedule` package.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineMonthService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='TimelineMonth' dateFormat='dd-MMM-yyyy' [showWeekend]="showWeekend"></e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public showWeekend: boolean = false;
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

> Clicking on the dates in the date header bar of Timeline month will allow you to navigate to the Timeline day view.

### Timeline Year view

In Timeline Year view, each row depicts a single resource. Whereas in the vertical view, each resource is grouped parallelly as columns. Here, the resource grouping follows the tree-view like hierarchical grouping structure and can contain any level of child resources.

To make use of the timeline Year view on Scheduler, import and inject `TimelineYear` module from the `ej2-schedule` package.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineYearService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineYearService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
      <e-views>
        <e-view option='TimelineYear' displayName: 'Horizontal Timeline Year', isSelected: true><e-view>
      </e-views>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

#### Resource grouping

The following code example depicts how to group the multiple resources on Timeline Year view and its relevant events are displayed accordingly under those resources.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineYearService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineYearService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings">
      <e-views>
        <e-view option='TimelineYear' displayName: 'Horizontal Timeline Year', isSelected: true><e-view>
          <e-view option='TimelineYear' displayName: 'Vertical Timeline Year', orientation: 'Vertical'><e-view>
      </e-views>
      <e-resources>
        <e-resource field="OwnerId" title="Owner" name="Owners"
          [dataSource]="ownerDataSource" [allowMultiple]="allowMultipleOwner"
          textField="OwnerText" idField="Id" colorField="OwnerColor">
        </e-resource>
      </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 3, 1);
    public views: Array<string> = ['TimelineYear'];
    public eventSettings: EventSettingsModel = {
        dataSource: resourceData
    };
    public allowMultipleOwner: Boolean = true;
    public ownerDataSource: Object[] = [
        { OwnerText: 'Nancy', Id: 1, OwnerColor: '#ffaa00' },
        { OwnerText: 'Steven', Id: 2, OwnerColor: '#f8a398' },
        { OwnerText: 'Michael', Id: 3, OwnerColor: '#7499e1' }
    ];
}
```

{% endtab %}

#### Auto row height

Timeline Year view supports Auto row height. When the feature `rowAutoHeight` is enabled, the row height gets auto-adjusted based on the number of overlapping events occupied in the same time range. If you disable the Auto row height, you have the `+ more` text indicator on each day cell of a Timeline Year view, clicking on which will allow you to view the hidden appointments of a day.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineYearService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineYearService],
  template: `<ejs-schedule width='100%' height='550px' [selectedDate]='selectedDate' [eventSettings]='eventSettings'>
  <e-views>
        <e-view option='TimelineYear' displayName: 'Horizontal Timeline Year', isSelected: true><e-view>
        <e-view option='TimelineYear' displayName: 'Vertical Timeline Year', orientation: 'Vertical'><e-view>
  </e-views>
  </ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 5, 17);
  public rowAutoHeight: boolean = true;
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

## Extending view intervals

It is possible to customize the display of default number of days on different Scheduler view modes. For example, a day view can be extended to display 3 days by setting the `interval` option as 3 for the `Day` option within the `views` property as depicted in the following code example. In the same way, you can also display 2 weeks by setting interval 2 for the `Week` option.

You can provide the alternative display name for such customized views on the Scheduler header bar, by setting the appropriate `displayName` property.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, DayService, WeekService } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [DayService, WeekService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' currentView="Day" [selectedDate]="selectedDate" [eventSettings]="eventSettings" >
  <e-views>
        <e-view displayName='3 Days' option='Day' [interval]="dayInterval"></e-view>
        <e-view displayName='2 Weeks' option='Week' [isSelected]="isSelected" [interval]="weekInterval"></e-view>
  </e-views> </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 1, 15);
    public isSelected: Boolean = true;
    public dayInterval: number = 3;
    public weekInterval: number = 2;
    public eventSettings: EventSettingsModel = { dataSource: scheduleData };
}
```

{% endtab %}

> The view intervals can be extended on all the Scheduler view modes except Agenda and Month-Agenda views.

## See Also

* [How to restrict view navigation while clicking on dates](./how-to/prevent-date-navigation)
