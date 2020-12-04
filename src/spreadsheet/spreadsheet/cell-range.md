---
title: "Cell Range"
component: "Spreadsheet"
description: "Learn the various operations that you can perform in range of cells of the Angular Spreadsheet."
---

# Cell Range

A group of cells in a sheet is known as cell range.

## Wrap text

Wrap text allows you to display large content as multiple lines in a single cell. By default, the wrap text support is enabled. Use the [`allowWrap`](../api/spreadsheet/#allowwrap) property to enable or disable the wrap text support in spreadsheet.

Wrap text can be applied or removed to a cell or range of cells in the following ways,

* Using the `wrap` property in `cell`, you can enable or disable wrap text to a cell at initial load.
* Select or deselect wrap button from ribbon toolbar to apply or remove the wrap text to the selected range.
* Using the [`wrap`](../api/spreadsheet/#wrap) method, you can apply or remove the wrap text once the component is loaded.

The following code example shows the wrap text functionality in spreadsheet.

{% tab template="spreadsheet/wrap-text", sourceFiles="app/**/*.ts", isDefaultActive=true, iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { dataSource } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (created)="created()" [showFormulaBar]="false">
                <e-sheets>
                  <e-sheet name="Movie List">
                    <e-ranges>
                      <e-range [dataSource]="data"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [index]=1 [width]=100></e-column>
                      <e-column [width]=140></e-column>
                      <e-column [width]=90></e-column>
                      <e-column [width]=150></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=90></e-column>
                      <e-column [width]=180></e-column>
                    </e-columns>
                    <e-rows>
                      <e-row [height]=30></e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=7 [wrap]="true"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=7 [wrap]="true"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=7 [wrap]="true"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=7 [wrap]="true"></e-cell>
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
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:H1');
        this.spreadsheetObj.cellFormat({ verticalAlign: 'middle' }, 'A1:H5');
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'A2:B5');
        this.spreadsheetObj.cellFormat({ textAlign: 'center' }, 'D2:D5');

        // To wrap the cells from E2 to E5 range
        this.spreadsheetObj.wrap('E2:E5');
        // To unwrap the H3 cell
        this.spreadsheetObj.wrap('H3', false);
    }
}
```

{% endtab %}

## Merge cells

Merge cells allows users to span two or more cells in the same row or column into a single cell. When cells with multiple values are merged, top-left most cell data will be the data for the merged cell. By default, the merge cells option is enabled. Use [`allowMerge`](../api/spreadsheet/#allowmerge) property to enable or disable the merge cells option in spreadsheet.

You can merge the range of cells in the following ways,

* Set the `rowSpan` and `colSpan` property in `cell` to merge the number of cells at initial load.
* Select the range of cells and apply merge by selecting the desired option from ribbon toolbar.
* Use [`merge`](../api/spreadsheet/#merge) method to merge the range of cells, once the component is loaded.

The available merge options in spreadsheet are,

| Type | Action |
|-------|---------|
| Merge All | Combines all the cells in a range in to a single cell (default). |
| Merge Horizontally | Combines cells in a range as row-wise. |
| Merge Vertically | Combines cells in a range as column-wise. |
| UnMerge | Splits the merged cells into multiple cells. |

The following code example shows the merge cells operation in spreadsheet.

{% tab template="spreadsheet/merge-cells", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { dataSource } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (created)="created()" [showFormulaBar]="false">
                <e-sheets>
                  <e-sheet name="Merge Cells">
                    <e-ranges>
                      <e-range [dataSource]="data"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=90></e-column>
                      <e-column [width]=150></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                    </e-columns>
                    <e-rows>
                      <e-row [height]=35></e-row>
                      <e-row [height]=35>
                        <e-cells>
                          <!-- Merging the 2nd cells of rows 2 and 3 through cell binding. -->
                          <e-cell [index]=1 [rowSpan]=2></e-cell>
                          <!-- Merging the 2nd row's 3rd and 4th cells through cell binding. -->
                          <e-cell [colSpan]=2></e-cell>
                          <!-- Merging the 2nd row's 7th, 8th and 9th cells through cell binding. -->
                          <e-cell [index]=6 [colSpan]=3></e-cell>
                          <!-- Merging the 2nd and 3rd rows 11th, 12th and 13th cells through cell binding. -->
                          <e-cell [index]=10 [rowSpan]=2 [colSpan]=3></e-cell>
                          <e-cell [index]=13 [colSpan]=2></e-cell>
                          <e-cell [index]=17 [colSpan]=2></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row [height]=35>
                        <e-cells>
                          <e-cell [index]=3 [colSpan]=3></e-cell>
                          <e-cell [index]=6 [colSpan]=4></e-cell>
                          <e-cell [index]=13 [colSpan]=3></e-cell>
                          <e-cell [index]=17 [colSpan]=2></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row [height]=35>
                        <e-cells>
                          <e-cell [index]=2 [colSpan]=3></e-cell>
                          <e-cell [index]=5 [colSpan]=2></e-cell>
                          <e-cell [index]=7 [colSpan]=3></e-cell>
                          <e-cell [index]=15 [colSpan]=2></e-cell>
                          <e-cell [index]=17 [colSpan]=2></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row [height]=35>
                        <e-cells>
                          <e-cell [index]=2 [colSpan]=3></e-cell>
                          <e-cell [index]=6 [colSpan]=4></e-cell>
                          <e-cell [index]=16 [colSpan]=2></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row [height]=35>
                        <e-cells>
                          <e-cell [index]=2 [colSpan]=4></e-cell>
                          <e-cell [index]=7 [colSpan]=3></e-cell>
                          <e-cell [index]=15 [colSpan]=2></e-cell>
                          <e-cell [index]=17 [colSpan]=2></e-cell>
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
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:S1');
        this.spreadsheetObj.numberFormat('h:mm AM/PM', 'C1:S1');
        this.spreadsheetObj.cellFormat({ verticalAlign: 'middle' }, 'A1:S11');
          // Merging the `K4:M4` cells using method
        this.spreadsheetObj.merge('K4:M4');
        // Merging the 5th and 6th row cells across 11th, 12th and 13th column
        this.spreadsheetObj.merge('K5:M6', 'Vertically');
        // Merging the 18th and 19th column cells across 2nd, 3rd and 4th row
        this.spreadsheetObj.merge('N4:O6', 'Horizontally');
    }
}
```

{% endtab %}

## See Also

* [Rows and columns](./rows-and-columns)
* [Formatting](./formatting)
* [Hyperlink](./link)
* [Sorting](./sort)
* [Filtering](./filter)
