---
title: "Editing"
component: "TreeGrid"
description: "Learn how to perform CRUD operations in various edit modes, and use different cell editors in the Essential JS 2 TreeGrid control."
---

# Editing

The TreeGrid component has options to dynamically insert, delete and update records.
Editing feature is enabled by using [`editSettings`](../api/treegrid/#editsettings) property and it requires a primary key column for CRUD operations.
To define the primary key, set [`columns.isPrimaryKey`](../api/treegrid/column/#isprimarykey) to `true` in particular column.

To use CRUD, inject the [`Edit`](../api/treegrid/#editmodule) module in treegrid.

You can check this video to learn about editing modes and editing types in Angular TreeGrid.

`youtube:Y1XKjCWiIB4`

{% tab template="treegrid/edit", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='priority' headerText='Priority' textAlign='Right' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Cell' };
    }
}

```

{% endtab %}

> * You can disable editing for a particular column, by specifying
[`columns.allowEditing`](../api/treegrid/column/#allowediting) to `false`.

## Toolbar with edit option

The treegrid toolbar has the built-in items to execute Editing actions.
You can define this by using the [`toolbar`](../api/treegrid/#toolbar) property.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='priority' headerText='Priority' textAlign='Right' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
        this.toolbarOptions = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
}

```

{% endtab %}

## Cell edit type and its params

The [`columns.editType`](../api/treegrid/column/#edittype) is used to customize the edit type of the particular column.
You can set the [`columns.editType`](../api/treegrid/column/#edittype) based on data type of the column.

* `numericedit` - [`NumericTextBox`](../numerictextbox) component for integers, double, and decimal data types.

* `defaultedit` - [`TextBox`](../textbox) component for string data type.

* `dropdownedit` - [`DropDownList`](../drop-down-list) component for list data type.

* `booleanedit` - [`CheckBox`](../check-box) component for boolean data type.

* `datepickeredit` - [`DatePicker`](../datepicker) component for date data type.

* `datetimepickeredit` - [`DateTimePicker`](../datetimepicker) component for date time data type.

Also, you can customize model of the [`columns.editType`](../api/treegrid/column/#edittype) component through the [`columns.edit.params`](../api/treegrid/column/#edit).

The following table describes cell edit type component and their corresponding edit params of the column.

Component |Example
-----|-----
[`NumericTextBox`](../numerictextbox) | params: { decimals: 2, value: 5 }
[`TextBox`](../textbox) | -
[`DropDownList`](../drop-down-list) | params: { value: 'Germany' }
[`Checkbox`](../check-box) | params: { checked: true}
[`DatePicker`](../datepicker) | params: { format:'dd.MM.yyyy' }
[`DateTimePicker`](../datetimepicker) | params: { value: new Date() }

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' editType='stringedit' textAlign='Left' width=180></e-column>
                    <e-column field='approved' headerText='Approved' editType='booleanedit' type='boolean' textAlign='Right' [displayAsCheckBox]='true' width=110></e-column>
                    <e-column field='priority' headerText='Priority' editType='dropdownedit' textAlign='Right' width=110></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' [format]='formatOptions' editType='datetimepickeredit' [edit]='editOptions' width=180></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' editType='numericedit' width=120 [edit]='editing'></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    public editing: Object;
    public formatOptions: Object;
    public editOptions: Object;
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
        this.toolbarOptions = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
        this.editing = { params: { format: 'n' } };
        this.formatOptions = { format: 'M/d/y hh:mm a', type: 'dateTime' };
        this.editOptions = { params: { format: 'M/d/y hh:mm a' } };
    }
}

```

{% endtab %}

> If edit type is not defined in the column, then it will be considered as the `stringedit` type (Textbox component).

## Cell Edit Template

The cell edit template is used to add a custom component for a particular column by invoking the following functions:

* `create` - It is used to create the element at the time of initialization.

* `write` - It is used to create the custom component or assign default value at the time of editing.

* `read` - It is used to read the value from the component at the time of save.

* `destroy` - It is used to destroy the component.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel } from '@syncfusion/ej2-angular-treegrid';
import { AutoComplete } from '@syncfusion/ej2-dropdowns';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data'  [treeColumnIndex]='1' height='315' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' editType='stringedit' [edit]='editOptions' textAlign='Left' width=180></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right'type='date'format='yMd'editType='datepickeredit' width=180></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public editOptions: Object;
    public elem: HTMLElement;
    public autoCompleteObj: AutoComplete;
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;

    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, newRowPosition: 'Below', mode: 'Cell' };
        this.editOptions = {
                create: () => {
                    this.elem = document.createElement('input');
                    return this.elem;
                },
                read: () => {
                    return this.autoCompleteObj.value;
                },
                destroy: () => {
                    this.autoCompleteObj.destroy();
                },
                write: (args: { rowData: Object, column: Column }) => {
                    this.autoCompleteObj = new AutoComplete({
                        dataSource: <{key: string, value: any}[]>this.treeGridObj.grid.dataSource,
                        fields: { value: 'taskName' },
                        value: args.rowData[args.column.field]
                    });
                    this.autoCompleteObj.appendTo(this.elem);
                }
            };
    }
}

```

{% endtab %}

## Edit Modes

TreeGrid supports the following types of edit modes, they are:

* Cell
* Row
* Dialog
* Batch

### Cell

In Cell edit mode, when you double click on a cell, it is changed to edit state.
You can change the cell value and save to the data source.
To enable Cell edit, set the [`editSettings.mode`](../api/treegrid/editSettingsModel/#mode) as `Cell`.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='priority' headerText='Priority' textAlign='Right' width=90></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' type='date' editType='datepickeredit' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Cell' };
        this.toolbarOptions = ['Add', 'Delete', 'Update', 'Cancel'];
    }
}

```

{% endtab %}

> Cell edit mode is default mode of editing.

### Row

In Row edit mode, when you start editing the currently selected record, the entire row is changed to edit state.
You can change the cell values of the row and save edited data to the data source.
To enable Row edit, set the [`editSettings.mode`](../api/treegrid/editSettingsModel/#mode) as `Row`.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='priority' headerText='Priority' textAlign='Right' width=90></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' type='date' editType='datepickeredit' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
        this.toolbarOptions = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
}

```

{% endtab %}

### Dialog

In Dialog edit mode, when you start editing the currently selected row, data will be shown on a dialog.
You can change the cell values and save edited data to the data source.
To enable Dialog edit, set the [`editSettings.mode`](../api/treegrid/editSettingsModel/#mode) as `Dialog`.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='priority' headerText='Priority' textAlign='Right' width=90></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' type='date' editType='datepickeredit' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
        this.toolbarOptions = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
}

```

{% endtab %}

### Batch

In Batch edit mode, when you double-click on the tree grid cell, then the target cell changed to edit state. You can bulk save (added, changed and deleted data in the single request) to data source by click on the toolbar's `Update` button or by externally invoking the [`batchSave`](../api/treegrid/edit/#batchsave) method. To enable Batch edit, set the [`editSettings.mode`](../api/treegrid/editSettings/#mode) as `Batch`.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { projectData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data' parentIdMapping='parentID' idMapping='TaskID' [toolbar]='toolbar' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' >
        <e-columns>
                    <e-column field='TaskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='TaskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='Priority' headerText='Priority' textAlign='Right' width=90></e-column>
                    <e-column field='StartDate' headerText='Start Date' textAlign='Right' format='yMd' type='date' editType='datepickeredit' width=90></e-column>
                    <e-column field='Duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];

    ngOnInit(): void {
        this.data = projectData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Batch' };
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
}

```

{% endtab %}

## Forms

### Reactive Forms

[`Reactive`](https://angular.io/guide/reactive-forms) Forms is a model-driven approach to create and manipulate the form controls. You can use reactive form to add and update treegrid records. To use reactive forms for editing operation, you can take leverage of the template support of dialog or inline edit mode. Setting the [`editSettings.mode`](../api/treegrid/editSettingsModel/#mode) as `Row/Dialog` and `editSettingsTemplate` as template variable of NgTemplate to define the treegrid editors.

In the below sample, We have created the `FormGroup` with `FormControls` for each columns, in the [`actionBegin`](../api/treegrid/#actionbegin)  event. While saving, we have validated the formgroup and updated the treegrid with the edited data from the FormGroup object.

{% tab template="treegrid/edit-dlg-react", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';
import { DialogEditEventArgs, SaveEventArgs } from '@syncfusion/ej2-angular-grids';
import { Dialog } from '@syncfusion/ej2-angular-popups';
import { FormGroup, AbstractControl, FormControl, Validators } from '@angular/forms';
import { DataUtil } from '@syncfusion/ej2-data';
import { ReactiveFormsModule ,  FormsModule} from '@angular/forms';
import { Browser } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-container',
   template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [toolbar]='toolbar' [editSettings]='editSettings' childMapping='subtasks' (actionBegin)="actionBegin($event)" (actionComplete)="actionComplete($event)">
    <e-columns>
        <e-column field='taskID' headerText='Task ID' width='120' textAlign='Right' isPrimaryKey='true' ></e-column>
        <e-column field='taskName' headerText='Task Name' width='225' ></e-column>
        <e-column field='startDate' headerText='Start Date' width='150' format="yMd" ></e-column>
        <e-column field='duration' headerText='Duration' width='90'   textAlign='Right' ></e-column>
        <e-column field='progress' headerText='Progress' width='90' textAlign='Right' ></e-column>
    </e-columns>

    <ng-template #editSettingsTemplate let-data>
            <div [formGroup]="taskForm">
                <div class="form-row">
                    <div class="form-group col-md-6">
                        <div class="e-float-input e-control-wrapper" [ngClass]="{'e-error': taskID.invalid && (taskID.dirty || taskID.touched)}">
                            <input formControlName="taskID" data-msg-containerid='taskIDError' id="taskID" name="taskID" type="text" [attr.disabled]="!data.isAdd ? '' : null">
                            <span class="e-float-line"></span>
                            <label class="e-float-text e-label-top" for="taskID"> Task ID</label>
                        </div>
                        <div id="taskIDError" [style.visibility]='((taskID.invalid && (taskID.dirty || taskID.touched)) || (taskID.invalid && submitClicked))? "visible": "hidden"'>
                            <label class="e-error" for="taskID" id="taskID-info" style="display: block;">*Task ID is required</label>
                        </div>
                    </div>
                    <div class="form-group col-md-6">
                        <div class="e-float-input e-control-wrapper" [ngClass]="{'e-error': taskName.invalid && (taskName.dirty || taskName.touched)}">
                            <input formControlName="taskName" data-msg-containerid='taskNameError' id="taskName" name="taskName" type="text">
                            <span class="e-float-line"></span>
                            <label class="e-float-text e-label-top" for="taskName">Task Name</label>
                        </div>
                        <div id="taskNameError" [style.visibility]='((taskName.invalid && (taskName.dirty || taskName.touched)) || (taskName.invalid && submitClicked))? "visible": "hidden"'>
                            <label class="e-error" for="taskName" id="taskName-info" style="display: block;">*Task Name is required</label>
                        </div>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group col-md-6">
                        <ejs-numerictextbox formControlName="duration" id="duration" placeholder="Duration" format="##" floatLabelType='Always'></ejs-numerictextbox>
                    </div>
                    <div class="form-group col-md-6">
                        <ejs-datepicker id="startDate" formControlName="startDate" placeholder="Start Date" floatLabelType='Always'></ejs-datepicker>
                        <div id="startDateError" [style.visibility]='((startDate.invalid && (startDate.dirty || startDate.touched)) || (startDate.invalid && submitClicked)) ? "visible": "hidden"'>
                            <label class="e-error" for="startDate" id="startDate-info" style="display: block;">*Start Date is required</label>
                        </div>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group col-md-6">
                        <ejs-dropdownlist id="progress" formControlName="progress" [dataSource]='progressDistinctData' [fields]="{text: 'progress', value: 'progress' }" placeholder="Progress" popupHeight='300px' floatLabelType='Always'></ejs-dropdownlist>
                    </div>
                </div>
            </div>
        </ng-template>
</ejs-treegrid>`,
})
export class AppComponent implements OnInit {
    public data: Object[] = [];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    public taskForm: FormGroup;
    public progressDistinctData: Object;
    public priorityDistinctData: Object;
    public submitClicked: boolean = false;

    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true , mode: 'Dialog' , newRowPosition: 'Below'};
        this.toolbarOptions = ['Add', 'Edit', 'Delete'];
        this.progressDistinctData = DataUtil.distinct(sampleData, 'progress', true);
        this.priorityDistinctData = DataUtil.distinct(sampleData, 'priority', true );
    }

    createFormGroup(data: ITaskModel): FormGroup {
        return new FormGroup({
            taskID: new FormControl(data.taskID, Validators.required),
            startDate: new FormControl(data.startDate, this.dateValidator()),
            taskName: new FormControl(data.taskName, Validators.required),
            duration: new FormControl(data.duration),
            progress: new FormControl(data.progress),
            priority: new FormControl(data.priority),
        });
    }

    dateValidator() {
        return (control: FormControl): null | Object  => {
            return control.value && control.value.getFullYear &&
            (1900 <= control.value.getFullYear() && control.value.getFullYear() <=  2099) ? null : { OrderDate: { value : control.value}};
        };
    }

    actionBegin(args: SaveEventArgs): void {
        if (args.requestType === 'beginEdit' || args.requestType === 'add') {
            this.submitClicked = false;
            this.taskForm = this.createFormGroup(args.rowData);
        }
        if (args.requestType === 'save') {
            this.submitClicked = true;
            if (this.taskForm.valid) {
                args.data = this.taskForm.value;
            } else {
                args.cancel = true;
            }
        }
    }

    actionComplete(args: DialogEditEventArgs): void {
        if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            // Set initial Focus
            if (args.requestType === 'beginEdit') {
                (args.form.elements.namedItem('taskName') as HTMLInputElement).focus();
            } else if (args.requestType === 'add') {
                (args.form.elements.namedItem('taskID') as HTMLInputElement).focus();
            }
        }
    }

    get taskID(): AbstractControl  { return this.taskForm.get('taskID'); }

    get taskName(): AbstractControl { return this.taskForm.get('taskName'); }

    get startDate(): AbstractControl { return this.taskForm.get('startDate'); }
}
export interface ITaskModel {
    taskID?: number;
    taskName?: string;
    startDate?: Date;
    duration?: number;
    progress?: number;
    priority?: string;
}

```

{% endtab %}

### Template-driven Forms

[`Template-driven`](https://angular.io/guide/forms#template-driven-forms) forms is a template-driven approach to create and manipulate the form controls. You can use template-driven form to add and update treegrid records. To use template-driven forms for editing operation, you can take leverage of the template support of dialog or inline edit mode. Setting the [`editSettings.mode`](../api/treegrid/editSettingsModel/#mode) as `Row/Dialog` and `editSettingsTemplate` as template variable of NgTemplate to define the treegrid editors.

In some cases, you need to add the new field editors in the dialog which are not present in the column model. In that situation, the dialog template will help you to customize the default edit dialog.

You can check this video to learn about how to customize the edit dialog of TreeGrid using template driven forms.

`youtube:IlVJBZOVUoA`

In the following sample, treegrid enabled with dialog template editing.

{% tab template="treegrid/edit-dlg-temp", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { DataUtil } from '@syncfusion/ej2-data';
import { DialogEditEventArgs, SaveEventArgs } from '@syncfusion/ej2-angular-grids';
import { EditService, ToolbarService, PageService } from '@syncfusion/ej2-angular-treegrid';
import { FormGroup } from '@angular/forms';

@Component({
    selector: 'app-container',
   template: `<ejs-treegrid [dataSource]='data' height='225' childMapping='subtasks' [treeColumnIndex]='1'allowPaging='true' [pageSettings]='pageSettings' [editSettings]='editSettings' [toolbar]='toolbar' (actionBegin)="actionBegin($event)" (actionComplete)="actionComplete($event)">
        <e-columns>
            <e-column field='taskID' headerText='Task ID' width='120' textAlign='Right' isPrimaryKey='true' ></e-column>
            <e-column field='taskName' headerText='Task Name' width='225' ></e-column>
            <e-column field='startDate' headerText='Start Date' width='150' format="yMd" ></e-column>
            <e-column field='approved' headerText='Approved' type='boolean' editType='booleanedit' [displayAsCheckBox]='true' width='90' textAlign='Right' ></e-column>
        </e-columns>
        <ng-template #editSettingsTemplate let-data>
        <div ngForm #taskForm="ngForm">
            <div class="form-row">
                <div class="form-group col-md-6">
                    <div class="e-float-input e-control-wrapper" [ngClass]="{'e-error': taskID.invalid && (taskID.dirty || taskID.touched)}">
                        <input [(ngModel)]="taskData.taskID" required id="taskID" name="taskID" type="text" [attr.disabled]="!data.isAdd ? '' : null" #taskID="ngModel">
                        <span class="e-float-line"></span>
                        <label class="e-float-text e-label-top" for="taskID"> Task ID</label>
                    </div>
                    <div id="taskIDError" *ngIf='taskID.invalid && (taskID.dirty || taskID.touched)'>
                        <label class="e-error" id="taskID-info" style="display: block;">*Task ID is required</label>
                    </div>
                </div>
                <div class="form-group col-md-6">
                    <div class="e-float-input e-control-wrapper" [ngClass]="{'e-error': taskName.invalid && (taskName.dirty || taskName.touched)}">
                        <input [(ngModel)]="taskData.taskName" required id="taskName" name="taskName" type="text" #taskName="ngModel">
                        <span class="e-float-line"></span>
                        <label class="e-float-text e-label-top" for="taskName">Task Name</label>
                    </div>
                    <div id="taskNameError" *ngIf='taskName.invalid && (taskName.dirty || taskName.touched)'>
                        <label class="e-error" id="taskName-info" style="display: block;">*Task Name is required</label>
                    </div>
                </div>
            </div>
            <div class="form-row">
                <div class="form-group col-md-6">
                    <ejs-numerictextbox [(ngModel)]="taskData.progress" name="progress" id="progress" placeholder="Progress" floatLabelType='Always'></ejs-numerictextbox>
                </div>
                <div class="form-group col-md-6">
                    <ejs-datepicker id="startDate" name="startDate" required [(ngModel)]="taskData.startDate" placeholder="Start Date" floatLabelType='Always'></ejs-datepicker>
                </div>
            </div>
            <div class="form-row">
                <div class="form-group col-md-6">
                    <ejs-numerictextbox [(ngModel)]="taskData.duration" name="duration" id="duration" placeholder="Duration" floatLabelType='Always'></ejs-numerictextbox>
                </div>
                <div class="form-group col-md-3">
                <ejs-checkbox #approved label='Approved' [(ngModel)]="taskData.approved" [ngModelOptions]="{standalone: true}" [checked]="taskData.approved"></ejs-checkbox>
                </div>
            </div>
        </div>
    </ng-template>
        </ejs-treegrid>`,
})
export class AppComponent implements OnInit {
    public data: Object[] = [];
    public editSettings: Object;
    public toolbar: string[];
    public pageSettings: Object;
    public taskData: ITaskModel;
    @ViewChild('taskForm')
    public taskForm: FormGroup;
    public progressDistinctData: Object;
    public priorityDistinctData: Object;

    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true , mode: 'Dialog' ,newRowPosition: 'Below'};
        this.toolbar = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
        this.pageSettings = { pageCount: 5 };
        this.progressDistinctData = DataUtil.distinct(sampleData, 'progress', true);
        this.priorityDistinctData = DataUtil.distinct(sampleData, 'priority', true );
    }

    actionBegin(args: SaveEventArgs): void {
        if (args.requestType === 'beginEdit' || args.requestType === 'add') {
            this.taskData = Object.assign({}, args.rowData);
        }
        if (args.requestType === 'save') {
            if (this.taskForm.valid) {
                args.data = this.taskData;
            } else {
                args.cancel = true;
            }
        }
    }

    actionComplete(args: DialogEditEventArgs): void {
        if (args.requestType === 'beginEdit' || args.requestType === 'add') {
            // Disable the Validation Rules
            args.form.ej2_instances[0].rules = {};
            // Set initial Focus
            if (args.requestType === 'beginEdit') {
                (args.form.elements.namedItem('taskName') as HTMLInputElement).focus();
            } else if (args.requestType === 'add') {
                (args.form.elements.namedItem('taskID') as HTMLInputElement).focus();
            }

        }
    }

    public focusIn(target: HTMLElement): void {
        target.parentElement.classList.add('e-input-focus');
    }

    public focusOut(target: HTMLElement): void {
        target.parentElement.classList.remove('e-input-focus');
    }
}
export interface ITaskModel {
    taskID?: number;
    taskName?: string;
    startDate?: Date;
    duration?: number;
    progress?: number;
    priority?: string;
    approved?: boolean;
}

```

{% endtab %}

> The template form editors should have **name** attribute.

### Template context

The Essential JS2 packages has a built-in template engine. Using the template engine, you can access the row information inside the HTML element and bind the attributes, values, or elements based on this row information.

The following properties will be available at the time of template execution.

| Property Name | Usage |
|---------------|--------|
| <kbd>isAdd</kbd> | A Boolean property; it defines whether the current row should be a new record or not.

In the following code example, the `taskID` textbox has been disabled by using the `isAdd` property.

```html
// The disabled attributes will be added based on the isAdd property.
<input formControlName="taskID" id="taskID" name="taskID" type="text" [attr.disabled]="!data.isAdd ? '' : null">

```

The following code example illustrates rendering the `taskID` textbox, when a new record is added.

```html

<div class="form-group col-md-6" *ngIf='data.isAdd'>
    <div class="e-float-input e-control-wrapper">
        <input formControlName="taskID" id="taskID" name="taskID" type="text" [attr.disabled]="!data.isAdd ? '' : null">
        <span class="e-float-line"></span>
        <label class="e-float-text e-label-top" for="taskID">Task ID</label>
    </div>
</div>

```

### Set focus to editor

By default, the first input element in the dialog will be focused while opening the dialog.
If the first input element is in disabled or hidden state, focus the valid input element in the
[`actionComplete`](../api/treegrid/#actioncomplete)
event based on `requestType` as `beginEdit`.

```typescript

    actionComplete: (args: DialogEditEventArgs) => {
        // Set initial Focus
        if (args.requestType === 'beginEdit') {
            (args.form.elements.namedItem('taskName')as HTMLInputElement).focus();
        }
    }

```

### Disable form validation

If you have interested to use [`angular form validation`](https://angular.io/guide/form-validation) then you need to disable the default validation rules in  the [`actionComplete`](../api/treegrid/#actioncomplete) event.

```typescript

    actionComplete(args: DialogEditEventArgs) {
        if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            // Disable the Validation Rules
            args.form.ej2_instances[0].rules = {};
        }
    }

```

### Adding validation rules for custom editors

If you have used additional fields that are not present in the column model, then add the validation rules to the [`actionComplete`](../api/treegrid/#actioncomplete) event.

```typescript

    actionComplete: (args: DialogEditEventArgs) => {
        if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            // Add Validation Rules
            args.form.ej2_instances[0].addRules('progress', {max: 100});
        }
    }

```

## Adding row position

The TreeGrid control provides the support to add the new row in the top, bottom, above selected row, below selected row and child position of tree grid content using [`editSettings.newRowPosition`](../api/treegrid/editSettingsModel/#newrowposition) property. By default, a new row will be added at the top of the treegrid.

The following examples shows how to set new row position as `Child` in tree grid.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='priority' headerText='Priority' textAlign='Right' width=90></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' type='date' editType='datepickeredit' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, newRowPosition: 'Child', mode: 'Cell' };
        this.toolbarOptions = ['Add', 'Delete', 'Update', 'Cancel'];
    }
}

```

{% endtab %}

## Command column

The command column provides an option to add CRUD action buttons in a column. This can be defined by the [`column.commands`](../api/treegrid/column/#commands) property.

The available built-in command buttons are:

| Command Button | Actions |
|----------------|---------|
| Edit | Edit the current row.|
| Delete | Delete the current row.|
| Save | Update the edited row.|
| Cancel | Cancel the edited state. |

{% tab template="treegrid/edit-command", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { CommandModel } from "@syncfusion/ej2-angular-grids" ;
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                    <e-column headerText='Commands' width=120 [commands]='commands'></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    public commands: CommandModel;
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
        this.toolbarOptions = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
        this.commands = [{ type: 'Edit', buttonOption: { iconCss: ' e-icons e-edit', cssClass: 'e-flat' } },
                { type: 'Delete', buttonOption: { iconCss: 'e-icons e-delete', cssClass: 'e-flat' } },
                { type: 'Save', buttonOption: { iconCss: 'e-icons e-update', cssClass: 'e-flat' } },
                { type: 'Cancel', buttonOption: { iconCss: 'e-icons e-cancel-icon', cssClass: 'e-flat' } }];
    }
}

```

{% endtab %}

### Custom command

 The custom command buttons can be added in a column by using the [`column.commands`](../api/treegrid/column/#commands) property and
the action for the custom buttons can be defined in the [`buttonOption.click`](../api/grid/commandButtonOptions/#click) event.

{% tab template="treegrid/edit-command", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit,ViewChild } from '@angular/core';
import { sampleData } from './datasource';
import { closest } from '@syncfusion/ej2-base';
import { IRow } from '@syncfusion/ej2-treegrid';
import { EditSettingsModel,CommandModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';
import { TreeGridComponent } from '@syncfusion/ej2-angular-treegrid';
@Component({
    selector: 'app-container',
    template: `<ejs-treegrid #treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' isPrimaryKey='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
                    <e-column headerText='Commands' width=120 [commands]='commands'></e-column>
       </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    public commands: CommandModel[];
    @ViewChild('treegrid')
    public treeGridObj: TreeGridComponent;
    public onClick = (args: Event) => {
    let rowIndex: number = (<HTMLTableRowElement>closest(args.target as Element, '.e-row')).rowIndex;
    let data: Object = this.treeGridObj.getCurrentViewRecords();
    alert(JSON.stringify(data[rowIndex]));
}
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Row' };
        this.toolbarOptions = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
        this.commands = [{ buttonOption: { content: 'Details', cssClass: 'e-flat', click: this.onClick.bind(this) } }];
    }
}

```

{% endtab %}

## Confirmation messages

### Delete confirmation

The delete confirm dialog can be shown when deleting a record by defining the [`showDeleteConfirmDialog`](../api/treegrid/editSettingsModel/#showdeleteconfirmdialog) as `true`

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='priority' headerText='Priority' textAlign='Right' width=90></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' type='date' editType='datepickeredit' width=90></e-column>
                    <e-column field='duration' headerText='Duration' textAlign='Right' width=80></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, showDeleteConfirmDialog: true, mode: 'Cell' };
        this.toolbarOptions = ['Add', 'Delete', 'Update', 'Cancel'];
    }
}

```

{% endtab %}

> The `showDeleteConfirmDialog` supports all type of edit modes.

## Column validation

Column validation allows you to validate the edited or added row data and it display errors for invalid fields before saving data.
TreeGrid uses `Form Validator` component for column validation.
You can set validation rules by defining the [`columns.validationRules`](../api/treegrid/column/#validationrules).

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' isPrimaryKey='true' textAlign='Right' width=90 [validationRules]='taskidRule' ></e-column>
                    <e-column field='taskName' headerText='Task Name' editType='stringedit' textAlign='Left' width=180  [validationRules]='stringRule' ></e-column>
                    <e-column field='approved' headerText='Approved' editType='booleanedit' type='boolean' textAlign='Right' [displayAsCheckBox]='true' width=110></e-column>
                    <e-column field='priority' headerText='Priority' editType='dropdownedit' textAlign='Right' width=110 [validationRules]='stringRule' ></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' [format]='formatOptions' editType='datetimepickeredit' [validationRules]='dateRule' width=180 ></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' editType='numericedit' width=120 [edit]='editing' [validationRules]='progressRule' ></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    public editing: Object;
    public formatOptions: Object;
    public editOptions: Object;
    public  stringRule: Object;
    public taskidRule: Object;
    public progressRule: Object;
    public dateRule: Object;
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Cell' };
        this.toolbarOptions = ['Add', 'Delete', 'Update', 'Cancel'];
        this.editing = { params: { format: 'n' } };
        this.formatOptions = { format: 'M/d/y hh:mm a', type: 'dateTime' };
        this.progressRule = { number: true, min: 0 };
        this.taskidRule = { required: true, number: true };
        this.dateRule = { date: true };
        this.stringRule = { required: true };
    }
}

```

{% endtab %}

## Custom validation

You can define your own custom validation rules for the specific columns by using `Form Validator custom rules`.

In the below demo, custom validation applied for `Priority` column.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' isPrimaryKey='true' textAlign='Right' width=90  ></e-column>
                    <e-column field='taskName' headerText='Task Name' editType='stringedit' textAlign='Left' width=180   ></e-column>
                    <e-column field='approved' headerText='Approved' editType='booleanedit' type='boolean' textAlign='Right' [displayAsCheckBox]='true' width=110></e-column>
                    <e-column field='priority' headerText='Priority' [validationRules]='customrule' textAlign='Right' width=110  ></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' [format]='formatOptions' editType='datetimepickeredit' width=180 ></e-column>
                    <e-column field='progress' headerText='Progress' textAlign='Right' editType='numericedit' width=120 [edit]='editing' ></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    public editing: Object;
    public formatOptions: Object;
    public editOptions: Object;
    public customrule: Object;
    public customFn: (args: { [key: string]: string }) => boolean = (args: { [key: string]: string }) => {
    return args['value'].length <= 8;
};
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Cell' };
        this.toolbarOptions = ['Add', 'Delete', 'Update', 'Cancel'];
        this.editing = { params: { format: 'n' } };
        this.formatOptions = { format: 'M/d/y hh:mm a', type: 'dateTime' };
        this.customrule = { required: true, minLength: [this.customFn, 'Value should be within 8 letters'] };
    }
}

```

{% endtab %}

## Persisting data in server

Edited data can be persisted in the database using the RESTful web services.

All the CRUD operations in the treegrid are done through [`DataManager`](../data). The `DataManager` has an option to bind all the CRUD related data in server-side.

> For your information, the ODataAdaptor persists data in the server as per OData protocol.

You can also check on this video about persisting data in server.

`youtube:UuD7_W2yIVs`

In the following section, we have explained how to perform CRUD operation in server-side using the [`UrlAdaptor`](../../data/adaptors.html#url-adaptor) and `RemoteSave Adaptor`.

### URL adaptor

You can use the [`UrlAdaptor`](../../data/adaptors.html#url-adaptor) of `DataManager` when binding data source from remote data.
In the initial load of treegrid, data are fetched from remote data and bound to the treegrid using `url` property of `DataManager`.
You can map The CRUD operation in treegrid can be mapped to server-side Controller actions using the properties `insertUrl`, `removeUrl`, `updateUrl` and `batchUrl`.

The following code example describes the above behavior.

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, UrlAdaptor } from '@syncfusion/ej2-data';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' idMapping='TaskID' parentIdMapping='parentID' >
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='90' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='170'></e-column>
            <e-column field='StartDate' headerText='Start Date' width='130' format="yMd" textAlign='Right' editType='datepickeredit'></e-column>
            <e-column field='EndDate' headerText='End Date' width='130' format="yMd" textAlign='Right' editType='datepickeredit'></e-column>
            <e-column field='Progress' headerText='Progress' width='100' textAlign='Right'></e-column>
        </e-columns>
    </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];

    public dataManager: DataManager = new DataManager({
        url: "Home/DataSource",
        updateUrl: "Home/Update",
        insertUrl: "Home/Insert",
        removeUrl: "Home/Delete",
        batchUrl: "Home/Remove",
        adaptor: new UrlAdaptor
    });

    ngOnInit(): void {
        this.data = this.dataManager;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, newRowPosition: 'Below', mode: 'Row' };
        this.toolbarOptions = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
}

```

Also, when using the `UrlAdaptor`, you need to return the data as JSON from the controller action and the JSON object must contain a property as `result` with dataSource as its value and one more property `count` with the dataSource total records count as its value.

The following code example describes the above behavior.

```typescript

public ActionResult DataSource(DataManager dm)
{
    var DataSource = TreeData.GetTree();
    var count = DataSource.ToList<TreeData>().Count();
    if (dm.Skip != 0)
    {
        DataSource = operation.PerformSkip(DataSource, dm.Skip);   //Paging
    }
    if (dm.Take != 0)
    {
        DataSource = operation.PerformTake(DataSource, dm.Take);
    }
    return dm.RequiresCounts ? Json(new { result = DataSource, count = count }) : Json(DataSource);
}

```

### Insert record

Using the `insertUrl` property, you can specify the controller action mapping URL to perform insert operation on the server-side.

The following code example describes the above behavior and also we have inserted new record based on the newRowPosition TreeGrid editSettings as "Below".

```typescript

public void Insert(TreeGridData value, int relationalKey)
{
    var i = 0;
    for (; i < TreeData.tree.Count; i++)
    {
        if (TreeData.tree[i].TaskID == relationalKey)
        {
            break;
        }
    }
    i += FindChildRecords(relationalKey); // Inserted new record when newRowPosition API is in "Below".
    TreeData.tree.Insert(i + 1, value);
}

public int FindChildRecords(int id)
{
    var count = 0;
    for (var i = 0; i < TreeData.tree.Count; i++)
    {
        if (TreeData.tree[i].ParentItem == id)
        {
            count++;
            count += FindChildRecords(TreeData.tree[i].TaskID);
        }
    }
    return count;
}

```

The newly added record details are bound to the `value` parameter and `relationalKey` contains primaryKey value of an selected record helps to find out the position of newly added record. Please refer to the following screenshot.

![Insert](images/insert.PNG)

### Update record

Using the `updateUrl` property, the controller action mapping URL can be specified to perform save/update operation on the server-side.

The following code example describes the previous behavior.

```typescript

public ActionResult Update(TreeGridData value)
{
    var val = TreeData.tree.Where(ds => ds.TaskID == value.TaskID).FirstOrDefault();
    val.TaskName = value.TaskName;
    val.StartDate = value.StartDate;
    val.Duration = value.Duration;
    val.Priority = value.Priority;
    val.Progress = value.Progress;
    return Json(value);
}

```

The updated record details are bound to the `value` parameter. Please refer to the following screenshot.

![Update](images/update.PNG)

### Delete record

Using the `removeUrl` and `batchUrl` property, the controller action mapping URL can be specified to perform delete operation on the server-side.

The following code example describes the previous behavior.

```typescript

public ActionResult Delete(int key)
{
    TreeData.tree.Remove(TreeData.tree.Where(ds => ds.TaskID == key).FirstOrDefault());
}

// Remove method (batchUrl) will be triggered when we delete parent record.

public ActionResult Remove(List<TreeGridData> changed, List<TreeGridData> added, List<TreeGridData> deleted)
{
    for (var i = 0; i < deleted.Count; i++)
    {
        TreeData.tree.Remove(TreeData.tree.Where(ds => ds.TaskID == deleted[i].TaskID).FirstOrDefault());
    }
}

```

The deleted record primary key value is bound to the `key` parameter. Please refer to the following screenshot.

![Delete](images/remove.PNG)

While delete parent record, the parent and child records is bound to the `deleted` parameter. Please refer to the following screenshot.

![Remove](images/delete.PNG)

### Remote Save Adaptor

You may need to perform all Tree Grid Actions in client-side except the CRUD operations, that should be interacted with server-side to persist data. It can be achieved in TreeGrid by using **RemoteSaveAdaptor**.

Datasource must be set to **json** property and set **RemoteSaveAdaptor** to the **adaptor** property. CRUD operations can be mapped to server-side using **updateUrl**, **insertUrl**, **removeUrl** and **batchUrl** properties.

You can use the following code example to use **RemoteSaveAdaptor** in TreeGrid.

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, RemoteSaveAdaptor } from '@syncfusion/ej2-data';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' idMapping='TaskID' parentIdMapping='parentID' >
        <e-columns>
            <e-column field='TaskID' headerText='Task ID' width='90' textAlign='Right'></e-column>
            <e-column field='TaskName' headerText='Task Name' width='170'></e-column>
            <e-column field='StartDate' headerText='Start Date' width='130' format="yMd" textAlign='Right' editType='datepickeredit'></e-column>
            <e-column field='EndDate' headerText='End Date' width='130' format="yMd" textAlign='Right' editType='datepickeredit'></e-column>
            <e-column field='Progress' headerText='Progress' width='100' textAlign='Right'></e-column>
        </e-columns>
    </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: DataManager;
    public value: any;
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    ngOnInit(): void {
        this.value = (window as any).griddata;
        this.data = new DataManager({
            json: JSON.parse(this.value),
            updateUrl: "Home/Update",
            insertUrl: "Home/Insert",
            removeUrl: "Home/Delete",
            batchUrl: "Home/Remove",
            adaptor: new RemoteSaveAdaptor();
        });
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, newRowPosition: 'Below', mode: 'Row' };
        this.toolbarOptions = ['Add', 'Edit', 'Delete', 'Update', 'Cancel'];
    }
}

```

The following code example describes how to fetch the data from `ViewBag` in angular.

```html
    <script type="text/javascript">
       window.griddata = '@Html.Raw(Json.Encode(ViewBag.dataSource))';
    </script>
```

The following code example describes the CRUD operations handled at server-side.

```typescript

public ActionResult Index(DataManager dm)
{
   var data = TreeData.GetTree();
   ViewBag.dataSource = data;
   return View();
}

public void Insert(TreeData value, int relationalKey)
{
    var i = 0;
    for (; i < TreeData.tree.Count; i++)
    {
        if (TreeData.tree[i].TaskID == relationalKey)
        {
            break;
        }
    }
    i += FindChildRecords(relationalKey); // Inserted new record when newRowPosition API is in "Below".
    TreeData.tree.Insert(i + 1, value);
}

public ActionResult Update(TreeData value)
{
    var val = TreeData.tree.Where(ds => ds.TaskID == value.TaskID).FirstOrDefault();
    val.TaskName = value.TaskName;
    val.StartDate = value.StartDate;
    val.Duration = value.Duration;
    val.Priority = value.Priority;
    val.Progress = value.Progress;
    return Json(value);
}

public ActionResult Delete(int key)
{
    TreeData.tree.Remove(TreeData.tree.Where(ds => ds.TaskID == key).FirstOrDefault());;
}

// Remove method (batchUrl) will be triggered when we delete parent record.

public ActionResult Remove(List<TreeGridData> changed, List<TreeGridData> added, List<TreeGridData> deleted)
{
    for (var i = 0; i < deleted.Count; i++)
    {
        TreeData.tree.Remove(TreeData.tree.Where(ds => ds.TaskID == deleted[i].TaskID).FirstOrDefault());
    }
}

```

## Default column values on add new

The treegrid provides an option to set the default value for the columns when adding a new record in it.
To set a default value for the particular column by defining the [`columns.defaultValue`](../api/treegrid/column/#defaultvalue).

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='priority' headerText='Priority' defaultValue='Normal' textAlign='Right' width=90></e-column>
                    <e-column field='startDate' headerText='Start Date' textAlign='Right' format='yMd' type='date' editType='datepickeredit' width=90></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, showDeleteConfirmDialog: true, mode: 'Cell' };
        this.toolbarOptions = ['Add', 'Delete', 'Update', 'Cancel'];
    }
}

```

{% endtab %}

## Disable editing for particular column

You can disable editing for particular columns by using the [`columns.allowEditing`](../api/treegrid/column/#allowediting).

In the following demo, editing is disabled for the `Start Date` column.

{% tab template="treegrid/edit-toolbar", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { sampleData } from './datasource';
import { EditSettingsModel, ToolbarItems } from '@syncfusion/ej2-angular-treegrid';

@Component({
    selector: 'app-container',
    template: `<ejs-treegrid [dataSource]='data'  [toolbar]='toolbarOptions' [treeColumnIndex]='1' height='270' [editSettings]='editSettings' childMapping='subtasks' >
        <e-columns>
                    <e-column field='taskID' headerText='Task ID' [isPrimaryKey]='true' textAlign='Right' width=90></e-column>
                    <e-column field='taskName' headerText='Task Name' textAlign='Left' width=180></e-column>
                    <e-column field='priority' headerText='Priority' defaultValue='Normal' textAlign='Right' width=90></e-column>
                    <e-column field='startDate' headerText='Start Date' [allowEditing]='false' textAlign='Right' format='yMd' type='date' editType='datepickeredit' width=90></e-column>
        </e-columns>
                </ejs-treegrid>`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbarOptions: ToolbarItems[];
    ngOnInit(): void {
        this.data = sampleData;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, showDeleteConfirmDialog: true, mode: 'Cell' };
        this.toolbarOptions = ['Add', 'Delete', 'Update', 'Cancel'];
    }
}

```

{% endtab %}

## Troubleshoot: Editing works only for first row

The Editing functionalities can be performed based upon the primary key value of the selected row.
If `primaryKey` is not defined in the treegrid, then edit or delete action take places the first row.