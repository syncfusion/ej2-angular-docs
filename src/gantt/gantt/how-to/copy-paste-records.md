---
title: "How To"
component: "Gantt"
description: "Learn how to copy and paste records in Gantt control."
---

# Copy and Paste records in Gantt

You can copy and paste a record in the Gantt chart by using the `addRecord` method and `custom context menu`. It is also possible to copy and paste the parent record with multiple hierarchical child records on the required position.

{% tab template="gantt/how-to/copypaste",sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { Gantt } from '@syncfusion/ej2-gantt';
import { GanttComponent, ContextMenuClickEventArgs, ContextMenuOpenEventArgs } from '@syncfusion/ej2-angular-gantt';
import { ContextMenuItemModel } from '@syncfusion/ej2-grids';
import { editingData} from './data';

@Component({
    selector: 'app-root',
    template:
       `<ejs-gantt #customcontextmenu id="ganttCustomContextmenu" height="430px" [dataSource]="editingData" [taskFields]="taskSettings" [enableContextMenu]="true" [contextMenuItems]="contextMenuItems" [editSettings]="editSettings" (contextMenuClick)="contextMenuClick($event)" (contextMenuOpen)="contextMenuOpen($event)"></ejs-gantt>`,
    encapsulation: ViewEncapsulation.None
})

export class AppComponent{
    // Data for Gantt
    public copiedRecord: any;
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
       this.contextMenuItems = [{ text: 'Copy', target: '.e-content', id: 'copy' } as ContextMenuItemModel,
        { text: 'Paste', target: '.e-content', id: 'paste' } as ContextMenuItemModel,
        ];
    }
    public contextMenuClick (args: ContextMenuClickEventArgs) {
        if (args.item.id === 'copy') {
            this.copiedRecord = args.rowData;
            this.copiedRecord.taskData.TaskID = this.ganttObj.currentViewData.length + 1;
        }
        if (args.item.id === 'paste') {
            this.ganttObj.addRecord(this.copiedRecord.taskData,'Below',args.rowData.index);
            if(this.copiedRecord.hasChildRecords) {
                addChildRecords(this.copiedRecord, args.rowData.index + 1);
            }
            this.copiedRecord = undefined;
        }
    }
    public contextMenuOpen (args: ContextMenuOpenEventArgs) {
        if (args.type !== 'Header') {
            if (this.copiedRecord) {
                args.hideItems.push('Copy');
            } else {
                args.hideItems.push('Paste');
             }
        }
    }
}

function addChildRecords(record, index): void {
    for(var i=0; i<record.childRecords.length; i++) {
          var childRecord = record.childRecords[i];
          childRecord.taskData.TaskID = this.ganttObj.currentViewData.length + 1;
          this.ganttObj.addRecord(childRecord.taskData,'Child',index);
          if(childRecord.hasChildRecords) {
              addChildRecords(childRecord, index + (i+1));
          }
    }
  }

```

{% endtab %}