---
title: "Editing"
component: "Spreadsheet"
description: "This section explains you about the editing feature in the Angular spreadsheet."
---

# Editing

You can edit the contents of a cell directly in the cell or by typing in the formula bar. By default, the editing feature is enabled in the spreadsheet. Use the [`allowEditing`](../api/spreadsheet/#allowediting) property to enable or disable the editing feature.

## Edit cell

You can start editing by one of the following ways,

* Double click a cell to start the edit mode.
* Press `F2` key to edit the active cell.
* Use formula bar to perform editing.
* Use `BACKSPACE` or `SPACE` key to clear the cell content and start the edit mode.
* Using the [`startEdit`](../api/spreadsheet/#startedit) method.

## Save cell

If the cell is in editable state, you can save the edited cell by one of the following ways,

* Perform mouse click on any other cell rather than the current editing cell.
* Press `Enter` or `Tab` keys to save the edited cell content.
* Using the [`endEdit`](../api/spreadsheet/#endedit) method.

## Cancel editing

To cancel the editing without saving the changes, you can use one of the following ways,

* Press `ESCAPE` key, this will remove the editable state and update the unchanged cell content.
* Using the [`closeEdit`](../api/spreadsheet/#closeedit) method.

The following sample shows how to prevent the editing and cell save. Here `E` column prevent the editing by using cancel argument as true in [`cellEdit`](../api/spreadsheet/#celledit) event. In `D` column, prevent saving the edited changes by using cancel argument as true in [`beforeCellSave`](../api/spreadsheet/#beforecellsave) and use [`closeEdit`](../api/spreadsheet/#closeedit) method in spreadsheet.

{% tab template="spreadsheet/editing", sourceFiles="app/**/*.ts", iframeHeight="450px", isDefaultActive=true %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent, CellEditEventArgs } from '@syncfusion/ej2-angular-spreadsheet';
import { enableRipple } from '@syncfusion/ej2-base';
import { dataSource } from './datasource';

enableRipple(true);

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (created)="created()" (cellEdit)="cellEdit($event)" (beforeCellSave)="beforeCellSave($event)" [showSheetTabs]="false" [showRibbon]="false">
                <e-sheets>
                  <e-sheet selectedRange="E11">
                    <e-ranges>
                      <e-range [dataSource]="data"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=120></e-column>
                      <e-column [width]=180></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                    </e-columns>
                    <e-rows>
                      <e-row [index]=10>
                        <e-cells>
                          <e-cell [index]=3 value="Total Amount:" [style]="{ fontWeight: 'bold' }"></e-cell>
                          <e-cell formula="=SUM(E2:E10)"></e-cell>
                        </e-cells>
                      </e-row>
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
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:E1');
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'A2:A10');
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'C2:C10');
        this.spreadsheetObj.numberFormat('$#,##0.00', 'D2:D10');
        this.spreadsheetObj.numberFormat('$#,##0.00', 'E2:E11');
    }

    // Triggers before going to the editing mode.
    cellEdit(args: CellEditEventArgs): void {
        // Preventing the editing in 5th(Amount) column.
        if (args.address.includes('E')) { args.cancel = true; }
    }

    // Trigger before saving the edited cell content.
    beforeCellSave(args: CellEditEventArgs): void {
        // Prevent saving the edited changes in 4th(Rate) column.
        if (args.address.includes('D')) {
            args.cancel = true;
            // Manually removes the editable state without saving the changes. Use `endEdit` method if you want to save the changes.
            this.spreadsheetObj.closeEdit();
        }
    }
}
```

{% endtab %}

## Limitations

* Text overflow in cells is not supported in Editing.

## Note

You can refer to our [Angular Spreadsheet](https://www.syncfusion.com/angular-ui-components/angular-spreadsheet) feature tour page for its groundbreaking feature representations. You can also explore our [Angular Spreadsheet example](https://ej2.syncfusion.com/angular/demos/#/material/spreadsheet/default) to knows how to present and manipulate data.

## See Also

* [Cell range](./cell-range)
* [Formatting](./formatting)
* [Hyperlink](./link)
* [Undo and Redo](./undo-redo)
* [Unlock the particular cells in the protected sheet](./protect-sheet#unlock-the-particular-cells-in-the-protected-sheet)
