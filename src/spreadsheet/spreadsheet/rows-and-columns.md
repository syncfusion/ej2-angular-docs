---
title: "Rows and columns"
component: "Spreadsheet"
description: "This section shows the various operations that you can perform in the rows and columns of the Angular spreadsheet."
---

# Rows and columns

Spreadsheet is a tabular format consisting of rows and columns. The intersection point of rows and columns are called as cells. The list of operations that you can perform in rows and columns are,

* Insert
* Delete
* Show and Hide

## Insert

You can insert rows or columns anywhere in a spreadsheet. Use the [`allowInsert`](../api/spreadsheet/#allowinsert) property to enable or disable the insert option in Spreadsheet.

### Row

The rows can be inserted in the following ways,

* Using [`insertRow`](../api/spreadsheet/#insertrow) method, you can insert the rows once the component is loaded.
* Using context menu, insert the empty rows in the desired position.

The following code example shows the options for inserting rows in the spreadsheet.

{% tab template="spreadsheet/insert/row", sourceFiles="app/**/*.ts", isDefaultActive=true, iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent, RowModel } from '@syncfusion/ej2-angular-spreadsheet';
import { dataSource } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (created)="created()" [showFormulaBar]="false"
                [showSheetTabs]="false" [showRibbon]="false">
                <e-sheets>
                  <e-sheet>
                    <e-ranges>
                      <e-range [dataSource]="data" startCell="B1"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=20></e-column>
                      <e-column [width]=90></e-column>
                      <e-column [width]=220></e-column>
                      <e-column [width]=90></e-column>
                      <e-column [width]=140></e-column>
                      <e-column [width]=90></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                    </e-columns>
                  </e-sheet>
                </e-sheets>
              </ejs-spreadsheet>`
})
export class AppComponent {
    @ViewChild('spreadsheet')
    spreadsheetObj: SpreadsheetComponent;

    data: object[] = dataSource;
    // Rows model that is going to insert dynamically
    rowsModel: RowModel[] = [
        {
            index: 9, // Need to specify the index for the first row collection, the specified rows will be inserted in this index.
            cells: [{ value: '' }, { value: '8' }, { value: 'Northwoods Cranberry Sauce' }, { value: '3' }, { value: '12 - 12 oz jars' },
                { value: '40.00' }, { value: '6' }, { value: 'false' }]
        },
        {
            cells: [{ value: '' }, { value: '9' }, { value: 'Mishi Kobe Niku' }, { value: '4' }, { value: '18 - 500 g pkgs.' },
                { value: '97.00' }, { value: '29' }, { value: 'true' }]
        }
    ];

    created() {
        // Applies style formatting before inserting the rows
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'B1:H1');
        // inserting a empty row at 0th index
        this.spreadsheetObj.insertRow();
        // inserting 2 rows at the 9th index with data
        this.spreadsheetObj.insertRow(this.rowsModel);
        // Applies style formatting after the rows are inserted
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'B3:B12');
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'D3:D12');
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'F3:H12');
    }
}
```

{% endtab %}

### Column

The columns can be inserted in the following ways,

* Using [`insertColumn`](../api/spreadsheet/#insertcolumn) method, you can insert the columns once the component is loaded.
* Using context menu, insert the empty columns in the desired position.

The following code example shows the options for inserting columns in the spreadsheet.

{% tab template="spreadsheet/insert/column", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent, CellModel, getCellAddress } from '@syncfusion/ej2-angular-spreadsheet';
import { dataSource } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (created)="created()" [showFormulaBar]="false" [showSheetTabs]="false"
                [showRibbon]="false">
                <e-sheets>
                  <e-sheet>
                    <e-ranges>
                      <e-range [dataSource]="data" startCell="A2"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=90></e-column>
                      <e-column [width]=220></e-column>
                      <e-column [width]=90></e-column>
                      <e-column [width]=140></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                    </e-columns>
                  </e-sheet>
                </e-sheets>
              </ejs-spreadsheet>`
})
export class AppComponent {
    @ViewChild('spreadsheet')
    spreadsheetObj: SpreadsheetComponent;

    data: object[] = dataSource;
    // Cells model that you are going to update in the inserted 5th column dynamically
    cellsModel: CellModel[] = [{ value: 'Unit Price', style: { fontWeight: 'bold', textAlign: 'center' } }, { value: '18.00' },
        { value: '19.00' }, { value: '10.00' }, { value: '22.00' }, { value: '21.35' }, { value: '25.00' }, { value: '30.00' },
        { value: '21.00' }, { value: '40.00' }, { value: '97.00' }];

    created() {
        // Applies style formatting before inserting the column
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A2:G2');
        // inserting a empty column at 0th index
        this.spreadsheetObj.insertColumn();
        // inserting 1 column at the 5th index with column model
        this.spreadsheetObj.insertColumn([{ index: 5, width: 90 }]);
        let rowIndex = 1;
        // Updating the 5th column data
        this.cellsModel.forEach((cell: CellModel): void => {
            this.spreadsheetObj.updateCell(cell, getCellAddress(rowIndex, 5)); rowIndex++;
        });
        // Applies style formatting after the columns are inserted
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'B3:B12');
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'D3:D12');
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'F3:H12');
    }
}
```

{% endtab %}

## Delete

Delete support provides an option for deleting the rows and columns in the spreadsheet. Use [`allowDelete`](../api/spreadsheet/#allowdelete) property to enable or disable the delete option in Spreadsheet.

The rows and columns can be deleted dynamically in the following ways,

* Using [`delete`](../api/spreadsheet/#delete) method, you can delete the loaded rows and columns.
* Using context menu, you can delete the selected rows and columns.

The following code example shows the delete operation of rows and columns in the spreadsheet.

{% tab template="spreadsheet/delete/row-column", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { dataSource } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (created)="created()" [showFormulaBar]="false" [showSheetTabs]="false"
                [showRibbon]="false">
                <e-sheets>
                  <e-sheet>
                    <e-ranges>
                      <e-range [dataSource]="data"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=90></e-column>
                      <e-column [width]=220></e-column>
                      <e-column [width]=90></e-column>
                      <e-column [width]=140></e-column>
                      <e-column [width]=90></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                    </e-columns>
                  </e-sheet>
                </e-sheets>
              </ejs-spreadsheet>`
})
export class AppComponent {
    @ViewChild('spreadsheet')
    spreadsheetObj: SpreadsheetComponent;

    data: object[] = dataSource;

    created() {
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:H1');
        // deleting the rows from 8th to 10th index. To delete row, the last argument of enum type is passed as 'Row'
        this.spreadsheetObj.delete(8, 10, 'Row');
        // deleting the 2nd and 5th indexed columns
        this.spreadsheetObj.delete(2, 2, 'Column');
        this.spreadsheetObj.delete(5, 5, 'Column');
        // Applies style formatting after deleted the rows and columns
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'A2:A8');
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'D2:G8');
    }
}
```

{% endtab %}

## Limitations

The following features have some limitations in Insert/Delete:

* Insert row/column between the formatting applied cells.
* Insert row/column between the data validation.
* Insert row/column between the conditional formatting applied cells.
* Insert/delete row/column between the filter applied cells.

## Hide and show

You can show or hide the rows and columns in the spreadsheet through property binding, method, and context menu.

## Row

The rows can be hidden or shown through the following ways,

* Using `hidden` property in row, you can hide/show the rows at initial load.
* Using `hideRow` method, you can hide the rows by specifying the start and end row index, set the last argument `hide` as `false` to unhide the hidden rows.
* Right-click on the row header and select the desired option from context menu

## Column

The columns can be hidden or shown through following ways,

* Using `hidden` property in columns, you can hide/show the columns at initial load.
* Using `hideColumn` method, you can hide the columns by specifying the start and end column index, set the last argument `hide` as `false` to unhide the hidden columns.
* Right-click on the column header and select the desired option from context menu

The following code example shows the hide/show rows and columns operation in the spreadsheet.

{% tab template="spreadsheet/hide-show", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { dataSource } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (created)="created()" [showFormulaBar]="false"
                [showSheetTabs]="false" [showRibbon]="false">
                <e-sheets>
                  <e-sheet>
                    <e-ranges>
                      <e-range [dataSource]="data"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=150></e-column>
                      <!-- Hiding the 1st and 2nd column index through property binding -->
                      <e-column [width]=100 [hidden]="true"></e-column>
                      <e-column [width]=100 [hidden]="true"></e-column>
                      <e-column [width]=80></e-column>
                      <e-column [width]=80></e-column>
                      <e-column [width]=80></e-column>
                      <e-column [width]=80></e-column>
                      <e-column [width]=80></e-column>
                    </e-columns>
                    <e-rows>
                      <e-row [index]=2 [hidden]="true"></e-row>
                      <e-row [hidden]="true"></e-row>
                    </e-rows>
                  </e-sheet>
                </e-sheets>
              </ejs-spreadsheet>`
})
export class AppComponent {
    @ViewChild('spreadsheet')
    spreadsheetObj: SpreadsheetComponent;

    data: object[] = dataSource;

    created() {
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:H1');
        // Unhide the 2nd index hidden column
        this.spreadsheetObj.hideColumn(1, 1, false);
        // Unhide the 3rd index hidden row
        this.spreadsheetObj.hideRow(3, 3, false);
        // Hiding the 6th index column
        this.spreadsheetObj.hideColumn(6);
        // Hiding the 8th and 9th index row
        this.spreadsheetObj.hideRow(8, 9);
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'D2:H11');
    }
}
```

{% endtab %}

## See Also

* [Hyperlink](./link)
* [Sorting](./sort)
* [Filtering](./filter)
