---
title: "How To"
component: "Gantt"
description: "Learn how to set new row position while adding new records in Gantt control."
---

# Set new row position in Gantt

In Gantt, a new row can be added in one of the following positions: Top, Bottom, Above, Below and Child. This position can be specified through the `newRowPostion` property. We can make use of the toolbarClick event to create a context menu that specifies the position in which the new row is to be added when adding a record through toolbar click.

The following code snippets demonstrate how to achieve this.

{% tab template="gantt/how-to/newrow",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { ToolbarItem, EditSettingsModel } from '@syncfusion/ej2-angular-gantt';
import { MenuItemModel, ContextMenu } from '@syncfusion/ej2-navigations';
import { Gantt } from '@syncfusion/ej2-gantt';

@Component({
    selector: 'app-root',
    template:
    `<ejs-contextmenu id='contextmenu' [items]= 'menuItems' (select)="select($event)"></ejs-contextmenu>`
       `<ejs-gantt id="ganttDefault" height="430px" [dataSource]="data" [taskFields]="taskSettings" [editSettings]="editSettings" [toolbar]="toolbar" (toolbarClick)="toolbarClick($event)"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent{
    // Data for Gantt
    public data: object[];
    public taskSettings: object;
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItem[];
    @ViewChild('gantt', {static: true})
    public ganttObj: GanttComponent;
    public ngOnInit(): void {
        this.data =  [
            {
                TaskID: 1,
                TaskName: 'Project Initiation',
                StartDate: new Date('04/02/2019'),
                EndDate: new Date('04/21/2019'),
                subtasks: [
                    {  TaskID: 2, TaskName: 'Identify Site location', StartDate: new Date('04/02/2019'), Duration: 4, Progress: 50 },
                    { TaskID: 3, TaskName: 'Perform Soil test', StartDate: new Date('04/02/2019'), Duration: 4, Progress: 50  },
                    { TaskID: 4, TaskName: 'Soil test approval', StartDate: new Date('04/02/2019'), Duration: 4, Progress: 50 },
                ]
            },
            {
                TaskID: 5,
                TaskName: 'Project Estimation',
                StartDate: new Date('04/02/2019'),
                EndDate: new Date('04/21/2019'),
                subtasks: [
                    { TaskID: 6, TaskName: 'Develop floor plan for estimation', StartDate: new Date('04/04/2019'), Duration: 3, Progress: 50 },
                    { TaskID: 7, TaskName: 'List materials', StartDate: new Date('04/04/2019'), Duration: 3, Progress: 50 },
                    { TaskID: 8, TaskName: 'Estimation approval', StartDate: new Date('04/04/2019'), Duration: 3, Progress: 50 }
                ]
            },
        ];
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            child: 'subtasks'
        };
        this.editSettings = {
            allowAdding:true
            };
            this.toolbar = ['Add'];
    }
    public menuItems: MenuItemModel[] = [
        {
            text: 'Bottom'
        },
        {
            text: 'Above'
        },
        {
            text: 'Below'
        },
        {
            text: 'Child'
        },
        {
            text: 'Top'
        }];
        public select(args: any) {
            if (args.item.text === "Bottom") {
            ganttObj.editSettings.newRowPosition = "Bottom";
            ganttObj.openAddDialog();
        } else if (args.item.text === "Above") {
            if (ganttObj.selectedRowIndex == -1) {
                alert("Please select any row");
            } else {
                ganttObj.editSettings.newRowPosition = "Above";
                ganttObj.openAddDialog();
            }
        } else if (args.item.text === "Below") {
            if (ganttObj.selectedRowIndex == -1) {
                alert("Please select any row");
            } else {
                ganttObj.editSettings.newRowPosition = "Below";
                ganttObj.openAddDialog();
            }
        } else if (args.item.text === "Child") {
            if (ganttObj.selectedRowIndex == -1) {
                alert("Please select any row");
            } else {
                ganttObj.editSettings.newRowPosition = "Child";
                ganttObj.openAddDialog();
            }
        } else if (args.item.text === "Top") {
            ganttObj.editSettings.newRowPosition = "Top";
            ganttObj.openAddDialog();
        }
        }
    public toolbarClick(args: ClickEventArgs): void {
            if (args.item.id === 'ganttDefault_add') {
                let contextmenuObj: ContextMenu = getInstance(document.getElementById("contextmenu_0"), ContextMenu) as ContextMenu;
                contextmenuObj.open(40, 20);
            }
    };
}

```

{% endtab %}