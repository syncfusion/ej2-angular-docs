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

The following sample shows the `Open` option by using the [`openUrl`](../api/spreadsheet/#openUrl) property in the Spreadsheet control. You can also use the [`beforeOpen`](../api/spreadsheet/#beforeOpen) event to trigger before opening an Excel file.

{% tab template="spreadsheet/open-save", sourceFiles="app/**/*.ts", isDefaultActive=true , iframeHeight="450px" %}

```javascript
import { Component } from '@angular/core';
import { SpreadsheetComponent, BeforeSaveEventArgs } from '@syncfusion/ej2-angular-spreadsheet';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet (beforeOpen)='beforeOpen($event)' openUrl='https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/open' allowOpen='true'> </ejs-spreadsheet>"
})
export class AppComponent {
     beforeOpen (args: BeforeOpenEventArgs) {
        // your code snippets here
    }
}
```

{% endtab %}

Please find the below table for the beforeOpen event arguments.

 | **Parameter** | **Type** | **Description** |
| ----- | ----- | ----- |
| file | FileList or string or File | To get the file stream. `FileList` -  contains length and item index. <br/> `File` - specifies the file lastModified and file name. |
| cancel | boolean | To prevent the open operation. |
| requestData | object |  To provide the Form data. |

> * Use `Ctrl + O` keyboard shortcut to open Excel documents.
> * The default value of the [allowOpen](../api/spreadsheet/#allowopen) property is `true`. For demonstration purpose, we have showcased the [allowOpen](../api/spreadsheet/#allowopen) property in previous code snippet.

### Open an external URL excel file while initial load

You can achieve to access the remote excel file by using the [`created`](../api/spreadsheet/#created) event. In this event you can fetch the excel file and convert it to a blob. Convert this blob to a file and [`open`](../api/spreadsheet/#open) this file by using Spreadsheet component open method.

{% tab template="spreadsheet/open-save", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet #spreadsheet (created)='created()' openUrl='https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/open' allowOpen='true'> </ejs-spreadsheet>"
})
export class AppComponent {
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
     created () {
        fetch("https://js.syncfusion.com/demos/ejservices/data/Spreadsheet/LargeData.xlsx") // fetch the remote url
          .then((response) => {
            response.blob().then((fileBlob) => { // convert the excel file to blob
            let file = new File([fileBlob], "Sample.xlsx"); //convert the blob into file
            this.spreadsheetObj.open({ file: file }); // open the file into Spreadsheet
            })
          })
    }
}
```

{% endtab %}

## Save

The Spreadsheet control saves its data, style, format, and more as Excel file document. To enable this feature, set [`allowSave`](../api/spreadsheet/#allowsave) as `true` and assign service url to the [`saveUrl`](../api/spreadsheet/#saveurl) property.

**User Interface**:

In user interface, you can save Spreadsheet data as Excel document by clicking `File > Save As` menu item in ribbon.

The following sample shows the `Save` option by using the [`saveUrl`](../api/spreadsheet/#saveUrl) property in the Spreadsheet control. You can also use the [`beforeSave`](../api/spreadsheet/#beforeSave) event to trigger before saving the Spreadsheet as an Excel file.

{% tab template="spreadsheet/open-save", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component } from '@angular/core';
import { SpreadsheetComponent, BeforeSaveEventArgs } from '@syncfusion/ej2-angular-spreadsheet';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet (beforeSave)='beforeSave($event)' saveUrl='https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save' allowSave='true'> </ejs-spreadsheet>"
})
export class AppComponent {
     beforeSave (args: BeforeSaveEventArgs) {
        // your code snippets here
    }
 }
```

{% endtab %}

Please find the below table for the beforeSave event arguments.

| **Parameter** | **Type** | **Description** |
| ----- | ----- | ----- |
| url | string |  Specifies the save url.  |
| fileName | string | Specifies the file name. |
| saveType | SaveType | Specifies the saveType like Xlsx, Xls, Csv and Pdf. |
| customParams | object | Passing the custom parameters from client to server while performing save operation. |
| isFullPost | boolean | It sends the form data from client to server, when set to true. It fetches the data from client to server and returns the data from server to client, when set to false. |
| needBlobData | boolean | You can get the blob data if set to true. |
| cancel | boolean | To prevent the save operations. |

> * Use `Ctrl + S` keyboard shortcut to save the Spreadsheet data as Excel file.
> * The default value of [allowSave](../api/spreadsheet/#allowsave) property is `true`. For demonstration purpose, we have showcased the [allowSave](../api/spreadsheet/#allowsave) property in previous code snippet.
> * Demo purpose only, we have used the online web service url link.

### To send and receive custom params from client to server

Passing the custom parameters from client to server by using [`beforeSave`](../api/spreadsheet/#beforeSave) event.

{% tab template="spreadsheet/open-save", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component } from '@angular/core';
import { SpreadsheetComponent, BeforeSaveEventArgs } from '@syncfusion/ej2-angular-spreadsheet';
import { data } from './datasource';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet #spreadsheet (beforeSave)='beforeSave($event)' saveUrl='https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save' allowSave='true'> <e-sheets> <e-sheet> <e-ranges> <e-range [dataSource]='data'></e-range></e-ranges><e-columns><e-column [width]=90></e-column><e-column [width]=100></e-column><e-column [width]=96></e-column><e-column [width]=120></e-column><e-column [width]=130></e-column><e-column [width]=120></e-column></e-columns></e-sheet></e-sheets></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {
    public data: object[];
    ngOnInit(): void {
        this.data = data;
    }
    beforeSave (args: BeforeSaveEventArgs) {
        args.customParams = { customParams: 'you can pass custom params in server side'}; // you can pass the custom params
    }
 }
```

{% endtab %}

Server side code snippets:

```csharp

    public IActionResult Save(SaveSettings saveSettings, string customParams)
        {
            Console.WriteLine(customParams); // you can get the custom params in controller side
            return Workbook.Save(saveSettings);
        }
```

### Methods

To save the Spreadsheet document as an `xlsx, xls, csv, or pdf` file, by using [save](../api/spreadsheet/#save) method should be called with the `url`, `fileName` and `saveType` as parameters. The following code example shows to save the spreadsheet file as an `xlsx, xls, csv, or pdf` in the button click event.

{% tab template="spreadsheet/open-save", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript
import { Component, OnInit,ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { ItemModel, MenuEventArgs } from '@syncfusion/ej2-angular-splitbuttons';
import { data } from './datasource';

@Component({
    selector: 'app-container',
    template: "<button ejs-dropdownbutton [items]='items' content='Save' (select)='itemSelect($event)'></button> <ejs-spreadsheet #spreadsheet > <e-sheets> <e-sheet> <e-ranges> <e-range [dataSource]='data'></e-range></e-ranges><e-columns><e-column [width]=90></e-column><e-column [width]=100></e-column><e-column [width]=96></e-column><e-column [width]=120></e-column><e-column [width]=130></e-column><e-column [width]=120></e-column></e-columns></e-sheet></e-sheets></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {
    public data: object[];
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
    ngOnInit(): void {
        this.data = data;
    }
    public items: ItemModel[] = [
        {
            text: "Save As xlsx"
        },
        {
            text: "Save As xls"
        },
        {
            text: "Save As csv"
        },
        {
            text: "Save As pdf"
        }];

    public itemSelect(args: MenuEventArgs) {
    if (args.item.text === 'Save As xlsx')
      this.spreadsheetObj.save({url: 'https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save', fileName: "Sample", saveType: "Xlsx"});
    if (args.item.text === 'Save As xls')
      this.spreadsheetObj.save({url: 'https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save', fileName: "Sample", saveType: "Xls"});
    if (args.item.text === 'Save As csv')
      this.spreadsheetObj.save({url: 'https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save',fileName: "Sample", saveType: "Csv"});
    if (args.item.text === 'Save As pdf')
      this.spreadsheetObj.save({url: 'https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save',fileName: "Sample", saveType: "Pdf"});
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

## Note

You can refer to our [Angular Spreadsheet](https://www.syncfusion.com/angular-ui-components/angular-spreadsheet) feature tour page for its groundbreaking feature representations. You can also explore our [Angular Spreadsheet example](https://ej2.syncfusion.com/angular/demos/#/material/spreadsheet/default) to knows how to present and manipulate data.

## See Also

* [Filtering](./filter)
* [Sorting](./sort)
* [Hyperlink](./link)