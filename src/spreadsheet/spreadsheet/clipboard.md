---
title: "Clipboard"
component: "Spreadsheet"
description: "This section explains you about the Clipboard feature (cut, copy, paste) in the Essential JS 2 spreadsheet."
---

# Clipboard

The Spreadsheet provides support for the clipboard operations (cut, copy, and paste). Clipboard operations can be enabled or disabled by setting the [`enableClipboard`](../api/spreadsheet/#enableclipboard) property in Spreadsheet.

> By default, the `enableClipboard` property is true.

## Cut

It is used to cut the data from selected range of cells, rows or columns in a spreadsheet and make it available in the clipboard.

**User Interface**:

Cut can be done in one of the following ways.

* Using Cut button in the Ribbon’s HOME tab to perform cut operation.
* Using Cut option in the Context Menu.
* Using `Ctrl + X` | `Command + X` keyboard shortcut.
* Using the [`cut`](../api/spreadsheet/#cut) method.

## Copy

It is used to copy the data from selected range of cells, rows or columns in a spreadsheet and make it available in the clipboard.

**User Interface**:

Copy can be done in one of the following ways.

* Using Copy button in the Ribbon’s HOME tab to perform copy operation.
* Using Copy option in the Context Menu.
* Using `Ctrl + C` | `Command + C` keyboard shortcut.
* Using the [`copy`](../api/spreadsheet/#copy) method.

## Paste

It is used to paste the clipboard data to the selected range, rows or columns. You have the following options in Paste,

* `Paste Special` - You can paste the values with formatting.
* `Paste` - You can paste only the values without formatting.

It also performs for external clipboard operation. If you perform cut and paste, clipboard data will be cleared, whereas in copy and paste the clipboard contents will be maintained. If you perform paste inside the copied range, the clipboard data will be cleared.

**User Interface**:

Paste can be done in one of the following ways.

* Using Paste button in the Ribbon’s HOME tab to perform paste operation.
* Using Paste option in the Context Menu.
* Using `Ctrl + V` | `Command + V` keyboard shortcut.
* Using the [`paste`](../api/spreadsheet/#paste) method.

> If you use the Keyboard shortcut key for cut (`Ctrl + X`) | copy (`Ctrl + C`) from other sources, you should use `Ctrl + V` shortcut while pasting into the spreadsheet.

{% tab template="spreadsheet/clipboard", sourceFiles="app/**/*.ts", isDefaultActive=true, iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { enableRipple } from '@syncfusion/ej2-base';
import { dataSource1 } from './datasource';

enableRipple(true);

@Component({
    selector: 'app-container',
    template: `<button ejs-dropdownbutton [items]='items' content='Clipboard' (select)='itemSelect($event)'></button>
    <ejs-spreadsheet #spreadsheet (created)="created()" [enableClipboard]="true">
                <e-sheets>
                  <e-sheet name="Price Details">
                    <e-ranges>
                      <e-range [dataSource]="priceData"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=130></e-column>
                      <e-column [width]=92></e-column>
                      <e-column [width]=96></e-column>
                    </e-columns>
                  </e-sheet>
                </e-sheets>
              </ejs-spreadsheet>`
})
export class AppComponent {
    @ViewChild('spreadsheet')
    spreadsheetObj: SpreadsheetComponent;

    priceData: object[] = dataSource1;
    public items: ItemModel[] = [
        {
          text: "Copy"
        },
        {
          text: "Cut"
        },
        {
          text: "Paste"
        }];

    created() {
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:H1');
    }
    public itemSelect(args: MenuEventArgs) {
    if (args.item.text === 'Copy')
      spreadsheet.copy();
    if (args.item.text === 'Cut')
      spreadsheet.cut();
    if (args.item.text === 'Paste')
      spreadsheet.paste();
  }
}
```

{% endtab %}

## Prevent the paste functionality

The following example shows, how to prevent the paste action in spreadsheet. In [`actionBegin`](../api/spreadsheet/#actionbegin) event, you can set `cancel` argument as false in paste request type.

{% tab template="spreadsheet/clipboard", sourceFiles="app/**/*.ts", isDefaultActive=true, iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { enableRipple } from '@syncfusion/ej2-base';
import { dataSource1 } from './datasource';

enableRipple(true);

@Component({
    selector: 'app-container',
    template: `<button ejs-dropdownbutton [items]='items' content='Clipboard' (select)='itemSelect($event)'></button>
    <ejs-spreadsheet #spreadsheet (created)="created()" (actionBegin)="actionBeginHandler()" [enableClipboard]="true">
                <e-sheets>
                  <e-sheet name="Price Details">
                    <e-ranges>
                      <e-range [dataSource]="priceData"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=130></e-column>
                      <e-column [width]=92></e-column>
                      <e-column [width]=96></e-column>
                    </e-columns>
                  </e-sheet>
                </e-sheets>
              </ejs-spreadsheet>`
})
export class AppComponent {
    @ViewChild('spreadsheet')
    spreadsheetObj: SpreadsheetComponent;

    priceData: object[] = dataSource1;
    public items: ItemModel[] = [
        {
          text: "Copy"
        },
        {
          text: "Cut"
        },
        {
          text: "Paste"
        }];

    created() {
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:H1');
    }
    // Triggers before the action begins.
    actionBeginHandler(pasteArgs) {
      // To cancel the paste action.
        if (pasteArgs.args.eventArgs.requestType === 'paste') {
            pasteArgs.args.eventArgs.cancel = true;
        }
    }
    public itemSelect(args: MenuEventArgs) {
    if (args.item.text === 'Copy')
      spreadsheet.copy();
    if (args.item.text === 'Cut')
      spreadsheet.cut();
    if (args.item.text === 'Paste')
      spreadsheet.paste();
  }
}
```

{% endtab %}

## Limitations

* External clipboard is not fully supported while copying data from another source and pasting into a spreadsheet, it only works with basic supports (Values, Number, cell, and Text formatting).
* If you copy =SUM(A2,B2) and paste, the formula reference will change depending on the pasted cell address but we don't have support for nested formula(formula reference will be same).
* Clipboard is not supported with conditional formatting (values only pasting).
* We have limitation while copying the whole sheet data and pasting it into another sheet.