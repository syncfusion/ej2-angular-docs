---
title: "Undo Redo"
component: "Spreadsheet"
description: "This section helps you to revert the last action performed and revert the last undo action performed with Spreadsheet."
---

# Undo and Redo

`Undo` option helps you to undone the last action performed and `Redo` option helps you to do the same action which is reverted in the Spreadsheet. You can use the [`allowUndoRedo`](../api/spreadsheet/#allowundoredo) property to enable or disable undo redo functionality in spreadsheet.

> * The default value for `allowUndoRedo` property is `true`.

By default, the `UndoRedo` module is injected internally into Spreadsheet to perform undo redo.

## Undo

It reverses the last action you performed with Spreadsheet. Undo can be done by any of the following ways:

* Select the undo item from HOME tab in Ribbon toolbar.
* Use `Ctrl + Z` keyboard shortcut to perform the undo.
* Use the [`undo`](../api/spreadsheet/#undo) method programmatically.

## Redo

It reverses the last undo action you performed with Spreadsheet. Redo can be done by any of the following ways:

* Select the redo item from HOME tab in Ribbon toolbar.
* Use `Ctrl + Y` keyboard shortcut to perform the redo.
* Use the [`redo`](../api/spreadsheet/#redo) method programmatically.

## Update custom actions in UndoRedo collection

You can update your own custom actions in UndoRedo collection, by using the [`updateUndoRedoCollection`](../api/spreadsheet/#updateUndoRedoCollection) method. And also customize the undo redo operations of your custom action by using `actionComplete` event.

The following code example shows `How to update and customize your own actions for undo redo` functionality in the Spreadsheet control.

{% tab template="spreadsheet/undo-redo", sourceFiles="app/**/*.ts", isDefaultActive=true , iframeHeight="450px" %}

```javascript
import { Component, OnInit,ViewChild } from '@angular/core';
import { defaultData } from './datasource';
import { addClass, removeClass } from '@syncfusion/ej2-base';
import { SpreadsheetComponent, getRangeIndexes } from '@syncfusion/ej2-angular-spreadsheet';

@Component({
    selector: 'app-container',
    template: "<button id='customBtn' class='e-btn' (click)='updateCollection()'> add/remove Class</button>   <ejs-spreadsheet #spreadsheet (actionComplete)='actionComplete($event)'> <e-sheets> <e-sheet> <e-ranges> <e-range [dataSource]='defaultData'></e-range></e-ranges><e-columns><e-column [width]=130></e-column><e-column [width]=92></e-column><e-column [width]=96></e-column></e-columns></e-sheet></e-sheets></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {

    public defaultData: object[];
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
    ngOnInit(): void {
        this.defaultData = defaultData;
    }
    actionComplete (args) {
        let actionEvents: any = args;
        if (actionEvents.eventArgs.action == "customCSS") {
            let Element:HTMLElement = this.spreadsheetObj.getCell(actionEvents.eventArgs.rowIdx,actionEvents.eventArgs.colIdx);
            if (actionEvents.eventArgs.requestType == "undo") {
                removeClass([Element],'customClass'); // To remove the custom class in undo action
            }
            else {
                addClass([Element],'customClass');// To add the custom class in redo action
            }
        }
    }
    updateCollection() {
        var cell = this.spreadsheetObj.getActiveSheet().activeCell;
        var cellIdx = getRangeIndexes(cell);
        var Element= this.spreadsheetObj.getCell(cellIdx[0], cellIdx[1]);
        if (!Element.classList.contains("customClass")) {
            Element.classList.add('customClass'); // To add the custom class in active cell element
            this.spreadsheetObj.updateUndoRedoCollection({ eventArgs: { class: 'customClass', rowIdx: cellIdx[0], colIdx: cellIdx[1], action: 'customCSS' } }); // To update the undo redo collection
        }
  }
}

```

{% endtab %}

## See Also

* [Sorting](./sort)
* [Filtering](./filter)
* [Hyperlink](./link)