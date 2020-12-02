---
title: "Tables"
component: "DocumentEditor"
description: "Learn how to insert, select, or delete table, row(s), and column(s) in JavaScript document editor."
---

# Tables

Tables are an efficient way to present information. Document editor can display and edit the tables. You can select and edit tables through keyboard, mouse, or touch interactions. Document editor exposes a rich set of APIs to perform these operations programmatically.

## Create a table

You can create and insert a table at cursor position by specifying the required number of rows and columns.

Refer to the following sample code.

```typescript
 this.documentEditor.editor.insertTable(3,3);
```

The maximum size of row and column is limited to 32767 and 63 respectively.

## Insert rows

You can add a row (or several rows) above or below the row at cursor position by using the `insertRow` method. This method accepts the following parameters:

Parameter | Type | Description
----------|------|-------------
above(optional) | boolean | This is optional and if omitted, it takes the value as false and inserts below the row at cursor position.
count(optional) | number | This is optional and if omitted, it takes the value as 1.

Refer to the following sample code.

```typescript
//Inserts a row below the row at cursor position
this.documentEditor.editor.insertRow();
//Inserts a row above the row at cursor position
this.documentEditor.editor.insertRow(false);
//Inserts three rows below the row at cursor position
this.documentEditor.editor.insertRow(true, 3)
```

## Insert columns

You can add a column (or several columns) to the left or right of the column at cursor position by using the `insertColumn` method. This method accepts the following parameters:

Parameter | Type | Description
----------|------|-------------
left(optional) | boolean| This is optional and if omitted, it takes the value as false and inserts to the right of column at cursor position.
count(optional) | number |  This is optional and if omitted, it takes the value as 1.

Refer to the following sample code.

```typescript
//Insert a column to the right of the column at cursor position.
this.documentEditor.editor.insertColumn();
//Insert a column to the left of the column at cursor position.
this.documentEditor.editor.insertColumn(false);
//Insert two columns to the left of the column at cursor position.
this.documentEditor.editor.insertColumn(false, 2);
```

### Select an entire table

If the cursor position is inside a table, you can select the entire table by using the following sample code.

```typescript
this.documentEditor.selection.selectTable();
```

### Select row

You can select the entire row at cursor position by using the following sample code.

```typescript
this.documentEditor.selection.selectRow();
```

If current selection spans across cells of different rows, all these rows will be selected.

### Select column

You can select the entire column at cursor position by using the following sample code.

```typescript
this.documentEditor.selection.selectColumn();
```

If current selection spans across cells of different columns, all these columns will be selected.

### Select cell

You can select the cell at cursor position by using the following sample code.

```typescript
this.documentEditor.selection.selectCell();
```

## Delete table

Document editor allows you to delete the entire table. You can use the `deleteTable()` method of editor instance, if selection is in table. Refer to the following sample code.

```typescript
this.documentEditor.editor.deleteTable();
```

## Delete row

Document editor allows you to delete the selected number of rows. You can use the `deleteRow()` method of editor instance to delete the selected number of rows, if selection is in table. Refer to the following sample code.

```typescript
this.documentEditor.editor.deleteRow();
```

## Delete column

Document editor allows you to delete the selected number of columns. You can use the `deleteColumn ()` method of editor instance to delete the selected number of columns, if selection is in table. Refer to the following sample code.

```typescript
this.documentEditor.editor.deleteColumn();
```

## Merge cells

You can merge cells vertically, horizontally, or combination of both to a single cell. To vertically merge the cells, the columns within selection should be even in left and right directions. To horizontally merge the cells, the rows within selection should be even in top and bottom direction.
Refer to the following sample code.

```typescript
this.documentEditor.editor.mergeCells()
```

## How to work with tables

The following sample demonstrates how to delete the table row or columns, merge cells and how to bind the API with button.

{% tab template="document-editor/tables",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, EditorService, SelectionService, SfdtExportService, EditorHistoryService, TableDialogService, ContextMenuService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    styleUrls: ['styles.css'],
    template: `<div style="width:100%;height:330px">
    <div>
        <ejs-toolbar (clicked)='toolbarButtonClick($event)'>
            <e-items>
                <e-item prefixIcon="e-de-icon-Table" tooltipText="Insert Table" id="table"></e-item>
                <e-item type="Separator"></e-item>
                <e-item prefixIcon="e-de-icon-InsertAbove" tooltipText="Insert new row above" id="insert_above"></e-item>
                <e-item prefixIcon="e-de-icon-InsertBelow" tooltipText="Insert new row below" id="insert_below"></e-item>
                <e-item type="Separator"></e-item>
                <e-item prefixIcon="e-de-icon-InsertLeft" tooltipText="Insert new column to the left" id="insert_left"></e-item>
                <e-item prefixIcon="e-de-icon-InsertRight" tooltipText="Insert new column to the right" id="insert_right"></e-item>
                <e-item type="Separator"></e-item>
                <e-item prefixIcon="e-de-icon-DeleteTable" tooltipText="Delete Entire table" id="delete_table"></e-item>
                <e-item prefixIcon="e-de-icon-DeleteRows" tooltipText="Delete the selected row" id="delete_row"></e-item>
                <e-item prefixIcon="e-de-icon-DeleteColumns" tooltipText="Delete the selected column" id="delete_column"></e-item>
                <e-item type="Separator"></e-item>
                <e-item prefixIcon="e-de-icon-Cell" tooltipText="Merge the selected cells" id="merge_cell"></e-item>
                <e-item type="Separator"></e-item>
                <e-item text="Dialog" tooltipText="Open insert table dialog" id="table_dialog"></e-item>
            </e-items>
        </ejs-toolbar>
    </div>
   <ejs-documenteditor #document_editor [isReadOnly]=false  [enableSelection]=true  [enableEditorHistory]=true  [enableEditor]=true [enableTableDialog]=true [enableContextMenu]=true [enableSfdtExport]=true style="display:block;width: 100%;height: 100%;" (created)="onCreated()"></ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [EditorService, SelectionService, SfdtExportService, EditorHistoryService, TableDialogService, ContextMenuService]
})

export class AppComponent {
    @ViewChild('document_editor')
    public documentEditor: DocumentEditorComponent;

    onCreated(): void {
        this.documentEditor.editor.insertTable(2, 2);
    }

    public toolbarButtonClick(arg: any) {
        switch (arg.item.id) {
            case 'table':
                //Insert table API to add table
                this.documentEditor.editor.insertTable(3, 2);
                break;
            case 'insert_above':
                //Insert the specified number of rows to the table above to the row at cursor position
                this.documentEditor.editor.insertRow(true, 2);
                break;
            case 'insert_below':
                //Insert the specified number of rows to the table below to the row at cursor position
                this.documentEditor.editor.insertRow();
                break;
            case 'insert_left':
                //Insert the specified number of columns to the table left to the column at cursor position
                this.documentEditor.editor.insertColumn(true, 2);
                break;
            case 'insert_right':
                //Insert the specified number of columns to the table right to the column at cursor position
                this.documentEditor.editor.insertColumn();
                break;
            case 'delete_table':
                //Delete the entire table
                this.documentEditor.editor.deleteTable();
                break;
            case 'delete_row':
                //Delete the selected number of rows
                this.documentEditor.editor.deleteRow();
                break;
            case 'delete_column':
                //Delete the selected number of columns
                this.documentEditor.editor.deleteColumn();
                break;
            case 'merge_cell':
                //Merge the selected cells into one (both vertically and horizontally)
                this.documentEditor.editor.mergeCells();
                break;
            case 'table_dialog':
                //Opens insert table dialog
                this.documentEditor.showDialog('Table');
                break;
        }
    }
}

```

{% endtab %}

## See Also

* [Feature modules](../document-editor/feature-module/)
* [Insert table dialog](../document-editor/dialog#table-dialog/)