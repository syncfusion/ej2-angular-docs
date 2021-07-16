---
title: "Multiple Resources and Grouping | Angular Scheduler"
component: "Scheduler"
description: "This article demonstrates how to assign a single or multiple resources to events and also shows how to group them in both hierarchical and vertical mode."
---

# Multiple resources and grouping

Resources and grouping support allows the Scheduler to be shared by multiple resources. Also, the appointments of each resources are displayed under relevant resources. Each resource in the Scheduler is arranged in a column/row wise order, with individual spacing to display all its respective appointments on a single page. It also supports the multiple levels of grouping of resources, thus enabling the categorization of resources in a hierarchical structure and shows it either in expandable groups (Timeline views) or else vertical hierarchy one after the other (Calendar views).

It is also possible to assign one or more resources to the same appointment, by allowing multiple selection of resource options available in the event editor window.

The HTML5 JavaScript Scheduler groups the resources based on different criteria. It includes grouping appointments based on resources, grouping resources based on dates, and timeline scheduling. Also, the data for resources bind with Scheduler either as a local JSON collection or URL, retrieving data from remote data services.

Learn how to add appointments of multiple resources to the Angular Scheduler from this video:

`youtube:K_fCX-zHVJQ`

## Resource fields

The default options available within the `resources` collection are as follows,

| Field name | Type | Description |
|-------|---------| --------------- |
| `field` | String | A value that binds to the resource field of event object. |
| `title` | String | It holds the title of the resource field to be displayed on the event editor window. |
| `name` | String | A unique resource name used for differentiating various resource objects while grouping. |
| `allowMultiple` | Boolean | When set to `true`, allows multiple selection of resource names, thus creating multiple instances of same appointment for the selected resources. |
| `dataSource` | Object | Assigns the resource `dataSource`, where data can be passed either as an array of JavaScript objects, or else can create an instance of [`DataManager`](http://ej2.syncfusion.com/documentation/data/api-dataManager.html) in case of processing remote data and can be assigned to the `dataSource` property. With the remote data assigned to `dataSource`, check the available [adaptors](http://ej2.syncfusion.com/documentation/data/adaptors.html) to customize the data processing. |
| `query` | Query | Defines the external [`query`](http://ej2.syncfusion.com/documentation/data/api-query.html) that will be executed along with the data processing. |
| `idField` | String | Binds the resource ID field name from the resources `dataSource`. |
| `textField` | String | Binds the text field name from the resources `dataSource`. It usually holds the resource names. |
| `groupIDField` | String | Binds the group ID field name from the resource `dataSource`. It usually holds the value of resource IDs of parent level resources. |
| `colorField` | String | Binds the color field name from the resource `dataSource`. The color value mapped in this field will be applied to the events of resources. |
| `startHourField` | String | Binds the start hour field name from the resource `dataSource`. It allows to provide different work start hour for the resources. |
| `endHourField` | String | Binds the end hour field name from the resource `dataSource`. It allows to provide different work end hour for the resources. |
| `workDaysField` | String | Binds the work days field name from the resources `dataSource`. It allows to provide different working days collection for the resources. |
| `cssClassField` | String | Binds the custom CSS class field name from the resources `dataSource`. It maps the CSS class written for the specific resources and applies it to the events of those resources. |

## Resource data binding

The data for resources can bind with Scheduler either as a local JSON collection or a service URL, retrieving resource data from remote data services.

### Using local JSON data

The following code example depicts how to bind the local JSON data to the `dataSource` of `resources` collection.

```typescript
import { Component } from '@angular/core';
import {
    WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService, EventSettingsModel
} from '@syncfusion/ej2-angular-schedule';
import { resourceData } from './datasource.ts';

@Component({
    selector: "app-root",
    providers: [WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings">
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
    public views: Array<string> = ['Week', 'Month', 'TimelineWeek', 'TimelineMonth', 'Agenda'];
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

### Using remote service URL

The following code example depicts how to bind the remote data for resources `dataSource`.

```typescript
import { Component } from '@angular/core';
import {
    WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService, EventSettingsModel
} from '@syncfusion/ej2-angular-schedule';
import { resourceData } from './datasource.ts';
import { DataManager, UrlAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: "app-root",
    providers: [WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings">
      <e-resources>
        <e-resource field="OwnerId" title="Owner" name="Owners"
          [dataSource]="resourceDataManager" [allowMultiple]="allowMultipleOwner"
          textField="OwnerText" idField="Id" colorField="OwnerColor">
        </e-resource>
      </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 3, 1);
    public views: Array<string> = ['Week', 'Month', 'TimelineWeek', 'TimelineMonth', 'Agenda'];
    public resourceDataManager: DataManager = new DataManager({
        url: 'Home/GetResourceData',
        adaptor: new UrlAdaptor,
        crossDomain: true
    });
    public eventSettings: EventSettingsModel = {
        dataSource: resourceData
    };
    public allowMultipleOwner: Boolean = true;
}
```

## Scheduler with multiple resources

It is possible to display the Scheduler in default mode without visually showcasing all the resources in it, but allowing to assign the required resources to the appointments through the event editor resource options.

The appointments belonging to the different resources will be displayed altogether on the default Scheduler, which will be differentiated based on the resource color assigned in the **resources** (depicting to which resource that particular appointment belongs) collection.

**Example:** To display default Scheduler with multiple resource options in the event editor, ignore the group option and simply define the `resources` property with all its internal options.

{% tab template="schedule/multiple-resource", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import {
    WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService, EventSettingsModel
} from '@syncfusion/ej2-angular-schedule';
import { resourceData } from './datasource.ts';

@Component({
    selector: "app-root",
    providers: [WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings">
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
    public views: Array<string> = ['Week', 'Month', 'TimelineWeek', 'TimelineMonth', 'Agenda'];
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

> Setting `allowMultiple` to `true` in the above code example allows you to select multiple resources from the event editor and also creates multiple copies of the same appointment in the Scheduler for each resources while rendering.

## Resource grouping

Resource grouping support allows the Scheduler to group the resources in a hierarchical structure both as an expandable groups (Timeline views) and as vertical hierarchy displaying resources one after the other (Resources view).

Scheduler supports both single and multiple levels of resource grouping that can be customized both in timeline and vertical Scheduler views.

Explore the advanced options available with the multiple resources and grouping concepts of Angular Scheduler by watching this video:

`youtube:0-7Pwde-DpU`

### Vertical resource view

The following code example displays how the multiple resources are grouped and its events are portrayed in the default calendar views.

{% tab template="schedule/resource-grouping", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import {
    WeekService, MonthService, AgendaService, EventSettingsModel, GroupModel
} from '@syncfusion/ej2-angular-schedule';
import { resourceConferenceData } from './datasource.ts';

@Component({
    selector: "app-root",
    providers: [WeekService, MonthService, AgendaService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings" [group]='group'>
      <e-resources>
        <e-resource field="ProjectId" title="Choose Project" name="Projects"
            [dataSource]="projectDataSource"
            textField="text" idField="id" colorField="color">
        </e-resource>
        <e-resource field="TaskId" title="Category" name="Categories"
          [dataSource]="categoryDataSource" [allowMultiple]="allowMultipleCategory"
          textField="text" idField="id" colorField="color">
        </e-resource>
      </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 3, 1);
    public views: Array<string> = ['Week', 'Month', 'Agenda'];
    public eventSettings: EventSettingsModel = {
        dataSource: resourceConferenceData
    };
    public group: GroupModel = {
        byGroupID: false,
        resources: ['Projects', 'Categories']
    };
    public projectDataSource: Object[] = [
        { text: 'PROJECT 1', id: 1, color: '#cb6bb2' },
        { text: 'PROJECT 2', id: 2, color: '#56ca85' },
        { text: 'PROJECT 3', id: 3, color: '#df5286' }
    ];
    public allowMultipleCategory: Boolean = true;
    public categoryDataSource: Object[] = [
        { text: 'Development', id: 1, color: '#df5286' },
        { text: 'Testing', id: 2, color: '#7fa900' }
    ];
}
```

{% endtab %}

### Timeline resource view

The following code example depicts how to group the multiple resources on Timeline Scheduler views and its relevant events are displayed accordingly under those resources.

{% tab template="schedule/resource-grouping", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import {
    TimelineViewsService, TimelineMonthService, AgendaService, EventSettingsModel, GroupModel
} from '@syncfusion/ej2-angular-schedule';
import { resourceData } from './datasource.ts';

@Component({
    selector: "app-root",
    providers: [TimelineViewsService, TimelineMonthService, AgendaService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [currentView]='currentView' [eventSettings]="eventSettings" [group]='group'>
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
    public selectedDate: Date = new Date(2018, 3, 4);
    public currentView: string = 'TimelineWeek';
    public views: Array<string> = ['TimelineWeek', 'TimelineMonth', 'Agenda'];
    public eventSettings: EventSettingsModel = {
        dataSource: resourceData
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

### Grouping single-level resources

This kind of grouping allows the Scheduler to display all the resources at a single level simultaneously. The appointments mapped under resources will be displayed with the colors as per the `colorField` defined on the resources collection.

**Example:** To display the Scheduler with single level resource grouping,

{% tab template="schedule/single-level-resource", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import {
    WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService, EventSettingsModel, GroupModel
} from '@syncfusion/ej2-angular-schedule';
import { resourceData } from './datasource.ts';

@Component({
    selector: "app-root",
    providers: [WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings" [group]='group'>
      <e-resources>
        <e-resource field="OwnerId" title="Owner" name="Owners"
          [dataSource]="ownerDataSource" [allowMultiple]="allowMultipleCategory"
          textField='OwnerText' idField='Id' colorField='OwnerColor'>
        </e-resource>
      </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 3, 1);
    public views: Array<string> = ['Week', 'Month', 'TimelineWeek', 'TimelineMonth', 'Agenda'];
    public eventSettings: EventSettingsModel = {
        dataSource: resourceData
    };
    public group: GroupModel = {
        resources: ['Owners']
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

> The `name` field defined in the **resources** collection namely `Owners` will be mapped within the `group` property, in order to enable the grouping option with those resource levels on the Scheduler.

### Grouping multi-level resources

It is possible to group the resources of Scheduler in multiple levels, by mapping the child resources to each parent resource. In the following example, there are 2 levels of resources, on which the second level resources are defined with `groupID` mapping to the first level resource's ID so as to establish the parent-child relationship between them.

**Example:** To display the Scheduler with multiple level resource grouping options,

{% tab template="schedule/multiple-level-resource", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from "@angular/core";
import {
  WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService,
  EventSettingsModel, GroupModel } from "@syncfusion/ej2-angular-schedule";
import { resourceData } from "./datasource";
@Component({
  selector: "app-root",
  providers: [WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService ],
  // specifies the template string for the Schedule component
  template: `<ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate"
      [views]="views" [currentView]="currentView" [eventSettings]="eventSettings" [group]="group">
      <e-resources>
        <e-resource field="RoomId" title="Room" name="Rooms" [dataSource]="roomDataSource"
         textField="RoomText" idField="Id" colorField="RoomColor">
        </e-resource>
        <e-resource field="OwnerId" title="Owner" name="Owners" [dataSource]="ownerDataSource"         [allowMultiple]="allowMultipleCategory" textField="OwnerText"
         idField="Id" groupIDField="OwnerGroupId" colorField="OwnerColor">
        </e-resource>
      </e-resources>
    </ejs-schedule>
  `
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 3, 1);
  public views: Array<string> = ["Week", "Month", "TimelineWeek", "TimelineMonth", "Agenda"];
  public eventSettings: EventSettingsModel = { dataSource: resourceData };
  public group: GroupModel = {
    resources: ["Rooms", "Owners"]
  };
  public roomDataSource: Object[] = [
    { RoomText: "ROOM 1", Id: 1, RoomColor: "#cb6bb2" },
    { RoomText: "ROOM 2", Id: 2, RoomColor: "#56ca85" }
  ];
  public allowMultipleOwner: Boolean = true;
  public ownerDataSource: Object[] = [
    { OwnerText: "Nancy", Id: 1, OwnerGroupId: 1, OwnerColor: "#ffaa00" },
    { OwnerText: "Steven", Id: 2, OwnerGroupId: 2, OwnerColor: "#f8a398" },
    { OwnerText: "Michael", Id: 3, OwnerGroupId: 1, OwnerColor: "#7499e1" }
  ];
}
```

{% endtab %}

### One-to-One grouping

In multi-level grouping, Scheduler usually groups the resources on the child level based on the `GroupID` that maps with the `Id` field of parent level resources (as `byGroupID` set to true by default). There are also option which allows you to group all the child resource(s) against each of its parent resource(s). To enable this kind of grouping, set `false` to the `byGroupID` option within the `group` property. In the following code example, there are two levels of resources, on which all the 3 resources at the child level is mapped one to one with each resource on the first level.

{% tab template="schedule/multiple-level-resource", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from "@angular/core";
import {
  WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService, EventSettingsModel, GroupModel
} from "@syncfusion/ej2-angular-schedule";
import { resourceData } from "./datasource";
@Component({
  selector: "app-root",
  providers: [WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [currentView]="currentView" [eventSettings]="eventSettings" [group]="group">
      <e-resources>
        <e-resource field="RoomId" title="Room" name="Rooms" [dataSource]="roomDataSource"
          textField="RoomText" idField="Id" colorField="RoomColor">
        </e-resource>
        <e-resource field="OwnerId" title="Owner" name="Owners"
          [dataSource]="ownerDataSource" [allowMultiple]="allowMultipleOwner"
          textField="OwnerText" idField="Id" colorField="OwnerColor">
        </e-resource>
      </e-resources>
    </ejs-schedule>
  `
})
export class AppComponent {
  public selectedDate: Date = new Date(2018, 3, 1);
  public views: Array<string> = ["Week", "Month", "TimelineWeek", "TimelineMonth", "Agenda"];
  public eventSettings: EventSettingsModel = {
    dataSource: resourceData
  };
  public group: GroupModel = {
    byGroupID: false,
    resources: ['Rooms', 'Owners']
  };
  public roomDataSource: Object[] = [
    { RoomText: 'ROOM 1', Id: 1, RoomColor: '#cb6bb2' },
    { RoomText: 'ROOM 2', Id: 2, RoomColor: '#56ca85' }
  ];
  public allowMultipleOwner: Boolean = true;
  public ownerDataSource: Object[] = [
    { OwnerText: 'Nancy', Id: 1, OwnerColor: '#ffaa00' },
    { OwnerText: 'Steven', Id: 2, OwnerColor: '#f8a398' },
    { OwnerText: 'Michael', Id: 3, OwnerColor: '#7499e1' }
  ];
}
```

{% endtab %}

### Grouping resources by date

It groups the number of resources under each date and is applicable only on the calendar views such as Day, Week, Work Week, Month, Agenda and Month-Agenda. To enable such grouping, set `byDate` option to `true` within the `group` property.

**Example:** To display the Scheduler with resources grouped by date,

{% tab template="schedule/group-by-date", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import {
    WeekService, MonthService, AgendaService, EventSettingsModel, GroupModel
} from '@syncfusion/ej2-angular-schedule';
import { resourceData } from './datasource.ts';

@Component({
    selector: "app-root",
    providers: [WeekService, MonthService, AgendaService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings" [group]='group'>
      <e-resources>
        <e-resource field="OwnerId" title="Owner" name="Owners"
          [dataSource]="ownerDataSource" [allowMultiple]="allowMultipleOwner"
          textField='text' idField='id' colorField='color'>
        </e-resource>
      </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 3, 1);
    public views: Array<string> = ['Week', 'Month', 'Agenda'];
    public eventSettings: EventSettingsModel = {
        dataSource: resourceData
    };
    public group: GroupModel = {
        byDate: true,
        resources: ['Owners']
    };
    public allowMultipleOwner: Boolean = true;
    public ownerDataSource: Object[] = [
        { text: 'Alice', id: 1, color: '#1aaa55' },
        { text: 'Smith', id: 2, color: '#7fa900' }
    ];
}
```

{% endtab %}

> This kind of grouping by date is not applicable on any of the timeline views.

### Grouping with empty resource datasource

When using grouping, it is mandatory to provide at least one resource data in dataSource collection this is the default behavior of our scheduler. If the resource does not have a dataSource, scheduler rendered like below image.

![Grouping with empty resource](./images/empty-datasource.png)

To handle this case you can make the default schedule by emptying the group property.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component, Inject, ViewEncapsulation, ViewChild } from "@angular/core";
import {
  ScheduleComponent, EventSettingsModel, GroupModel, ResourceDetails, TreeViewArgs,
  WeekService, MonthService, AgendaService, ResizeService,DragAndDropService
} from "@syncfusion/ej2-angular-schedule";

@Component({
    selector: "app-root",
    providers: [WeekService, MonthService, AgendaService, ResizeService, DragAndDropService],
    // specifies the template string for the Schedule component
    template: `
   <ejs-schedule #scheduleObj cssClass='schedule-group' width='100%' height='650px' [group]="group" [selectedDate]="selectedDate"  [readonly]="true"
        [eventSettings]="eventSettings" (dataBinding)='onDataBinding($events)'>
        <e-views>
            <e-view option="Week"></e-view>
            <e-view option="Month"></e-view>
            <e-view option="Agenda"></e-view>
        </e-views>
        <e-resources>
            <e-resource field='AirlineId' title='Airline Name' name='Airlines' [allowMultiple]='allowMultiple' [dataSource]='resourceDataSource'
                textField='AirlineName' idField='AirlineId' colorField='AirlineColor'>
            </e-resource>
        </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
  @ViewChild("scheduleObj")
  public scheduleObj: ScheduleComponent;
  public selectedDate: Date = new Date(2018, 3, 1);
  public resourceDataSource: Object[] = [];
  public group: GroupModel = { resources: ["Airlines"] };
  public allowMultiple: Boolean = true;
  public eventSettings: EventSettingsModel = {
    dataSource: [],
    fields: {
      subject: { title: "Travel Summary", name: "Subject" },
      location: { title: "Source", name: "Location" },
      description: { title: "Comments", name: "Description" },
      startTime: { title: "Departure Time", name: "StartTime" },
      endTime: { title: "Arrival Time", name: "EndTime" }
    }
  };
  onDataBinding(args) {
    //check the resource count
    if ((this.scheduleObj.resourceCollection[0].dataSource as any).length === 0 &&
    this.scheduleObj.group.resources.length > 0) {
      // Render default scheduler to handle above case.
      this.scheduleObj.group.resources = [];
    }
  }
}
```

{% endtab %}

## Customizing parent resource cells

In timeline view work cells of parent resource can be customized by checking the `elementType` as `resourceGroupCells` in the event `renderCell`. In the following code example, background color of the work hours has been changed.

{% tab template="schedule/default", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import { TimelineViewsService, TimelineMonthService, EventSettingsModel, GroupModel, RenderCellEventArgs } from '@syncfusion/ej2-angular-schedule';
import { resourceData } from './datasource.ts';

@Component({
    selector: "app-root",
    providers: [TimelineViewsService, TimelineMonthService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views" currentView='TimelineWeek'
      [eventSettings]="eventSettings" [group]='group' (renderCell)="onRenderCell($event)">
      <e-resources>
        <e-resource field="RoomId" title="Room" name="Rooms"
          [dataSource]="roomDataSource" [allowMultiple]="allowMultipleRoom"
          textField='text' idField='id' colorField='color'></e-resource>
        <e-resource field="OwnerId" title="Owner" name="Owners"
          [dataSource]="ownerDataSource" [allowMultiple]="allowMultipleOwner"
          textField='text' idField='id' colorField='color' groupIDField='groupId'></e-resource>
      </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 3, 4);
    public views: Array<string> = ['TimelineDay', 'TimelineWeek', 'TimelineMonth'];
    public eventSettings: EventSettingsModel = { dataSource: resourceData };
    public group: GroupModel = { resources: ['Rooms', 'Owners'] };
    public allowMultipleRoom: Boolean = false;
    public allowMultipleOwner: Boolean = true;
    public roomDataSource: Object[] = [
      { text: 'ROOM 1', id: 1, color: '#cb6bb2' },
      { text: 'ROOM 2', id: 2, color: '#56ca85' }
    ];
    public ownerDataSource: Object[] = [
      { text: 'Nancy', id: 1, groupId: 1, color: '#ffaa00' },
      { text: 'Steven', id: 2, groupId: 2, color: '#f8a398' },
      { text: 'Michael', id: 3, groupId: 1, color: '#7499e1' }
    ];
    public onRenderCell(args: RenderCellEventArgs): void {
      if (args.elementType == 'resourceGroupCells' && args.element.className.indexOf('e-work-hours') > 0) {
        args.element.style.background = "#FAFAE3";
      }
    }
}
```

{% endtab %}

## Working with shared events

Multiple resources can share the same events, thus allowing the CRUD action made on it to reflect on all other shared instances simultaneously. To enable such option, set `allowGroupEdit` option to `true` within the `group` property. With this property enabled, a single appointment
object will be maintained within the appointment collection, even if it is shared by more than one resource – whereas the resource fields of such appointment object will be in array which hold the IDs of the multiple resources.

> Any actions such as create, edit or delete held on any one of the shared event instances, will be reflected on all other related instances visible on the UI.

**Example:** To edit all the resource events simultaneously,

{% tab template="schedule/resource-grouping", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import {
    WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService, ResizeService, EventSettingsModel, GroupModel
} from '@syncfusion/ej2-angular-schedule';
@Component({
    selector: "app-root",
    providers: [WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService, ResizeService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings" [group]='group'>
      <e-resources>
        <e-resource field="ConferenceId" title="Conference" name="Conferences"
          [dataSource]="conferenceDataSource" [allowMultiple]="allowMultipleCategory"
          textField='Text' idField='Id' colorField='Color'>
        </e-resource>
      </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 5, 5);
    public views: Array<string> = ['Week', 'Month', 'TimelineWeek', 'TimelineMonth', 'Agenda'];
    public eventSettings: EventSettingsModel = {
        dataSource: [
            {
                Id: 1,
                Subject: 'Burning Man',
                StartTime: new Date(2018, 5, 1, 15, 0),
                EndTime: new Date(2018, 5, 1, 17, 0),
                ConferenceId: [1, 2, 3]
            }, {
                Id: 2,
                Subject: 'Data-Driven Economy',
                StartTime: new Date(2018, 5, 2, 12, 0),
                EndTime: new Date(2018, 5, 2, 14, 0),
                ConferenceId: [1, 2]
            }, {
                Id: 3,
                Subject: 'Techweek',
                StartTime: new Date(2018, 5, 2, 15, 0),
                EndTime: new Date(2018, 5, 2, 17, 0),
                ConferenceId: [2, 3]
            }, {
                Id: 4,
                Subject: 'Content Marketing World',
                StartTime: new Date(2018, 5, 2, 18, 0),
                EndTime: new Date(2018, 5, 2, 20, 0),
                ConferenceId: [1, 3]
            }, {
                Id: 5,
                Subject: 'B2B Marketing Forum',
                StartTime: new Date(2018, 5, 3, 10, 0),
                EndTime: new Date(2018, 5, 3, 12, 0),
                ConferenceId: [1, 2, 3]
            }]
    };
    public group: GroupModel = {
        allowGroupEdit: true,
        resources: ['Conferences']
    };
    public allowMultipleCategory: Boolean = true;
    public conferenceDataSource: Object[] = [
        { Text: 'Margaret', Id: 1, Color: '#1aaa55' },
        { Text: 'Robert', Id: 2, Color: '#357cd2' },
        { Text: 'Laura', Id: 3, Color: '#7fa900' }
    ];
}
```

{% endtab %}

## Simple resource header customization

It is possible to customize the resource header cells using built-in template option and change the look and appearance of it in both the vertical and timeline view modes. All the resource related fields and other information can be accessed within the resource header template option.

**Example:** To customize the resource header and display it along with designation field, refer the below code example.

{% tab template="schedule/resource-header", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import {
    WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService, EventSettingsModel, GroupModel
} from '@syncfusion/ej2-angular-schedule';
import { doctorData } from './datasource.ts';
@Component({
    selector: "app-root",
    providers: [WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings" [group]='group'>
        <e-resources>
            <e-resource field="DoctorId" title="Doctor Name" name="Doctors"
            [dataSource]="doctorDataSource"
            textField='text' idField='id' colorField='color' designationField='designation'>
            </e-resource>
        </e-resources>
        <ng-template #resourceHeaderTemplate let-data>
            <div class='template-wrap'>
                <div class="resource-details">
                    <div class="resource-name">{{data.resourceData.text}}</div>
                    <div class="resource-designation">{{data.resourceData.designation}}</div>
                </div>
            </div>
        </ng-template>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 3, 5);
    public views: Array<string> = ['Week', 'Month', 'TimelineWeek', 'TimelineMonth', 'Agenda'];
    public eventSettings: EventSettingsModel = {
        dataSource: doctorData
    };
    public group: GroupModel = {
        resources: ['Doctors']
    };
    public allowMultipleDoctors: Boolean = true;
    public doctorDataSource: Object[] = [
        { text: 'Will Smith', id: 1, color: '#ea7a57', designation: 'Cardioligst' },
        { text: 'Alice', id: 2, color: '#7fa900', designation: 'Neurologist' },
        { text: 'Robson', id: 3, color: '#7fa900', designation: 'Orthopedic Surgeon'  }
    ];
}
```

{% endtab %}

> To customize the resource header in compact mode properly make use of the class `e-device` as in the code example.

![Resource header template in compact mode](./images/header-template.png)

## Customizing resource header with multiple columns

It is possible to customize the resource headers to display with multiple columns such as Room, Type and Capacity. The following code example depicts the way to achieve it and is applicable only on timeline views.

{% tab template="schedule/resource-header-column-customization", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript

import { Component } from '@angular/core';
import {
    TimelineViewsService, TimelineMonthService, EventSettingsModel, GroupModel, RenderCellEventArgs
} from '@syncfusion/ej2-angular-schedule';
import { roomData } from './datasource.ts';
@Component({
    selector: "app-root",
    providers: [TimelineViewsService, TimelineMonthService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings" [group]='group' (renderCell)='onRenderCell($event)'>
        <e-resources>
            <e-resource field="RoomId" title="Room Type" name="MeetingRoom"
            [dataSource]="roomDataSource" [allowMultiple]='allowMultipleRoom'
            textField='text' idField='id' colorField='color'>
            </e-resource>
        </e-resources>
        <ng-template #resourceHeaderTemplate let-data>
            <div class='template-wrap'>
                <div class="room-name">{{data.resourceData.text}}</div>
                <div class="room-type">{{data.resourceData.type}}</div>
                <div class="room-capacity">{{data.resourceData.capacity}}</div>
            </div>
        </ng-template>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 7, 1);
    public views: Array<string> = ['TimelineWeek', 'TimelineMonth'];
    public eventSettings: EventSettingsModel = {
        dataSource: roomData
    };
    public group: GroupModel = {
        resources: ['MeetingRoom']
    };
    public allowMultipleRoom: Boolean = true;
    public roomDataSource: Object[] = [
        { text: 'Jammy', id: 1, color: '#ea7a57', capacity: 20, type: 'Conference' },
        { text: 'Tweety', id: 2, color: '#7fa900', capacity: 7, type: 'Cabin' },
        { text: 'Nestle', id: 3, color: '#5978ee', capacity: 5, type: 'Cabin' },
        { text: 'Phoenix', id: 4, color: '#fec200', capacity: 15, type: 'Conference' },
        { text: 'Mission', id: 5, color: '#df5286', capacity: 25, type: 'Conference' },
        { text: 'Hangout', id: 6, color: '#00bdae', capacity: 10, type: 'Cabin' },
        { text: 'Rick Roll', id: 7, color: '#865fcf', capacity: 20, type: 'Conference' },
        { text: 'Rainbow', id: 8, color: '#1aaa55', capacity: 8, type: 'Cabin' },
        { text: 'Swarm', id: 9, color: '#df5286', capacity: 30, type: 'Conference' },
        { text: 'Photogenic', id: 10, color: '#710193', capacity: 25, type: 'Conference' }
    ];
    onRenderCell(args: RenderCellEventArgs):void {
        if (args.elementType === 'emptyCells' && args.element.classList.contains('e-resource-left-td')) {
            let target: HTMLElement = args.element.querySelector('.e-resource-text') as HTMLElement;
            target.innerHTML = '<div class="name">Rooms</div><div class="type">Type</div><div class="capacity">Capacity</div>';
        }
    }
}
```

{% endtab %}

## Displaying tooltip for resource headers

It is possible to display tooltips over the resource headers showing the resource information. By default, there won't be any tooltips displayed on the resource headers, and to enable it, you need to assign the customized template design to the `headerTooltipTemplate` option within the `group` property.

{% tab template="schedule/header-tooltip", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import {
    WeekService, MonthService, TimelineViewsService, TimelineMonthService, EventSettingsModel, GroupModel } from '@syncfusion/ej2-angular-schedule';
import { resourceData } from './datasource.ts';
@Component({
    selector: "app-root",
    providers: [WeekService, MonthService, TimelineViewsService, TimelineMonthService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings" [group]='group'>
        <e-resources>
            <e-resource field="OwnerId" title="Owner" name="Owners"
            [dataSource]="roomDataSource" [allowMultiple]='allowMultipleRoom'
            textField='OwnerText' idField='Id' groupIdField='OwnerGroupId' colorField='OwnerColor'>
            </e-resource>
        </e-resources>
        <ng-template #groupHeaderTooltipTemplate let-data>
            <div class='template-wrap'>
                <div class="res-text">Name:  {{data.resourceData.OwnerText}} </div>
            </div>
        </ng-template>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 3, 1);
    public views: Array<string> = ['Week', 'Month', 'TimelineWeek', 'TimelineMonth'];
    public eventSettings: EventSettingsModel = {
        dataSource: resourceData
    };
    public group: GroupModel = {
        resources: ['Owners']
    };
    public allowMultipleRoom: Boolean = true;
    public roomDataSource: Object[] = [
        { OwnerText: 'Nancy', Id: 1, OwnerGroupId: 1, OwnerColor: '#ffaa00' },
        { OwnerText: 'Steven', Id: 2, OwnerGroupId: 2, OwnerColor: '#f8a398' },
        { OwnerText: 'Michael', Id: 3, OwnerGroupId: 1, OwnerColor: '#7499e1' }
    ];
}
```

{% endtab %}

## Choosing among resource colors for appointments

By default, the colors defined on the top level resources collection will be applied for the events. In case, if you want to apply specific resource color to events irrespective of its top-level parent resource color, it can be achieved by defining `resourceColorField` option within the `eventSettings` property.

In the following example, the colors mentioned in the second level will get applied over the events.

{% tab template="schedule/multiple-resource", sourceFiles="app/**/*.ts", iframeHeight="627px" %}

```typescript
import { Component, ViewChild } from "@angular/core";
import {
   ScheduleComponent, WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService, EventSettingsModel, GroupModel
} from "@syncfusion/ej2-angular-schedule";
import { ChangeArgs } from "@syncfusion/ej2-buttons";
import { resourceData } from "./datasource";
@Component({
  selector: "app-root",
  providers: [WeekService, MonthService, AgendaService, TimelineViewsService, TimelineMonthService],
  // specifies the template string for the Schedule component
  template: `<div style="padding: 10px;"><ejs-radiobutton label="Rooms" name="default" value="Rooms" checked="true" (change)="onChange($event)"></ejs-radiobutton>
  <ejs-radiobutton label="Owners" name="default" value="Owners" (change)="onChange($event)"></ejs-radiobutton>
  </div>
    <ejs-schedule #scheduleObj width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [currentView]="currentView" [eventSettings]="eventSettings" [group]="group">
      <e-resources>
        <e-resource field="RoomId" title="Room" name="Rooms" [dataSource]="roomDataSource"
          textField="RoomText" idField="Id" colorField="RoomColor">
        </e-resource>
        <e-resource field="OwnerId" title="Owner" name="Owners"
          [dataSource]="ownerDataSource" [allowMultiple]="allowMultipleCategory"
          textField="OwnerText" idField="Id" groupIDField="OwnerGroupId" colorField="OwnerColor">
        </e-resource>
      </e-resources>
    </ejs-schedule>
  `
})
export class AppComponent {
  @ViewChild('scheduleObj')
  public scheduleObj: ScheduleComponent;
  public selectedDate: Date = new Date(2018, 3, 1);
  public views: Array<string> = ["Week", "Month", "TimelineWeek", "TimelineMonth", "Agenda"];
  public eventSettings: EventSettingsModel = {
    dataSource: resourceData,
    resourceColorField: 'Rooms'
  };
  public group: GroupModel = {
    resources: ["Rooms", "Owners"]
  };
  public roomDataSource: Object[] = [
    { RoomText: "ROOM 1", Id: 1, RoomColor: "#cb6bb2" },
    { RoomText: "ROOM 2", Id: 2, RoomColor: "#56ca85" }
  ];
  public allowMultipleOwner: Boolean = true;
  public ownerDataSource: Object[] = [
    { OwnerText: "Nancy", Id: 1, OwnerGroupId: 1, OwnerColor: "#ffaa00" },
    { OwnerText: "Steven", Id: 2, OwnerGroupId: 2, OwnerColor: "#f8a398" },
    { OwnerText: "Michael", Id: 3, OwnerGroupId: 1, OwnerColor: "#7499e1" }
  ];
  public onChange(args: ChangeArgs): void {
    this.scheduleObj.eventSettings.resourceColorField = args.value;
  }
}
```

{% endtab %}

> The value of the `resourceColorField` field should be mapped with the `name` value given within the `resources` property.

## Dynamically add and remove resources

It is possible to add or remove the resources dynamically to and from the Scheduler respectively. In the following example, when the checkboxes are checked and unchecked, the respective resources gets added up or removed from the Scheduler layout. To add new resource dynamically, `addResource` method is used which accepts the arguments such as resource object, resource name (within which level, the resource object to be added) and index (position where the resource needs to be added).

To remove the resources dynamically, `removeResource` method is used which accepts the index (position from where the resource to be removed) and resource name (within which level, the resource object presents) as parameters.

{% tab template="schedule/dynamic-resource", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { holidayData, birthdayData, companyData, personalData } from './datasource.ts';
import { ChangeEventArgs } from '@syncfusion/ej2-buttons';
import { ScheduleComponent, EventSettingsModel, GroupModel, MonthService, TimelineViewsService, TimelineMonthService, ResizeService, DragAndDropService } from '@syncfusion/ej2-angular-schedule';

@Component({
  selector: "app-root",
  providers: [MonthService, TimelineViewsService, TimelineMonthService, ResizeService, DragAndDropService],
  // specifies the template string for the Schedule component
  template: `<div class="control-section">
  <div class="col-lg-12 property-section">
    <table id="property" title="Show / Hide Resource">
        <tbody>
            <tr>
                <td>
                    <ejs-checkbox cssClass="personal" label="My Calender" value="1" [checked]="true" [disabled]="true" (change)="onChange($event)"></ejs-checkbox>
                </td>
                <td>
                    <ejs-checkbox cssClass="company" label="Company" value="2" [checked]="false" (change)="onChange($event)"></ejs-checkbox>
                </td>
                <td>
                    <ejs-checkbox cssClass="birthday" label="Birthday" value="3" [checked]="false" (change)="onChange($event)"></ejs-checkbox>
                </td>
                <td>
                    <ejs-checkbox cssClass="holiday" label="Holiday" value="4" [checked]="false" (change)="onChange($event)"></ejs-checkbox>
                </td>
            </tr>
        </tbody>
    </table>
</div>
  <div>
      <ejs-schedule #scheduleObj cssClass='schedule-add-remove-resources' width='100%' height='650px' [group]="group" [selectedDate]="selectedDate"
          [eventSettings]="eventSettings">
          <e-resources>
              <e-resource field='CalendarId' title='Calendars' [dataSource]='resourceDataSource' [allowMultiple]='allowMultiple' name='Calendars'
                  textField='CalendarText' idField='CalendarId' colorField='CalendarColor'>
              </e-resource>
          </e-resources>
          <e-views>
              <e-view option="Month"></e-view>
              <e-view option="TimelineWeek"></e-view>
              <e-view option="TimelineMonth"></e-view>
          </e-views>
      </ejs-schedule>
  </div>
</div>`
})

export class AppComponent {
    public calendarCollections: Object[] = [
        { CalendarText: 'My Calendar', CalendarId: 1, CalendarColor: '#c43081' },
        { CalendarText: 'Company', CalendarId: 2, CalendarColor: '#ff7f50' },
        { CalendarText: 'Birthday', CalendarId: 3, CalendarColor: '#AF27CD' },
        { CalendarText: 'Holiday', CalendarId: 4, CalendarColor: '#808000' }
    ];
    public group: GroupModel = { resources: ['Calendars'] };
    public resourceDataSource: Object[] = [this.calendarCollections[0]];
    public allowMultiple: Boolean = true;
    public selectedDate: Date = new Date(2018, 3, 1);
    public eventSettings: EventSettingsModel = { dataSource: this.generateCalendarData() };
    @ViewChild('scheduleObj')
    public scheduleObj: ScheduleComponent;
    generateCalendarData(): Object[] {
        return [...personalData, ...companyData, ...birthdayData, ...holidayData];
    }
    onChange(args: ChangeEventArgs): void {
        let value: number = parseInt((<Element>args.event.target).getAttribute('value'), 10);
        let resourceData: Object[] =
            this.calendarCollections.filter((calendar: { [key: string]: Object }) => calendar.CalendarId === value);
        if (args.checked) {
            this.scheduleObj.addResource(resourceData[0], 'Calendars', value - 1);
        } else {
            this.scheduleObj.removeResource(value, 'Calendars');
        }
    }
}
```

{% endtab %}

## Setting different working days and hours for resources

Each resource in the Scheduler can have different working hours as well as different working days set to it. There are default options available within the `resources` collection, to customize the default working hours and days of the Scheduler.

### Set different work days

Different working days can be set for the resources of Scheduler using the `workDaysField` property which maps the working days field from the resource dataSource. This field accepts the collection of day indexes (from 0 to 6) of a week. By default, it is set to [1, 2, 3, 4, 5] and in the following example, each resource has been set with different values and therefore each of them will render only those working days. This option is applicable only on the calendar views and is not applicable on timeline views.

{% tab template="schedule/multiple-resource", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import {
    WeekService, WorkWeekService, MonthService, EventSettingsModel, GroupModel
} from '@syncfusion/ej2-angular-schedule';
import { doctorData } from './datasource.ts';
@Component({
    selector: "app-root",
    providers: [WeekService, WorkWeekService, MonthService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [currentView]='currentView' [eventSettings]="eventSettings" [group]='group'>
      <e-resources>
        <e-resource field="DoctorId" title="Conference" name="Conferences"
          [dataSource]="conferenceDataSource" [allowMultiple]="allowMultipleCategory"
          textField='text' idField='id' colorField='color' workDaysField='workDays'>
        </e-resource>
      </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 3, 1);
    public views: Array<string> = ['Week', 'WorkWeek', 'Month'];
    public currentView: string = 'WorkWeek';
    public eventSettings: EventSettingsModel = {
        dataSource: doctorData
    };
    public group: GroupModel = {
        resources: ['Conferences']
    };
    public allowMultipleCategory: Boolean = true;
    public conferenceDataSource: Object[] = [
        { text: 'Will Smith', id: 1, color: '#ea7a57', workDays: [1, 2, 4, 5] },
        { text: 'Alice', id: 2, color: 'rgb(53, 124, 210)', workDays: [1, 3, 5] },
        { text: 'Robson', id: 3, color: '#7fa900' , workDays: [2,6]}
    ];
}
```

{% endtab %}

### Set different work hours

Working hours indicates the work hour duration of a day, which is highlighted visually with active color over the work cells. Each resource on the Scheduler can be defined with its own set of working hours as depicted in the following example.

* `startHourField` - Denotes the start time of the working/business hour in a day.
* `endHourField` - Denotes the end time limit of the working/business hour in a day.

{% tab template="schedule/multiple-resource", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component } from '@angular/core';
import {
    WeekService, MonthService, TimelineViewsService, TimelineMonthService, EventSettingsModel, GroupModel
} from '@syncfusion/ej2-angular-schedule';
import { doctorData } from './datasource.ts';
@Component({
    selector: "app-root",
    providers: [WeekService, MonthService, TimelineViewsService, TimelineMonthService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule width="100%" height="550px" [selectedDate]="selectedDate" [views]="views"
      [eventSettings]="eventSettings" [group]='group'>
      <e-resources>
        <e-resource field="DoctorId" title="Conference" name="Conferences"
          [dataSource]="conferenceDataSource" [allowMultiple]="allowMultipleCategory"
          textField='text' idField='id' colorField='color' startHourField='startHour' endHourField='endHour'>
        </e-resource>
      </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
    public selectedDate: Date = new Date(2018, 3, 1);
    public views: Array<string> = ['Week', 'Month', 'TimelineWeek', 'TimelineMonth'];
    public eventSettings: EventSettingsModel = {
        dataSource: doctorData
    };
    public group: GroupModel = {
        resources: ['Conferences']
    };
    public allowMultipleCategory: Boolean = true;
    public conferenceDataSource: Object[] = [
        { text: 'Will Smith', id: 1, color: '#ea7a57', startHour: '08:00', endHour: '15:00' },
        { text: 'Alice', id: 2, color: '#357cd2', startHour: '10:00', endHour: '18:00' },
        { text: 'Robson', id: 3, color: '#7fa900', startHour: '06:00', endHour: '13:00' }
    ];
}
```

{% endtab %}

In this example, a resource named `Will Smith` is depicted with working hours ranging from 8.00 AM to 3.00 PM and is visually illustrated with active colors, whereas the other two resources have different working hours set.

## Compact view in mobile

Although the Scheduler views are designed keeping in mind the responsiveness of the control in mobile devices, however when using Scheduler with multiple resources - it is difficult to view all the resources and its relevant events at once on the mobile. Therefore, we have introduced a new compact mode specially for displaying multiple resources of Scheduler on mobile devices. By default, this mode is enabled while using Scheduler with multiple resources on mobile devices. If in case, you need to disable this compact mode, set `false` to the `enableCompactView` option within the `group` property. Disabling this option will display the exact desktop mode of Scheduler view on mobile devices.

With this compact view enabled on mobile, you can view only single resource at a time and to switch to other resources, there is a treeview at the left listing out all other available resources - clicking on which will display that particular resource and its related appointments.

![Resources in compact mode](./images/resource-mobile.png)

Clicking on the menu icon before the resource text will show the resources available in the Scheduler as following.

![Resources menu option in compact mode](./images/resource-menu.png)

## Adaptive UI in desktop

By default, the Scheduler layout adapts automatically in the desktop and mobile devices with appropriate UI changes. In case, if the user wants to display the Adaptive scheduler in desktop mode with adaptive enhancements, then the property `enableAdaptiveUI` can be set to true. Enabling this option will display the exact mobile mode of Scheduler view on desktop devices.

Some of the default changes made for compact Scheduler to render in desktop devices are as follows,
* View options displayed in the Navigation drawer.
* Plus icon is added to the header for new event creation.
* Today icon is added to the header instead of the Today button.
* With Multiple resources – only one resource has been shown to enhance the view experience of resource events details clearly. To switch to other resources, there is a TreeView on the left that lists all other available resources, clicking on which will display that particular resource and its related events.

{% tab template="schedule/resource-grouping", sourceFiles="app/**/*.ts", iframeHeight="588px" %}

```typescript
import { Component, ViewChild, ViewEncapsulation } from '@angular/core';
import {
    ScheduleComponent, EventSettingsModel, GroupModel,
    DayService, WeekService, MonthService, DragAndDropService, View
} from '@syncfusion/ej2-angular-schedule';
import { extend } from '@syncfusion/ej2-base';
import { resourceData, timelineResourceData } from './datasource.ts';

@Component({
    selector: "app-root",
    providers: [DayService, WeekService, MonthService, DragAndDropService],
    // specifies the template string for the Schedule component
    template: `
    <ejs-schedule #scheduleObj id="schedule" width='100%' height='650px' [group]="group" [(currentView)]="currentView"
      [selectedDate]="selectedDate" [enableAdaptiveUI]="true" [eventSettings]="eventSettings">
      <e-views>
        <e-view option="Day"></e-view>
        <e-view option="Week"></e-view>
        <e-view option="Month"></e-view>
      </e-views>
      <e-resources>
        <e-resource field='ProjectId' title='Choose Project' [dataSource]='projectDataSource'
          [allowMultiple]='allowMultiple' name='Projects' textField='text' idField='id' colorField='color'>
        </e-resource>
        <e-resource field='TaskId' title='Category' [dataSource]='categoryDataSource' [allowMultiple]='allowMultiple'
          name='Categories' textField='text' idField='id' groupIDField='groupId' colorField='color'>
        </e-resource>
      </e-resources>
    </ejs-schedule>`
})
export class AppComponent {
    @ViewChild('scheduleObj')
    public scheduleObj: ScheduleComponent;
    public selectedDate: Date = new Date(2018, 3, 4);
    public currentView: View = 'Month';
    public group: GroupModel = {
        resources: ['Projects', 'Categories']
    };
    public projectDataSource: Object[] = [
        { text: 'PROJECT 1', id: 1, color: '#cb6bb2' },
        { text: 'PROJECT 2', id: 2, color: '#56ca85' },
        { text: 'PROJECT 3', id: 3, color: '#df5286' }
    ];
    public categoryDataSource: Object[] = [
        { text: 'Nancy', id: 1, groupId: 1, color: '#df5286' },
        { text: 'Steven', id: 2, groupId: 1, color: '#7fa900' },
        { text: 'Robert', id: 3, groupId: 2, color: '#ea7a57' },
        { text: 'Smith', id: 4, groupId: 2, color: '#5978ee' },
        { text: 'Michael', id: 5, groupId: 3, color: '#df5286' },
        { text: 'Root', id: 6, groupId: 3, color: '#00bdae' }
    ];
    public allowMultiple: Boolean = true;
    public eventSettings: EventSettingsModel = {
        dataSource: <Object[]>extend([], resourceData.concat(timelineResourceData), null, true)
    };
}
```

{% endtab %}

> You can refer to our [Angular Scheduler](https://www.syncfusion.com/angular-ui-components/angular-scheduler) feature tour page for its groundbreaking feature representations. You can also explore our [Angular Scheduler example](https://ej2.syncfusion.com/angular/demos/#/material/schedule/overview) to knows how to present and manipulate data.
