---
title: "FreezePane"
component: "Spreadsheet"
description: "This section helps you to learn how to freeze and unfreeze a row and column in the Spreadsheet control."
---

# FreezePanes

Freeze Panes helps you to keep particular rows or columns visible when scrolling the sheet content in the spreadsheet. You can specify the number of frozen rows and columns using the [`frozenRows`](../api/spreadsheet/#frozenRows) and [`frozenColumns`](../api/spreadsheet/#frozenColumns) properties inside the [`Sheet`](../api/spreadsheet#sheets) property.

## Apply freezepanes on UI

**User Interface**:

In the active spreadsheet, click the cell where you want to create freeze panes. Freeze panes can be done in any of the following ways:

* Select the View tab in the Ribbon toolbar and choose the `Freeze Panes` item.
* Use the [`freezePanes`](../api/spreadsheet/#freezePanes) method programmatically.

## FrozenRows

It allows you to keep a certain number of rows visible while scrolling vertically through the rest of the worksheet.

**User Interface**:

In the active spreadsheet, select the cell where you want to create frozen rows. Frozen rows can be done in any one of the following ways:

* Select the View tab in the Ribbon toolbar and choose the `Freeze Rows` item.
* You can specify the number of frozen rows using the `frozenRows` property inside the `Sheet` property.

## FrozenColumns

It allows you to keep a certain number of columns visible while scrolling horizontally through the rest of the worksheet.

**User Interface**:

In the active spreadsheet, select the cell where you want to create frozen columns. Frozen columns can be done in any one of the following ways:

* Select the View tab in the Ribbon toolbar and choose the `Freeze Columns` item.
* You can specify the number of frozen columns using the `frozenColumns` property inside the `Sheet` property.

In this demo, the frozenColumns is set as ‘2’, and the frozenRows is set as ‘2’. Hence, the two columns on the left and the top two rows are frozen.

{% tab template="spreadsheet/freezepane", sourceFiles="app/**/*.ts", isDefaultActive=true, iframeHeight="450px" %}

```javascript

import { Component, OnInit,ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { tradeData } from './datasource';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet #spreadsheet> <e-sheets> <e-sheet [frozenRows]=2 [frozenColumns]=2> <e-ranges> <e-range [dataSource]='tradeData'></e-range></e-ranges><e-columns><e-column [width]=100></e-column><e-column [width]=120></e-column><e-column [width]=96></e-column></e-columns></e-sheet></e-sheets></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {

    public tradeData: object[];
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
    ngOnInit(): void {
        this.tradeData = tradeData;
    }
}

```

{% endtab %}

## Limitations

Freeze Panes feature is not compatible with all the features which are available in the spreadsheet and it has limited features support. Here, we have listed out the features which are not compatible with Freeze Panes feature.

* Show/hide rows and columns with freeze panes.
* Filtering support with freeze panes.
* Merging the cells between freeze and unfreeze area.

## See Also

* [Sorting](./sort)
* [Filtering](./filter)
* [Undo Redo](./undo-redo)