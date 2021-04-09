---
title: "Open and Save"
component: "Spreadsheet"
description: "This section helps to learn how to open and save excel file in Spreadsheet control"
---

# Open and Save

In import an excel file, it needs to be read and converted to client side Spreadsheet model. The converted client side Spreadsheet model is sent as JSON which is used to render Spreadsheet. Similarly, when you save the Spreadsheet, the client Spreadsheet model is sent to the server as JSON for processing and saved. Server configuration is used for this process.

## Open

The Spreadsheet control opens an Excel document with its data, style, format, and more. To enable this feature, set [`allowOpen`](../api/spreadsheet/#allowopen) as `true` and assign service url to the [`openUrl`](../api/spreadsheet/#openurl) property.

**User Interface**:

In user interface you can open an Excel document by clicking `File > Open` menu item in ribbon.

The following code example shows `Open` option in the Spreadsheet control.

{% tab template="spreadsheet/open-save", sourceFiles="app/**/*.ts", isDefaultActive=true , iframeHeight="450px" %}

```javascript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet openUrl='https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/open' allowOpen='true'> </ejs-spreadsheet>"
})
export class AppComponent { }
```

{% endtab %}

> * Use `Ctrl + O` keyboard shortcut to open Excel documents.
> * The default value of the [allowOpen](../api/spreadsheet/#allowopen) property is `true`. For demonstration purpose, we have showcased the [allowOpen](../api/spreadsheet/#allowopen) property in previous code snippet.

## Save

The Spreadsheet control saves its data, style, format, and more as Excel file document. To enable this feature, set [`allowSave`](../api/spreadsheet/#allowsave) as `true` and assign service url to the [`saveUrl`](../api/spreadsheet/#saveurl) property.

**User Interface**:

In user interface, you can save Spreadsheet data as Excel document by clicking `File > Save As` menu item in ribbon.

The following code example shows `Save` option in the Spreadsheet control.

{% tab template="spreadsheet/open-save", sourceFiles="app/**/*.ts", isDefaultActive=true , iframeHeight="450px" %}

```javascript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet saveUrl='https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save' allowSave='true'> </ejs-spreadsheet>"
})
export class AppComponent { }
```

{% endtab %}

> * Use `Ctrl + S` keyboard shortcut to save the Spreadsheet data as Excel file.
> * The default value of [allowSave](../api/spreadsheet/#allowsave) property is `true`. For demonstration purpose, we have showcased the [allowSave](../api/spreadsheet/#allowsave) property in previous code snippet.

### Methods

To save the Spreadsheet document as an `xlsx, xls, csv, or pdf` file, by using [save](../api/spreadsheet/#save) method should be called with the `url`, `fileName` and `saveType` as parameters. The following code example shows to save the spreadsheet file as an `xlsx, xls, csv, or pdf` in the button click event.

{% tab template="spreadsheet/local-data-binding", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component, OnInit,ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { data } from './datasource';

@Component({
    selector: 'app-container',
    template: `<button class="e-btn e-primary" (click)="xlsx()" >Save As xlsx</button>
    <button class="e-btn e-primary" (click)="xls()" >Save As xls</button>
    <button class="e-btn e-primary" (click)="csv()" >Save As csv</button>
    <button class="e-btn e-primary" (click)="pdf()" >Save As pdf</button>
    <ejs-spreadsheet #spreadsheet> <e-sheets> <e-sheet> <e-ranges> <e-range [dataSource]='data'></e-range></e-ranges><e-columns><e-column [width]=90></e-column><e-column [width]=100></e-column><e-column [width]=96></e-column><e-column [width]=120></e-column><e-column [width]=130></e-column><e-column [width]=120></e-column></e-columns></e-sheet></e-sheets></ejs-spreadsheet>`
})
export class AppComponent implements OnInit {
    public data: object[];
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
    xlsx(): void {
        this.spreadsheetObj.save({url: 'https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save', fileName: "Sample", saveType: "Xlsx"});
    }
    xls(): void {
        this.spreadsheetObj.save({url: 'https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save', fileName: "Sample", saveType: "Xls"});
    }
    csv(): void {
        this.spreadsheetObj.save({url: 'https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save', fileName: "Sample", saveType: "Csv"});
    }
    pdf(): void {
        this.spreadsheetObj.save({url: 'https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save', fileName: "Sample", saveType: "Pdf"});
    }
    ngOnInit(): void {
        this.data = data;
    }
  };
}
```

{% endtab %}

## Server Configuration

In Spreadsheet control, Excel import and export support processed in `server-side`, to use importing and exporting in your projects, it is required to create a server with any of the following web services.

* WebAPI
* WCF Service
* ASP.NET MVC Controller Action

> * [Refer](../api/spreadsheet/#allowsave) to the link about, perform an Excel import and export operation with help of `WebAPI` configuration.

## Supported File Formats

The following list of Excel file formats are supported in Spreadsheet:

* MS Excel (.xlsx)
* MS Excel 97-2003 (.xls)
* Comma Separated Values (.csv)

## See Also

* [Filtering](./filter)
* [Sorting](./sort)
* [Hyperlink](./link)