---
title: "Auto row height in Angular Scheduler"
component: "Scheduler"
description: "This section shows the way to auto-adjust the height of the work-cells of Scheduler based on the number of appointments present in those time ranges."
---

# Auto Row Height

By default, the height of the Scheduler rows in Timeline views are static and therefore, when the same time range holds multiple overlapping appointments, a `+n more` text indicator will be displayed. With this feature enabled, you can now view all the overlapping appointments present in those specific time range by auto-adjusting the row height based on the presence of the appointments count, instead of displaying the `+n more` text indicators.

To enable auto row height adjustments on Scheduler Timeline views and Month view, set `true` to the `rowAutoHeight` property whose default value is `false`.

> This auto row height adjustment is applicable only on all the Timeline views as well as on the calendar Month view.

Now, let's see how it works on those applicable views with examples.

## Calendar month view

By default, the rows of the calendar Month view can hold only the limited appointments count based on its row height, and the rest of the overlapping appointments are indicated with a `+n more` text indicator. The following example shows how the month view row auto-adjusts based on the number of appointments count, when this `RowAutoHeight` feature is enabled.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, MonthService, View } from '@syncfusion/ej2-angular-schedule';
import { scheduleData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [MonthService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [views]="scheduleViews" [rowAutoHeight]="rowAutoHeight" [selectedDate]="selectedDate" [eventSettings]="eventSettings" [currentView]="currentView">
  <e-views><e-view option='Month' ></e-view></e-views></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
  public scheduleViews: View[] = ['Month'];
  public rowAutoHeight: boolean = true;
  public currentView: View = 'Month';
  public eventSettings: EventSettingsModel = { dataSource: scheduleData };
 }
```

{% endtab %}

## Timeline views

When the feature `RowAutoHeight` is enabled in Timeline views, the row height gets auto-adjusted based on the number of overlapping events occupied on the same time range, which is demonstrated in the following example.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { EventSettingsModel, TimelineViewsService, TimelineMonthService, AgendaService, View } from '@syncfusion/ej2-angular-schedule';
import { eventData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineViewsService, TimelineMonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [views]="scheduleViews" [selectedDate]="selectedDate" [eventSettings]="eventSettings" [rowAutoHeight]="rowAutoHeight" [currentView]="currentView">
  <e-views> <e-view option='TimelineDay'></e-view>
            <e-view option='TimelineWeek'></e-view>
            <e-view option='TimelineWorkWeek'></e-view>
            <e-view option='TimelineMonth'></e-view>
            <e-view option='Agenda'></e-view>
  </e-views></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 1, 15);
  public rowAutoHeight: boolean = true;
  public scheduleViews: View[] = ['TimelineWeek'];
  public currentView: View = 'TimelineWeek';
  public eventSettings: EventSettingsModel = { dataSource: eventData };
 }
```

{% endtab %}

## Timeline views with multiple resources

The following example shows how the auto row adjustment feature works on timeline views with multiple resources.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { ScheduleComponent, EventSettingsModel, TimelineViewsService, DragAndDropService, GroupModel, ResizeService, View, TimelineMonthService, AgendaService } from '@syncfusion/ej2-angular-schedule';
import { roomData } from './datasource';

@Component({
  selector: 'app-root',
  providers: [TimelineViewsService, ResizeService, DragAndDropService, TimelineMonthService, AgendaService],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width='100%' height='550px' [views]="scheduleViews" [selectedDate]="selectedDate" [eventSettings]="eventSettings"  [group]="group" [currentView]="currentView" [rowAutoHeight]="rowAutoHeight">
  <e-resources><e-resource field='RoomId' title='Room Type' [dataSource]='resourceDataSource' [allowMultiple]='allowMultiple' name='MeetingRoom' textField='text' idField='id' colorField='color'></e-resource>
  <e-views> <e-view option='TimelineDay'></e-view>
            <e-view option='TimelineWeek'></e-view>
            <e-view option='TimelineWorkWeek'></e-view>
            <e-view option='TimelineMonth'></e-view>
            <e-view option='Agenda'></e-view></e-views></e-resources></ejs-schedule>`
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 7, 1);
  public rowAutoHeight: boolean = true;
  public scheduleViews: View[] = ['TimelineWeek'];
  public currentView: View = 'TimelineWeek';
  public group: GroupModel = {
    enableCompactView: false,
    resources: ['MeetingRoom']
  };
  public allowMultiple: Boolean = true;
  public resourceDataSource: Object[] = [
    { text: 'Room A', id: 1, color: '#98AFC7' },
    { text: 'Room B', id: 2, color: '#99c68e' },
    { text: 'Room C', id: 3, color: '#C2B280' },
    { text: 'Room D', id: 4, color: '#3090C7' },
    { text: 'Room E', id: 5, color: '#95b9' },
    { text: 'Room F', id: 6, color: '#95b9c7' },
    { text: 'Room G', id: 7, color: '#deb887' },
    { text: 'Room H', id: 8, color: '#3090C7' },
    { text: 'Room I', id: 9, color: '#98AFC7' },
    { text: 'Room J', id: 10, color: '#778899' }
  ];
  
  public eventSettings: EventSettingsModel = {
    dataSource: roomData,
    fields: {
      id: 'Id',
      subject: { name: 'Subject', title: 'Summary' },
      location: { name: 'Location', title: 'Location' },
      description: { name: 'Description', title: 'Comments' },
      startTime: { name: 'StartTime', title: 'From' },
      endTime: { name: 'EndTime', title: 'To' }
    }
  };

 }
```

{% endtab %}

## Appointments occupying entire cell

By default, with the feature `rowAutoHeight`, there will be a space in the bottom of the cell when appointment is rendered. To avoid this space, we can set true to the property `ignoreWhitespace` with in `eventSettings` whereas its default property value is false. In the following code example, the whitespace below the appointments has been ignored.

{% tab template="schedule/ignore-whitespace", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import {
    TimelineViewsService, TimelineMonthService, EventSettingsModel, GroupModel
} from '@syncfusion/ej2-angular-schedule';
import { resourceData } from './datasource.ts';

@Component({
    selector: "app-root",
    providers: [TimelineViewsService, TimelineMonthService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [currentView]='currentView' [rowAutoHeight]="rowAutoHeight" [eventSettings]="eventSettings" [group]='group'>
      <e-resources>
        <e-resource field="RoomId" title="Room" name="Rooms"
            [dataSource]="roomDataSource"
            textField="RoomText" idField="Id" colorField="RoomColor">
        </e-resource>
        <e-resource field="OwnerId" title="Owner" name="Owners"
          [dataSource]="ownerDataSource" [allowMultiple]="allowMultipleCategory"
          textField='OwnerText' idField='Id' groupIDField='OwnerGroupId' colorField='OwnerColor'>
        </e-resource>
      </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2021, 7, 4);
    public currentView: string = 'TimelineWeek';
    public rowAutoHeight: boolean = true;
    public views: Array<string> = ['TimelineWeek', 'TimelineMonth'];
    public eventSettings: EventSettingsModel = {
        dataSource: resourceData,
        ignoreWhitespace: true

    };
    public group: GroupModel = {
        resources: ['Rooms', 'Owners']
    };
    public roomDataSource: Object[] = [
        { RoomText: 'ROOM 1', Id: 1, RoomColor: '#cb6bb2' },
        { RoomText: 'ROOM 2', Id: 2, RoomColor: '#56ca85' }
    ];
    public allowMultipleOwner: Boolean = true;
    public ownerDataSource: Object[] = [
        { OwnerText: 'Nancy', Id: 1, OwnerGroupId: 1, OwnerColor: '#ffaa00' },
        { OwnerText: 'Steven', Id: 2, OwnerGroupId: 2, OwnerColor: '#f8a398' },
        { OwnerText: 'Michael', Id: 3, OwnerGroupId: 1, OwnerColor: '#7499e1' }
    ];
}
```

{% endtab %}

**Note**: The property `ignoreWhitespace` will be applicable only when `rowAutoHeight` feature is enabled in the Scheduler

> You can refer to our [Angular Scheduler](https://www.syncfusion.com/angular-ui-components/angular-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [Angular Scheduler example](https://ej2.syncfusion.com/angular/demos/#/material/schedule/overview) to knows how to present and manipulate data.
