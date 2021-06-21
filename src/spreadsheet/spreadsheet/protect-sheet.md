---
title: "Protection"
component: "Spreadsheet"
description: "This section helps you to protect and unprotect the spreadsheet."
---

# Protection

Sheet protection helps you to prevent the users from modifying the data in the spreadsheet.

## Protect Sheet

Protect sheet feature helps you to prevent the unknown users from accidentally changing, editing, moving, or deleting data in a spreadsheet.
You can use the [`isProtected`](../api/spreadsheet/#isProtected) property to enable or disable the Protecting functionality.

> * The default value for `isProtected` property is `false`.

By default in protected sheet, selecting, formatting, inserting, deleting functionalities are disabled. To enable some of the above said functionalities
the `protectSettings` options are used in a protected spreadsheet.

The available `protectSettings` options in spreadsheet are,

| Options | Uses |
|-----|------|
| `Select Cells` | Used to perform Cell Selection. |
| `Format Cells` | Used to perform Cell formatting. |
| `Format Rows` | Used to perform Row formatting. |
| `Format Columns` | Used to perform Column formatting. |
| `Insert Link` | Used to perform Hyperlink Insertions. |

> * The default value for all `protectSettings` options are `false`.

By default, the `Protect Sheet` module is injected internally into the Spreadsheet to perform sheet protection function.

**User Interface**:

In the active Spreadsheet, the sheet protection can be done by any of the following ways:

* Select the Protect Sheet item in the Ribbon toolbar under the Data Tab, and then select your desired options.
* Right-click the sheet tab, select the Protect Sheet item in the context menu, and then select your desired options.
* Use the [`protectSheet()`](../api/spreadsheet/#protectSheet) method programmatically.

The following example shows `Protect Sheet` functionality in the Spreadsheet control.

{% tab template="spreadsheet/protect-sheet", sourceFiles="app/**/*.ts", isDefaultActive=true, iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { enableRipple } from '@syncfusion/ej2-base';
import { dataSource1, dataSource2 } from './datasource';

enableRipple(true);

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (created)="created()">
                <e-sheets>
                  <e-sheet name="Budget" [isProtected]="true" [protectSettings]="{ selectCells: true }">
                    <e-ranges>
                      <e-range [dataSource]="budgetData"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                    </e-columns>
                  </e-sheet>
                  <e-sheet name="Salary">
                    <e-ranges>
                      <e-range [dataSource]="salaryData"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
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

    budgetData: object[] = dataSource1;

    salaryData: object[] = dataSource2;

    created() {
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:D1');
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold'}, 'A11:D11');
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'Salary!A1:D1');
        this.spreadsheetObj.protectSheet(1, { selectCells: false});
    }
}
```

{% endtab %}

## Unprotect Sheet

Unprotect sheet is used to enable all the functionalities that are already disabled in a protected spreadsheet.

**User Interface**:

In the active Spreadsheet, the sheet Unprotection can be done by any of the following ways:

* Select the `Unprotect Sheet` item in the Ribbon toolbar under the Data Tab.
* Right-click the sheet tab, select the `Unprotect Sheet` item in the context menu.
* Use the [`unprotectSheet()`](../api/spreadsheet/#unprotectSheet) method programmatically.

## Unlock the particular cells in the protected sheet

In protected spreadsheet, to make some particular cell or range of cells are editable, you can use [`lockCells()`](../api/spreadsheet/#lockCells) method, with the parameter `range` and `isLocked` property as false.

{% tab template="spreadsheet/lock-cells", sourceFiles="app/**/*.ts", iframeHeight="480px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { Dialog } from '@syncfusion/ej2-popups';
import { enableRipple } from '@syncfusion/ej2-base';
import { dataSource1, dataSource2 } from './datasource';

enableRipple(true);

@Component({
    selector: 'app-container',
    template: `<button class="e-btn" style="margin: 5px 0;" (click)="btnClick()">
                Unlock cells</button>
              <div id="dialog"></div>
              <ejs-spreadsheet #spreadsheet id="spreadsheet" (created)="created()">
                <e-sheets>
                  <e-sheet name="Budget" [isProtected]="true" [protectSettings]="{ selectCells: true }">
                    <e-ranges>
                      <e-range [dataSource]="budgetData"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
                    </e-columns>
                  </e-sheet>
                  <e-sheet name="Salary">
                    <e-ranges>
                      <e-range [dataSource]="salaryData"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=100></e-column>
                      <e-column [width]=100></e-column>
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

    dialogObj: Dialog;

    budgetData: object[] = dataSource1;

    salaryData: object[] = dataSource2;

    created() {
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:D1');
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold'}, 'A11:D11');
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'Salary!A1:D1');

        // Creating dialog component,
        this.dialogObj = new Dialog({
            header: 'Spreadsheet',
            target: document.getElementById('spreadsheet'),
            content: '"A1:F3" range of cells has been unlocked.',
            showCloseIcon: true,
            isModel: true,
            visible: false,
            width: '500px',
            buttons: [{
                click: this.lockCells.bind(this), buttonModel: { content: 'Ok', isPrimary: true }
            }];
        });
        this.dialogObj.appendTo('#dialog');
    }

    btnClick (): void {
        this.dialogObj.show();
    }

    lockCells(): void {
        this.spreadsheetObj.lockCells('A1:F3', false);
        this.dialogObj.hide();
    }
}
```

{% endtab %}

## Limitations of Protect Sheet

* Password protection is not supported in Protect sheet feature.

## Protect Workbook

Protect workbook feature helps you to protect the workbook so that users cannot insert, delete, rename, hide the sheets in the spreadsheet.
You can use the [`password`](../api/spreadsheet/#password) property to protect workbook with password.
You can use the [`isProtected`](../api/spreadsheet/#isProtected) property to protect or unprotect the workbook without the password.

> The default value for `isProtected` property is `false`.

**User Interface**:

In the active Spreadsheet, you can protect the worksheet by selecting the Data tab in the Ribbon toolbar and choosing the `Protect Workbook` item. Then, enter the password and confirm it and click on OK.

The following example shows `Protect Workbook` by using the [`isProtected`](../api/spreadsheet/#isProtected) property in the Spreadsheet control.

{% tab template="spreadsheet/local-data-binding", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component, OnInit,ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { data } from './datasource';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet #spreadsheet [isProtected]='true'> <e-sheets> <e-sheet> <e-ranges> <e-range [dataSource]='data'></e-range></e-ranges><e-columns><e-column [width]=90></e-column><e-column [width]=100></e-column><e-column [width]=96></e-column><e-column [width]=120></e-column><e-column [width]=130></e-column><e-column [width]=120></e-column></e-columns></e-sheet></e-sheets></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {
    public data: object[];
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
    ngOnInit(): void {
        this.data = data;
    }
  };
}
```

{% endtab %}

The following example shows `Protect Workbook` by using the [`password`](../api/spreadsheet/#password) property in the Spreadsheet control. To unprotect the workbook, click the unprotect workbook button in the data tab and provide the password as syncfusion in the dialog box.

{% tab template="spreadsheet/local-data-binding", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component, OnInit,ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { data } from './datasource';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet #spreadsheet password='syncfusion'> <e-sheets> <e-sheet> <e-ranges> <e-range [dataSource]='data'></e-range></e-ranges><e-columns><e-column [width]=90></e-column><e-column [width]=100></e-column><e-column [width]=96></e-column><e-column [width]=120></e-column><e-column [width]=130></e-column><e-column [width]=120></e-column></e-columns></e-sheet></e-sheets></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {
    public data: object[];
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
    ngOnInit(): void {
        this.data = data;
    }
  };
}
```

{% endtab %}

## Unprotect Workbook

Unprotect Workbook is used to enable the insert, delete, rename, move, copy, hide or unhide sheets feature  in the spreadsheet.

**User Interface**:

In the active Spreadsheet, the workbook Unprotection can be done in any of the following ways:

* Select the `Unprotect Workbook` item in the Ribbon toolbar under the Data Tab and provide the valid password in the dialog box.

## Limitations of Protect Workbook

* Encryption with password is not supported in the Protect workbook feature.

## Note

You can refer to our [Angular Spreadsheet](https://www.syncfusion.com/angular-ui-components/angular-spreadsheet) feature tour page for its groundbreaking feature representations. You can also explore our [Angular Spreadsheet example](https://ej2.syncfusion.com/angular/demos/#/material/spreadsheet/default) to knows how to present and manipulate data.

## See Also

* [Hyperlink](./link)