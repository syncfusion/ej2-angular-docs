---
title: "Clipboard"
component: "TreeGrid"
description: "Learn how to use the copy to clipboard functionality in the Essential JS 2 Tree Grid Control."
---

# Clipboard

The clipboard provides an option to copy selected rows or cells data into the clipboard.

The following list of keyboard shortcuts is supported in the Tree Grid to copy selected rows or cells data into clipboard.

Interaction keys |Description
-----|-----
<kbd>Ctrl + C</kbd> |Copy selected rows or cells data into clipboard.
<kbd>Ctrl + Shift + H</kbd> |Copy selected rows or cells data with header into clipboard.

{% tab template="treegrid/clipboard", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { SelectionSettingsModel } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' [allowSelection]='true' [allowPaging]='true' height='260' [selectionSettings]='selectionOptions' [pageSettings]='pageSettings' childMapping='subtasks' [treeColumnIndex]='1'>
        <e-columns>
            <e-column field='taskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
            <e-column field='taskName' headerText='Task Name' width='200'></e-column>
            <e-column field='startDate' headerText='Start Date' width='100' format="yMd" textAlign='Right'></e-column>
            <e-column field='duration' headerText='Duration' width='90' textAlign='Right'></e-column>
            <e-column field='progress' headerText='Progress' width='90' textAlign='Right'></e-column>
        </e-columns>
    </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public selectionOptions: SelectionSettingsModel;
    public pageSettings: Object ;

    ngOnInit(): void {
        this.data = sampleData;
        this.selectionOptions = { type: 'Multiple'};
        this.pageSettings = {pageSize: 10};
    }
}
```

{% endtab %}

## Copy to clipboard by external buttons

To copy selected rows or cells data into clipboard with help of external buttons, you need to invoke the [`copy`](../../api/treegrid/clipboard/#copy) method.

{% tab template="treegrid/copy-method", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';
import { sampleData } from './datasource';
import { TreeGridComponent, SelectionSettingsModel  } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template:
    `<button ej-button id='copy' (click)='copy()'>Copy</button>
     <button ej-button id='copyHeader' (click)='copyHeader()'>CopyHeader</button>
        <ejs-treegrid #treegrid [dataSource]='data' [allowSelection]='true' [allowPaging]='true' height='230' [selectionSettings]='selectionOptions' [pageSettings]='pageSettings' childMapping='subtasks' [treeColumnIndex]='1'>
        <e-columns>
            <e-column field='taskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
            <e-column field='taskName' headerText='Task Name' width='200'></e-column>
            <e-column field='startDate' headerText='Start Date' width='100' format="yMd" textAlign='Right'></e-column>
            <e-column field='duration' headerText='Duration' width='90' textAlign='Right'></e-column>
            <e-column field='progress' headerText='Progress' width='90' textAlign='Right'></e-column>
        </e-columns>
    </ejs-treegrid>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent implements OnInit {

    public data: Object[];
    public selectionOptions: SelectionSettingsModel;
    public pageSettings: Object ;
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;
        this.selectionOptions = { type: 'Multiple'};
        this.pageSettings = {pageSize: 10};
    }

    copy() {
        this.treeGridObj.copy();
    }

    copyHeader() {
        this.treeGridObj.copy(true);
    }
}
```

{% endtab %}

## Copy Hierarchy Modes

Tree Grid provides support for a set of copy modes with [`copyHierarchyMode`](../api/treegrid/#copyHierarchymode) property. The below are the type of filter mode available in TreeGrid.

* **Parent** : This is the default copy hierarchy mode in Tree Grid. Clipboard value have the selected records with its parent records. If the selected records not have any parent record then the selected record will be in clipboard.

* **Child** : Clipboard value have the selected records with its child record. If the selected records do not have any child record then the selected records will be in clipboard.

* **Both** : Clipboard value have the selected records with its both parent and child record. If the selected records do not have any parent and child record then the selected records alone in clipboard.

* **None** : Only the Selected records will be in clipboard.

{% tab template="treegrid/clipboard", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';
import { sampleData } from './datasource';
import { ChangeEventArgs } from '@syncfusion/ej2-angular-dropdowns';
import { TreeGridComponent  } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template:
    `<div style="padding-top: 7px; float:left">Hierarchy Mode</div><div style="padding-left: 10px; display: inline-block"><ejs-dropdownlist (change)='onChange($event)' [dataSource]='dropData' value='Parent' [fields]='fields'></ejs-dropdownlist></div>
        <ejs-treegrid #treegrid [dataSource]='data' [allowSelection]='true' [allowPaging]='true' height='230' copyHierarchyMode='Parent' [selectionSettings]='selectionOptions' [pageSettings]='pageSettings' childMapping='subtasks' [treeColumnIndex]='1'>
        <e-columns>
            <e-column field='taskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
            <e-column field='taskName' headerText='Task Name' width='200'></e-column>
            <e-column field='startDate' headerText='Start Date' width='100' format="yMd" textAlign='Right'></e-column>
            <e-column field='duration' headerText='Duration' width='90' textAlign='Right'></e-column>
            <e-column field='progress' headerText='Progress' width='90' textAlign='Right'></e-column>
        </e-columns>
    </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public dropData: Object[];
    public fields: Object;
    public selectionOptions: SelectionSettingsModel;
    public pageSettings: Object ;
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;
         this.dropData = [
        { id: 'Parent', mode: 'Parent' },
        { id: 'Child', mode: 'Child' },
        { id: 'Both', mode: 'Both' },
        { id: 'None', mode: 'None' },
    ];
    this.fields = { text: 'mode', value: 'id' };
    this.selectionOptions = { type: 'Multiple'};
    this.pageSettings = {pageSize: 10};
    }

    onChange(e: ChangeEventArgs): any {
        let mode: any = <string>e.value;
        this.treeGridObj.copyHierarchyMode = mode;
    }
}
```

{% endtab %}

### Limitations of Copy Functionality

* Only current view records will be available in copy clipboard.

## AutoFill

AutoFill Feature allows you to copy the data of selected cells and paste it to another cells by just dragging the autofill icon of the selected cells up to required cells. This feature is enabled by defining `enableAutoFill` property as true.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { SelectionSettingsModel, EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' [enableAutoFill]='true'  [enableHover]='false' [allowPaging]='true' [pageSettings]='pageSettings' [editSettings]='editSettings' [allowSelection]='true' [toolbar]='toolbar' [selectionSettings]='selectionOptions' height='220' childMapping='subtasks' [treeColumnIndex]='1'>
                <e-columns>
                    <e-column field='taskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
                    <e-column field='taskName' headerText='Task Name' width='200'></e-column>
                    <e-column field='startDate' headerText='Start Date' width='100' format="yMd" textAlign='Right'></e-column>
                    <e-column field='duration' headerText='Duration' width='90' textAlign='Right'></e-column>
                    <e-column field='progress' headerText='Progress' width='90' textAlign='Right'></e-column>
                </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public selectionOptions: SelectionSettingsModel;
    public editSettings: EditSettingsModel;
    public pageSettings: Object ;
    public toolbar: ToolbarItems[];

    ngOnInit(): void {
        this.data = sampleData;
        this.selectionOptions = { type: 'Multiple', mode: 'Cell', cellSelectionMode: 'Box' };
        this.editSettings= { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Batch' },
        this.toolbar = ['Add', 'Update', 'Cancel'];
        this.pageSettings = {pageSize: 10};
    }
}
```

{% endtab %}

> * If `enableAutoFill` is set to true, then the autofill icon will be displayed on cell selection to copy cells.
> * It requires the selection `mode` to be `Cell`, `cellSelectionMode` to be `Box` and also Batch Editing should be enabled.

### Limitations of AutoFill

* Since the string values are not parsed to number and date type, so when the selected string type cells are dragged to number type cells then it will display as **NaN**. For date type cells, when the selected string type cells are dragged to date type cells then it will display as an **empty cell**.
* Linear series and the sequential data generations are not supported in this autofill feature.

## Paste

You can able to copy the content of a cell or a group of cells by selecting the cells and pressing <kbd>Ctrl + C</kbd> shortcut key and paste it to another set of cells by selecting the cells and pressing <kbd>Ctrl + V</kbd> shortcut key.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { SelectionSettingsModel, EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data' height='220' [enableHover]='false' [allowPaging]='true' [pageSettings]='pageSettings' [editSettings]='editSettings' [toolbar]='toolbar' [allowSelection]='true' [selectionSettings]='selectionOptions' childMapping='subtasks' [treeColumnIndex]='1'>
                <e-columns>
                    <e-column field='taskID' headerText='Task ID' width='70' textAlign='Right'></e-column>
                    <e-column field='taskName' headerText='Task Name' width='200'></e-column>
                    <e-column field='startDate' headerText='Start Date' width='100' format="yMd" textAlign='Right'></e-column>
                    <e-column field='duration' headerText='Duration' width='90' textAlign='Right'></e-column>
                    <e-column field='progress' headerText='Progress' width='90' textAlign='Right'></e-column>
                </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public selectionOptions: SelectionSettingsModel;
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];

    ngOnInit(): void {
        this.data = sampleData;
        this.selectionOptions = { type: 'Multiple', mode: 'Cell', cellSelectionMode: 'Box' };
        this.editSettings= { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Batch' },
        this.toolbar = ['Add', 'Update', 'Cancel'];
    }
}
```

{% endtab %}

> To perform paste functionality, it requires the selection `mode` to be `Cell`,  `cellSelectionMode` to be `Box` and also Batch Editing should be enabled.

### Limitations of Paste Functionality

* Since the string values are not parsed to number and date type, so when the copied string type cells are pasted to number type cells then it will display as **NaN**. For date type cells, when the copied string format cells are pasted to date type cells then it will display as an **empty cell**.