---
title: "Formulas"
component: "Spreadsheet"
description: "This section helps you to understand the formula feature in the Essential JS 2 spreadsheet."
---

# Formulas

Formulas are used for calculating the data in a worksheet. You can refer the cell reference from same sheet or from different sheets.

## Usage

You can set formula for a cell in the following ways,

* Using the `formula` property from `cell`, you can set the formula or expression to each cell at initial load.
* Set the formula or expression through data binding.
* You can set formula for a cell by [`editing`](./editing).
* Using the [`updateCell`](../api/spreadsheet/#updatecell) method, you can set or update the cell formula.

## User Defined Functions

The list of formulas supported in the spreadsheet is sufficient for most of your calculations. If not, you can add your own custom function using the [`addCustomFunction`](../api/spreadsheet/#addcustomfunction) method. Use [`computeExpression`](../api/spreadsheet/#computeexpression) method, if you want to compute any formula or expression.

The following code example shows the calculation of data using supported and custom `formulas` in the spreadsheet.

{% tab template="spreadsheet/formula", sourceFiles="app/**/*.ts", iframeHeight="450px", isDefaultActive=true %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { enableRipple } from '@syncfusion/ej2-base';
import { dataSource } from './datasource';

enableRipple(true);

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (created)="created()" [showRibbon]="false"
                [showSheetTabs]="false">
                <e-sheets>
                  <e-sheet>
                    <e-ranges>
                      <e-range [dataSource]="data" startCell="A2"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=150></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                    </e-columns>
                    <e-rows>
                      <e-row [height]=40 [customHeight]="true">
                        <e-cells>
                          <e-cell value="Monthly Expense" [colSpan]=5 [style]="{ textAlign: 'center', fontWeight: 'bold', verticalAlign: 'middle', fontStyle: 'italic', fontSize: '15pt' }"></e-cell>
                          <e-cell formula="=SUM(E2:E10)"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row [index]=11>
                        <e-cells>
                          <e-cell value="Totals" [style]="{ fontStyle: 'italic', fontWeight: 'bold' }"></e-cell>
                          <!-- Calculating total of each column data through cell binding. -->
                          <e-cell formula="=SUM(B3:B11)"></e-cell>
                          <e-cell formula="=SUM(C3:C11)"></e-cell>
                          <e-cell formula="=SUM(D3:D11)"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=1 value="Number of Categories" [colSpan]=2 [style]="{ fontWeight: 'bold', textAlign: 'right' }"></e-cell>
                          <e-cell [index]=3 formula="=COUNTA(A3:A11)"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=1 value="Average Spend" [colSpan]=2 [style]="{ fontWeight: 'bold', textAlign: 'right' }"></e-cell>
                          <e-cell [index]=3 formula="=AVERAGE(B3:B11)" format="$#,##0"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=1 value="Min Spend" [colSpan]=2 [style]="{ fontWeight: 'bold', textAlign: 'right' }"></e-cell>
                          <e-cell [index]=3 formula="=MIN(B3:B11)" format="$#,##0"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=1 value="Max Spend" [colSpan]=2 [style]="{ fontWeight: 'bold', textAlign: 'right' }"></e-cell>
                          <e-cell [index]=3 formula="=Max(B3:B11)" format="$#,##0"></e-cell>
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

    // Custom function to calculate percentage between two cell values.
    calculatePercentage(firstCell: string, secondCell: string): number {
      return Number(firstCell) / Number(secondCell);
    }

    created() {
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A2:E2');
        this.spreadsheetObj.numberFormat('$#,##0', 'B3:D12');
        this.spreadsheetObj.numberFormat('0%', 'E3:E12');

        // Adding custom function for calculating the percentage between two cells.
        this.spreadsheetObj.addCustomFunction(this.calculatePercentage, 'PERCENTAGE');
        // Calculate percentage using custom added formula in E12 cell.
        this.spreadsheetObj.updateCell({ formula: '=PERCENTAGE(C12,D12)' }, 'E12');
        this.spreadsheetObj.setRowHeight(30,1);
    }
}
```

{% endtab %}

## Formula bar

Formula bar is used to edit or enter cell data in much easier way. By default, the formula bar is enabled in the spreadsheet. Use the [`showFormulaBar`](../api/spreadsheet/#showformulabar) property to enable or disable the formula bar.

## Named Ranges

You can define a meaningful name for a cell range and use it in the formula for calculation. It makes your formula much easier to understand and maintain. You can add named ranges to the Spreadsheet in the following ways,

* Using the [`definedNames`](../api/spreadsheet/#definednames) collection, you can add multiple named ranges at initial load.
* Use the [`addDefinedName`](../api/spreadsheet/#adddefinedname) method to add a named range dynamically.
* You can remove an added named range dynamically using the [`removeDefinedName`](../api/spreadsheet/#removedefinedname) method.
* Select the range of cells, and then enter the name for the selected range in the name box.

The following code example shows the usage of named ranges support.

{% tab template="spreadsheet/defined-name", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { enableRipple } from '@syncfusion/ej2-base';
import { dataSource } from './datasource';

enableRipple(true);

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (created)="created()" (beforeDataBound)="beforeDataBound()" [showRibbon]="false" [showSheetTabs]="false">
                <e-definednames>
                  <!-- Setting names for 'categories', 'monthly spendings' and 'annual spendings' ranges. -->
                  <e-definedname name="Categories" refersTo="=Budget Details!A3:A11"></e-definedname>
                  <e-definedname name="MonthlySpendings" refersTo="=Budget Details!B3:B11"></e-definedname>
                  <e-definedname name="AnnualSpendings" refersTo="=Budget Details!C3:C11"></e-definedname>
                </e-definednames>
                <e-sheets>
                  <e-sheet name="Budget Details">
                    <e-ranges>
                      <e-range [dataSource]="data" startCell="A2"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=150></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                      <e-column [width]=120></e-column>
                    </e-columns>
                    <e-rows>
                      <e-row [height]=40 [customHeight]="true">
                        <e-cells>
                          <e-cell value="Monthly Expense" [colSpan]=5 [style]="{ textAlign: 'center', fontWeight: 'bold', verticalAlign: 'middle', fontStyle: 'italic', fontSize: '15pt' }"></e-cell>
                          <e-cell formula="=SUM(E2:E10)"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row [index]=11>
                        <e-cells>
                          <e-cell value="Totals" [style]="{ fontStyle: 'italic', fontWeight: 'bold' }"></e-cell>
                          <!-- Initializing the formulas using defined names. -->
                          <e-cell formula="=SUM(MonthlySpendings)"></e-cell>
                          <e-cell formula="=SUM(AnnualSpendings)"></e-cell>
                          <e-cell formula="=SUM(LastYearSpendings)"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=1 value="Number of Categories" [colSpan]=2 [style]="{ fontWeight: 'bold', textAlign: 'right' }"></e-cell>
                          <e-cell [index]=3 formula="=COUNTA(Categories)"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=1 value="Average Spend" [colSpan]=2 [style]="{ fontWeight: 'bold', textAlign: 'right' }"></e-cell>
                          <e-cell [index]=3 formula="=AVERAGE(MonthlySpendings)" format="$#,##0"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=1 value="Min Spend" [colSpan]=2 [style]="{ fontWeight: 'bold', textAlign: 'right' }"></e-cell>
                          <e-cell [index]=3 formula="=MIN(MonthlySpendings)" format="$#,##0"></e-cell>
                        </e-cells>
                      </e-row>
                      <e-row>
                        <e-cells>
                          <e-cell [index]=1 value="Max Spend" [colSpan]=2 [style]="{ fontWeight: 'bold', textAlign: 'right' }"></e-cell>
                          <e-cell [index]=3 formula="=Max(MonthlySpendings)" format="$#,##0"></e-cell>
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

    beforeDataBound() {
        // Adding name dynamically for `last year spending` and `percentage change` ranges.
        this.spreadsheetObj.addDefinedName({ name: 'LastYearSpendings', refersTo: '=D3:D11' });
        this.spreadsheetObj.addDefinedName({ name: 'PercentageChange', refersTo: '=E3:E11' });
    }

    created() {
        // Removing the unwanted `PercentageChange` named range
        this.spreadsheetObj.removeDefinedName('PercentageChange', '');
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A2:E2');
        this.spreadsheetObj.numberFormat('$#,##0', 'B3:D12');
        this.spreadsheetObj.numberFormat('0%', 'E3:E12');
        this.spreadsheetObj.setRowHeight(30,1);
    }
}
```

{% endtab %}

## Supported Formulas

The list of supported formulas can be find in following [`link`](https://ej2.syncfusion.com/documentation/spreadsheet/formulas#supported-formulas).

## See Also

* [Editing](./editing)
* [Formatting](./formatting)
* [Open](./open)
* [Save](./save)
