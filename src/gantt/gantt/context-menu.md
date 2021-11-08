---
title: "Context Menu"
component: "Gantt"
description: "Learn how to use the context menu and add custom context menu items in the Essential JS 2 Gantt control."
---

# Context menu

The Gantt control allows you to perform quick actions by using context menu. When right-clicking the context menu, the context menu options are shown. To enable this feature, set the [`enableContextMenu`](../api/gantt/#enablecontextmenu) to true. The default context menu options are enabled using the [`editSettings`](../api/gantt/#editsettings) property. The context menu options can be customized using the [`contextMenuItems`](../api/gantt/#contextmenuitems) property.

To use the context menu, inject the `ContextMenuService` in the provider section of `AppModule`.

The default items are listed in the following table.

Items| Description
----|----
`AutoFit`|  Auto-fits the current column.
`AutoFitAll` | Auto-fits all columns.
`SortAscending` | Sorts the current column in ascending order.
`SortDescending` | Sorts the current column in descending order.
`TaskInformation`|  Edits the current task.
`Add` | Adds a new row to the Gantt.
`Indent` | Indent the selected record to one level.
`Outdent` | Outdent the selected record to one level.
`DeleteTask` | Deletes the current task.
`Save` | Saves the edited task.
`Cancel` | Cancels the edited task.
`DeleteDependency` | Deletes the current dependency task link.
`Convert` | Converts current task to milestone or vice-versa.
{% tab template="gantt/contextmenu/default",sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { editingData} from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt id="ganttContextmenu" height="430px" [dataSource]="editingData" [taskFields]="taskSettings" [enableContextMenu]="true" [allowSorting]="true" [allowResizing]="true" [editSettings]="editSettings"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})

export class AppComponent{
    // Data for Gantt
    public editingData: object[];
    public taskSettings: object;
    public editSettings: object;
    public ngOnInit(): void {
        this.editingData = editingData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            dependency: 'Predecessor',
            child: 'subtasks'
        };
        this.editSettings = {
        allowAdding: true,
        allowEditing: true,
        allowDeleting: true
       };
    }
}

```

{% endtab %}

## Custom context menu items

The custom context menu items can be added by defining the [`contextMenuItems`](../api/gantt/#contextmenuitems) as a collection of [`contextMenuItemModel`](../api/grid/contextMenuItemModel/).
Actions for the customized items can be defined in the [`contextMenuClick`](../api/gantt/#contextmenuclick) event and the visibility of customized items can be defined in the [`contextMenuOpen`](../api/gantt/#contextmenuopen) event.

To create custom context menu items for header area, define the target property as `.e-gridheader`.

The following sample shows context menu item for parent rows to expand or collapse child rows in the content area and a context menu item to hide columns in the header area.

{% tab template="gantt/contextmenu/custom",sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { GanttComponent, ContextMenuClickEventArgs, ContextMenuOpenEventArgs } from '@syncfusion/ej2-angular-gantt';
import { ContextMenuItemModel } from '@syncfusion/ej2-grids';
import { editingData} from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt #customcontextmenu id="ganttCustomContextmenu" height="430px" [dataSource]="editingData" [taskFields]="taskSettings" [enableContextMenu]="true" [contextMenuItems]="contextMenuItems" [allowSorting]="true" [allowResizing]="true" [editSettings]="editSettings" (contextMenuClick)="contextMenuClick($event)" (contextMenuOpen)="contextMenuOpen($event)"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})

export class AppComponent{
    // Data for Gantt
    public editingData: object[];
    public taskSettings: object;
    public editSettings: object;
    public contextMenuItems: (string | ContextMenuItemModel)[];
    @ViewChild('customcontextmenu', {static: true})
    public ganttObj: GanttComponent;
    public ngOnInit(): void {
        this.editingData = editingData;
        this.taskSettings = {
            id: 'TaskID',
            name: 'TaskName',
            startDate: 'StartDate',
            duration: 'Duration',
            progress: 'Progress',
            dependency: 'Predecessor',
            child: 'subtasks'
        };
        this.editSettings = {
        allowAdding: true,
        allowEditing: true,
        allowDeleting: true
       };
       this.contextMenuItems = ['AutoFitAll', 'AutoFit', 'TaskInformation', 'DeleteTask', 'Save', 'Cancel', 'SortAscending', 'SortDescending', 'Add', 'DeleteDependency', 'Convert',
        { text: 'Collapse the Row', target: '.e-content', id: 'collapserow' } as ContextMenuItemModel,
        { text: 'Expand the Row', target: '.e-content', id: 'expandrow' } as ContextMenuItemModel,
        { text: 'Hide Column', target: '.e-gridheader', id: 'hidecols' } as ContextMenuItemModel
        ];
    }

    public contextMenuClick (args: ContextMenuClickEventArgs) {
        let record = args.rowData;
        if (args.item.id === 'collapserow') {
            this.ganttObj.collapseByID(Number(record.ganttProperties.taskId));
            }
        if (args.item.id === 'expandrow') {
            this.ganttObj.expandByID(Number(record.ganttProperties.taskId));
            }
        if (args.item.id === 'hidecols') {
            this.ganttObj.hideColumn(args.column.headerText);
        }
    }
    public contextMenuOpen (args: ContextMenuOpenEventArgs) {
        let record = args.rowData;
            if (args.type !== 'Header') {
                if (!record.hasChildRecords) {
                    args.hideItems.push('Collapse the Row');
                    args.hideItems.push('Expand the Row');
                } else {
                    if(record.expanded){
                        args.hideItems.push("Expand the Row");
                    } else {
                        args.hideItems.push("Collapse the Row");
                    }
                }
        }
    }
}

```

{% endtab %}

> You can show an specific item in context menu for header/content area in the Gantt control by defining the `target` property.