---
title: "Kanban drag and drop"
component: "Kanban"
description: "This article explains how to drag and drop the card information from an external source and vice versa."
---

# Drag and drop

All cards can be dragged and dropped across the columns or within the columns or swimlane row or kanban to an external source and vice versa.

The following drag and drop types are available in the Kanban board.

* Internal drag and drop
    * Column drag and drop
    * Swimlane drag and drop
* External drag and drop
    * Kanban to Kanban
    * Kanban to External source and vice versa.

> Dropped card position varies based on the `sortSettings` property.

## Internal drag and drop

Allows the user to drag and drop the cards within the kanban board. Based on this, we can categorize into two ways.

* Column drag and drop
* Swimlane drag and drop

### Column drag and drop

By default, all cards can be dragged and dropped across the columns and within the columns. You cannot drag and drop the cards when disabling the `allowDragAndDrop` property.

> You can prevent the drag or drop behavior of the particular column by disabling the `allowDrag` or `allowDrop` property.
> You can also control the flow of transition cards between the columns by using the `transitionColumns` property.

In the following example, disable the drag and drop behavior on the Kanban board.

{% tab template="kanban/drag-and-drop" sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { CardSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='data' [cardSettings]='cardSettings' [allowDragAndDrop]='allowDragAndDrop'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public data: Object[] = kanbanData;
    public allowDragAndDrop: Boolean = false;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
}

```

{% endtab %}

### Swimlane drag and drop

By default, Swimlane allows drag and drop across the columns within the swimlane row. Kanban does not allow dragging the cards across the swimlane rows.

Enabling the `dragAndDrop` property allows you to drag the cards across the swimlane rows, which is specified inside the `swimlaneSettings` property.

{% tab template="kanban/swimlane-drag-and-drop" sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { CardSettingsModel, SwimlaneSettingsModel } from '@syncfusion/ej2-angular-kanban';
import { kanbanData } from './datasource';

@Component({
  selector: 'app-root',
  template: `<ejs-kanban keyField='Status' [dataSource]='data' [cardSettings]='cardSettings' [swimlaneSettings]='swimlaneSettings'>
                <e-columns>
                  <e-column headerText='To do' keyField='Open'></e-column>
                  <e-column headerText='In Progress' keyField='InProgress'></e-column>
                  <e-column headerText='Testing' keyField='Testing'></e-column>
                  <e-column headerText='Done' keyField='Close'></e-column>
                </e-columns>
            </ejs-kanban>`
})
export class AppComponent {
    public data: Object[] = kanbanData;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    public swimlaneSettings: SwimlaneSettingsModel = { keyField: 'Assignee', allowDragAndDrop: true };
}

```

{% endtab %}

## External drag and drop

Allows the user to drag and drop the cards from one kanban to another kanban or Kanban to an external source and vice versa.

### Kanban to kanban

Drag and drop the card from one kanban to another kanban and vice versa. This can be achieved by specifying the `externalDropId` property which is used to specify the id of the dropped kanban element and the `dragStop` event which is used to delete the card on dragged Kanban and add the card on dropped Kanban using the `deleteCard` and `addCard` public methods.

> Before adding a card to dropped kanban, you can manually change the card data `headerField` when the same card data `headerField` is dropped to another Kanban.

In the following example, Drag the card from one Kanban and drop it into another kanban using the `dragStop` event. In this event, remove the card from the dragged Kanban by using the `deleteCard` public method and add the card to the dropped Kanban by using the `addCard` public method.

{% tab template="kanban/kanban-to-kanban" sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { closest } from '@syncfusion/ej2-base';
import { CardSettingsModel, DragEventArgs, KanbanComponent } from '@syncfusion/ej2-angular-kanban';
import { kanbanAData, kanbanBData } from './datasource';
@Component({
  selector: 'app-root',
  template: `<div class="container-fluid">
      <div class="row">
        <div class="col-sm-6">
        <h4>Kanban A</h4>
        <ejs-kanban id='KanbanA' #KanbanA keyField='Status' [dataSource]='dataA' [externalDropId]='externalKanbanADropId'
          [cardSettings]='cardSettings' (dragStop)='onKanbanADragStop($event)'>
          <e-columns>
            <e-column headerText='To do' keyField='Open'></e-column>
            <e-column headerText='Done' keyField='Close'></e-column>
          </e-columns>
        </ejs-kanban>
      </div>
        <div class="col-sm-6">
        <h4>Kanban B</h4>
        <ejs-kanban id='KanbanB' #KanbanB keyField='Status' [dataSource]='dataB' [externalDropId]='externalKanbanBDropId'
          [cardSettings]='cardSettings' (dragStop)='onKanbanBDragStop($event)'>
          <e-columns>
            <e-column headerText='To do' keyField='Open'></e-column>
            <e-column headerText='Done' keyField='Close'></e-column>
          </e-columns>
        </ejs-kanban>
      </div>
      </div>
    </div>`
})
export class AppComponent {
  @ViewChild('KanbanA')
    public kanbanObjA: KanbanComponent;
    @ViewChild('KanbanB')
    public kanbanObjB: KanbanComponent;
    public dataA: Object[] = kanbanAData;
    public dataB: Object[] = kanbanBData;
    public cardSettings: CardSettingsModel = {
        contentField: 'Summary',
        headerField: 'Id'
    };
    public externalKanbanADropId: string[] = ["#KanbanB"];
    public externalKanbanBDropId: string[] = ["#KanbanA"];
    onKanbanADragStop(args: DragEventArgs) {
      let kanbanBElement: Element = <Element>closest(args.event.target as Element, '#KanbanB');
      if (kanbanBElement) {
        this.kanbanObjA.deleteCard(args.data);
        this.kanbanObjB.addCard(args.data, args.dropIndex);
        args.cancel = true;
    }
    };
    onKanbanBDragStop(args: DragEventArgs) {
      let kanbanAElement: Element = <Element>closest(args.event.target as Element, '#KanbanA');
      if (kanbanAElement) {
        this.kanbanObjB.deleteCard(args.data);
        this.kanbanObjA.addCard(args.data, args.dropIndex);
        args.cancel = true;
    }
    };
}

```

{% endtab %}

### Treeview to Kanban

Drag the card from the Kanban board and drop it to the Treeview component and vice versa.

In the following sample, remove the data from the Kanban board using the `deleteCard` public method and add to the Treeview component using the `addNodes` public method at Kanban `dragStop` event when dragging the card and dropping it to the Treeview component. Remove the data from Treeview using the `removeNodes` public method and add to Kanban board using the `openDialog` public method when dragging the list from the Treeview component and dropping it to the kanban board.

{% tab template="kanban/kanban-to-treeview" sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { closest } from '@syncfusion/ej2-base';
import { CardSettingsModel, DragEventArgs, KanbanComponent } from '@syncfusion/ej2-angular-kanban';
import { kanbanData, treeViewData } from './datasource';
import { TreeViewComponent } from '@syncfusion/ej2-angular-navigations';
import { DragAndDropEventArgs } from '@syncfusion/ej2-navigations';
@Component({
  selector: 'app-root',
  template: `<div class="container-fluid">
      <div class="row">
        <div class="col-md-6">
        <h4>Kanban</h4>
        <ejs-kanban id='Kanban' #Kanban keyField='Status' [dataSource]='data' [externalDropId]='externalKanbanDropId'
          [cardSettings]='cardSettings' (dragStop)='onKanbanDragStop($event)'>
          <e-columns>
            <e-column headerText='To do' keyField='Open'></e-column>
              <e-column headerText='Done' keyField='Close'></e-column>
          </e-columns>
        </ejs-kanban>
      </div>
      <div class="col-md-6">
        <h4>TreeView</h4>
        <ejs-treeview id='TreeView' #TreeView [fields]='field' [allowDragAndDrop]='allowDragAndDrop' (nodeDragStop)="onTreeDragStop($event)">
            <ng-template #nodeTemplate="" let-data="">
                <div id="treelist">
                  <div id="treeviewlist">{{data.Id}} - {{data.Status}}</div>
                </div>
            </ng-template>
        </ejs-treeview>
      </div>
     </div>
   </div>`
})
export class AppComponent {
  @ViewChild('Kanban')
  public kanbanObj: KanbanComponent;
  @ViewChild('TreeView')
  public treeObj: TreeViewComponent;
  public data: Object[] = kanbanData;
  public cardSettings: CardSettingsModel = {
    contentField: 'Summary',
    headerField: 'Id'
  };
  public externalKanbanDropId: string[] = ['#TreeView'];
  public field: Object = { dataSource: treeViewData, id: 'Id', text: 'Status' };
  public allowDragAndDrop: boolean = true;
  onKanbanDragStop(args: DragEventArgs) {
    let treeViewElement: Element = <Element>closest(args.event.target as Element, '#TreeView');
    if (treeViewElement) {
      this.kanbanObj.deleteCard(args.data);
      this.treeObj.addNodes(args.data);
      args.cancel = true;
    }
  };
  onTreeDragStop(args: DragAndDropEventArgs) {
    let kanbanElement: Element = <Element>closest(args.event.target as Element, '#Kanban');
    if (kanbanElement) {
      let treeData: { [key: string]: Object }[] =
        this.treeObj.fields.dataSource as { [key: string]: Object }[];
      const filteredData: { [key: string]: Object }[] =
        treeData.filter((item: any) => item.Id === parseInt(args.draggedNodeData.id as string, 10));
      this.treeObj.removeNodes([args.draggedNodeData.id] as string[]);
      this.kanbanObj.openDialog('Add', filteredData[0]);
      args.cancel = true;
    }
  };
}

```

{% endtab %}

### Schedule to Kanban

Drag the card from the Kanban board and drop it to the Schedule component and vice versa.

In the following sample, remove the data from the Kanban board using the `deleteCard` public method and add to the schedule component using the `addNodes` public method at Kanban `dragStop` event when dragging the card and dropping it to the Treeview component. Remove the data from Treeview using the `removeNodes` public method and add to Kanban board using the `addCard` public method when dragging the list from the Treeview component and dropping it to the kanban board.

{% tab template="kanban/kanban-to-schedule" sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { closest, removeClass, extend } from '@syncfusion/ej2-base';
import { CardSettingsModel, DragEventArgs, KanbanComponent } from '@syncfusion/ej2-angular-kanban';
import { kanbanData, scheduleData } from './datasource';
import {
    EventSettingsModel, View, GroupModel, TimelineViewsService, TimelineMonthService,
    ResizeService, WorkHoursModel, DragAndDropService, ResourceDetails, ScheduleComponent, ScheduleDragEventArgs
} from '@syncfusion/ej2-angular-schedule';
@Component({
  selector: 'app-root',
  template: `<div class="container-fluid">
      <div class="row">
        <div class="col-md-4" style="width: 30%">
        <h4>Kanban</h4>
        <ejs-kanban id='Kanban' #Kanban keyField='DepartmentName' [dataSource]='data' [externalDropId]='externalKanbanDropId'
          [cardSettings]='cardSettings' (dragStop)='onKanbanDragStop($event)'>
          <e-columns>
            <e-column headerText='GENERAL' keyField='GENERAL'></e-column>
          </e-columns>
        </ejs-kanban>
      </div>
      <div class="col-md-8" style="width: 70%">
        <h4>Schedule</h4>
        <ejs-schedule id='Schedule' #Schedule width='100%' height='650px' [group]="group" [currentView]="currentView" [selectedDate]="selectedDate" [workHours]="workHours" [eventSettings]="eventSettings" (dragStop)="scheduleDragStop($event)">
                <e-resources>
                    <e-resource field='DepartmentID' title='Department' name='Departments' [dataSource]='departmentDataSource' textField='Text' idField='Id' colorField='Color'>
                    </e-resource>
                    <e-resource field='ConsultantID' title='Consultant' name='Consultants' [dataSource]='consultantDataSource' [allowMultiple]='allowMultiple' textField='Text' idField='Id' groupIDField="GroupId" colorField='Color'>
                    </e-resource>
                </e-resources>
                <ng-template #resourceHeaderTemplate let-data>
                    <div class="template-wrap">
                        <div class="specialist-category">
                            <div class="specialist-name">{{getConsultantName(data)}}</div>
                            <div class="specialist-designation">{{getConsultantDesignation(data)}}</div>
                        </div>
                    </div>
                </ng-template>
                <e-views>
                    <e-view option='TimelineDay'></e-view>
                    <e-view option='TimelineMonth'></e-view>
                </e-views>
            </ejs-schedule>
       </div>
     </div>
   </div>`,
  providers: [TimelineViewsService, TimelineMonthService, ResizeService, DragAndDropService]
})
export class AppComponent {
  @ViewChild('Kanban')
  public kanbanObj: KanbanComponent;
  @ViewChild('Schedule')
  public scheduleObj: ScheduleComponent;
  public data: Object[] = kanbanData;
  public scheduleDataSource: Object[] = <Object[]>extend([], scheduleData, null, true);
  public cardSettings: CardSettingsModel = {
    contentField: 'Name',
    headerField: 'Id'
  };
  public externalKanbanDropId: string[] = ['#Schedule'];
  public selectedDate: Date = new Date(2018, 7, 1);
    public currentView: View = 'TimelineDay';
    public workHours: WorkHoursModel = { start: '08:00', end: '18:00' };
  public departmentDataSource: Object[] = [
        { Text: 'GENERAL', Id: 1, Color: '#bbdc00' },
        { Text: 'DENTAL', Id: 2, Color: '#9e5fff' }
    ];
    public consultantDataSource: Object[] = [
        { Text: 'Alice', Id: 1, GroupId: 1, Color: '#bbdc00', Designation: 'Cardiologist' },
        { Text: 'Nancy', Id: 2, GroupId: 2, Color: '#9e5fff', Designation: 'Orthodontist' },
        { Text: 'Robert', Id: 3, GroupId: 1, Color: '#bbdc00', Designation: 'Optometrist' },
        { Text: 'Robson', Id: 4, GroupId: 2, Color: '#9e5fff', Designation: 'Periodontist' },
        { Text: 'Laura', Id: 5, GroupId: 1, Color: '#bbdc00', Designation: 'Orthopedic' },
        { Text: 'Margaret', Id: 6, GroupId: 2, Color: '#9e5fff', Designation: 'Endodontist' }
    ];
    public group: GroupModel = { enableCompactView: false, resources: ['Departments', 'Consultants'] };
    public allowMultiple: Boolean = false;
    public eventSettings: EventSettingsModel = {
        dataSource: this.scheduleDataSource,
        fields: {
            subject: { title: 'Patient Name', name: 'Name' },
            startTime: { title: 'From', name: 'StartTime' },
            endTime: { title: 'To', name: 'EndTime' },
            description: { title: 'Reason', name: 'Description' }
        }
    };

  getConsultantName(value: ResourceDetails): string {
        return (value as ResourceDetails).resourceData[(value as ResourceDetails).resource.textField] as string;
    }

    getConsultantStatus(value: ResourceDetails): boolean {
        let resourceName: string =
            (value as ResourceDetails).resourceData[(value as ResourceDetails).resource.textField] as string;
        if (resourceName === 'GENERAL' || resourceName === 'DENTAL') {
            return false;
        } else {
            return true;
        }
    }

    getConsultantDesignation(value: ResourceDetails): string {
        let resourceName: string =
            (value as ResourceDetails).resourceData[(value as ResourceDetails).resource.textField] as string;
        if (resourceName === 'GENERAL' || resourceName === 'DENTAL') {
            return '';
        } else {
            return (value as ResourceDetails).resourceData.Designation as string;
        }
    }

    getConsultantImageName(value: ResourceDetails): string {
        return this.getConsultantName(value).toLowerCase();
    }

    onKanbanDragStop(args: DragEventArgs) {
    let scheduleElement: Element = <Element>closest(args.event.target as Element, '#Schedule');
        if (scheduleElement) {
            this.kanbanObj.deleteCard(args.data);
            this.scheduleObj.openEditor(args.data[0], 'Add', true);
            args.cancel = true;
        }
    };
    scheduleDragStop(args: ScheduleDragEventArgs) {
    let kanbanElement: Element = <Element>closest(args.event.target as Element, '#Kanban');
        if (kanbanElement) {
            this.scheduleObj.deleteEvent(args.data.Id);
             removeClass([this.scheduleObj.element.querySelector('.e-selected-cell')], 'e-selected-cell');
             this.kanbanObj.openDialog('Add', args.data);
             args.cancel = true;
        }
    };
}

```

{% endtab %}
