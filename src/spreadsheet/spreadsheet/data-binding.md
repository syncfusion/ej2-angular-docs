---
title: "Data Binding"
component: "Spreadsheet"
description: "Learn how to bind local and remote data, change data dynamically, datasource change event in the Essential JS 2 Spreadsheet control."
---

# Data Binding

The Spreadsheet uses [`DataManager`](../data), which supports both RESTful JSON data services and local JavaScript object array binding to a range. The `dataSource` property can be assigned either with the instance of [`DataManager`](../data) or JavaScript object array collection.

> To bind data to a cell, use `cell data binding` support.

## Local data

To bind local data to the Spreadsheet, you can assign a JavaScript object array to the `dataSource` property.

Refer to the following code example for local data binding.

{% tab template="spreadsheet/local-data-binding", sourceFiles="app/**/*.ts", isDefaultActive=true , iframeHeight="450px" %}

```javascript
import { Component, OnInit,ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { data } from './datasource';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet #spreadsheet> <e-sheets> <e-sheet> <e-ranges> <e-range [dataSource]='data'></e-range></e-ranges><e-columns><e-column [width]=90></e-column><e-column [width]=100></e-column><e-column [width]=96></e-column><e-column [width]=120></e-column><e-column [width]=130></e-column><e-column [width]=120></e-column></e-columns></e-sheet></e-sheets></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {
    public data: object[];
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
    ngOnInit(): void {
        this.data = data;
    }
  };
```

{% endtab %}

> The local data source can also be provided as an instance of the [`DataManager`](../data). By default, [`DataManager`](../data) uses [`JsonAdaptor`](../data/adaptors/#json-adaptor) for local data-binding.

## Remote data

To bind remote data to the Spreadsheet control, assign service data as an instance of [`DataManager`](../data) to the `dataSource` property. To interact with remote data source, provide the service endpoint `url`.

Refer to the following code example for remote data binding.

{% tab template="spreadsheet/remote-data-binding", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript

import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet #spreadsheet><e-sheets><e-sheet name='Shipment Details'> <e-ranges> <e-range [showFieldAsHeader]='false' startCell='A2' [dataSource]='data' [query]='query'>  </e-range> </e-ranges><e-rows><e-row><e-cells><e-cell value='Order ID'></e-cell> <e-cell value='Customer Name'></e-cell> <e-cell value='Freight'></e-cell>  <e-cell value='Ship Name'></e-cell><e-cell value='Ship City'></e-cell> <e-cell value='Ship Country'></e-cell></e-cells> </e-row></e-rows><e-columns><e-column [width]=100></e-column>  <e-column [width]=130></e-column> <e-column [width]=100></e-column>  <e-column [width]=220></e-column>  <e-column [width]=150></e-column> <e-column [width]=180></e-column>  </e-columns> </e-sheet></e-sheets></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {
  
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
    public query: Query = new Query().select(['OrderID', 'CustomerID', 'ShipName', 'ShipCity', 'ShipCountry', 'Freight']).take(200);
    public data: DataManager = new DataManager({
        url: 'https://js.syncfusion.com/demos/ejServices//wcf/Northwind.svc/Orders',
        crossDomain: true
    });
    ngOnInit(): void {
        this.data = this.data;
    }
}

```

{% endtab %}

> By default, `DataManager` uses **ODataAdaptor** for remote data-binding.

### Binding with OData services

`OData` is a standardized protocol for creating and consuming data. You can retrieve data from OData service using the DataManager. Refer to the following code example for remote Data binding using OData service.

{% tab template="spreadsheet/remote-data-binding", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript

import { Component, OnInit } from '@angular/core';
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet #spreadsheet (created)='created()'> <e-sheets> <e-sheet> <e-ranges> <e-range [dataSource]='data'></e-range></e-ranges><e-columns><e-column [width]=80></e-column><e-column [width]=80></e-column><e-column [width]=80></e-column><e-column [width]=80></e-column><e-column [width]=80></e-column><e-column [width]=80></e-column><e-column [width]=280></e-column><e-column [width]=180></e-column><e-column [width]=80></e-column><e-column [width]=180></e-column><e-column [width]=180></e-column></e-columns> </e-sheet></e-sheets></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {
  
    public data: DataManager;

    ngOnInit(): void {
        this.data = new DataManager({
            url: 'https://ej2services.syncfusion.com/production/web-services/api/Orders',
            adaptor: new ODataAdaptor(),
            crossDomain: true
        });
    }

    created(){
         //Applies cell and number formatting to specified range of the active sheet
          spreadsheet.cellFormat({ fontWeight: 'bold', textAlign: 'center', verticalAlign: 'middle' },
            'A1:K1');
    };
}

```

{% endtab %}

### Web API

You can use WebApiAdaptor to bind spreadsheet with Web API created using OData endpoint.

{% tab template="spreadsheet/remote-data-binding", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript

import { Component, OnInit } from '@angular/core';
import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet #spreadsheet (created)='created()'> <e-sheets> <e-sheet> <e-ranges> <e-range [dataSource]='data'></e-range></e-ranges><e-columns><e-column [width]=80></e-column><e-column [width]=80></e-column><e-column [width]=80></e-column><e-column [width]=80></e-column><e-column [width]=80></e-column><e-column [width]=80></e-column><e-column [width]=280></e-column><e-column [width]=180></e-column><e-column [width]=80></e-column><e-column [width]=180></e-column><e-column [width]=180></e-column></e-columns> </e-sheet></e-sheets></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {
  
    public data: DataManager;

    ngOnInit(): void {
        this.data = new DataManager({
            url: 'https://ej2services.syncfusion.com/production/web-services/api/Orders',
            adaptor: new WebApiAdaptor(),
            crossDomain: true
        });
    }

    created(){
         //Applies cell and number formatting to specified range of the active sheet
          spreadsheet.cellFormat({ fontWeight: 'bold', textAlign: 'center', verticalAlign: 'middle' },
            'A1:K1');
    };
}

```

{% endtab %}

## Cell data binding

The Spreadsheet control can bind the data to individual cell in a sheet . To achive this you can use the
`value` property.

Refer to the following code example for cell data binding.

{% tab template="spreadsheet/cell-data-binding", sourceFiles="app/**/*.ts", iframeHeight="450px" %}

```javascript

import { Component, OnInit,ViewChild } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet #spreadsheet> <e-sheets> <e-sheet selectedRange='D13'><e-rows> <e-row><e-cells> <e-cell value='Order ID'></e-cell> <e-cell value='Customer ID'></e-cell> <e-cell value='Employee ID'></e-cell>  <e-cell value='Ship Name'></e-cell> <e-cell value='Ship City'></e-cell>  <e-cell value='Ship Address'></e-cell>  </e-cells>  </e-row>  <e-row>  <e-cells>  <e-cell value='10248'></e-cell>  <e-cell value='VINET'></e-cell>  <e-cell value='5'></e-cell>  <e-cell value='Vins et alcools Chevalier'></e-cell>  <e-cell value='Reims'></e-cell>  <e-cell value='59 rue de lAbbaye'></e-cell>  </e-cells>  </e-row>  <e-row>  <e-cells>  <e-cell value='10249'></e-cell>  <e-cell value='TOMSP'></e-cell>  <e-cell value='3'></e-cell> <e-cell value='Toms Spezialitäten'></e-cell>  <e-cell value='Münster'></e-cell>  <e-cell value='Luisenstr. 48'></e-cell>  </e-cells>  </e-row>  <e-row>  <e-cells>  <e-cell value='10250'></e-cell>  <e-cell value='HANAR'></e-cell>  <e-cell value='2'></e-cell>  <e-cell value='Hanari Carnes'></e-cell>  <e-cell value='Rio de Janeiro'></e-cell> <e-cell value='Rua do Paço, 67'></e-cell> </e-cells>  </e-row>  <e-row>  <e-cells> <e-cell value='10251'></e-cell>  <e-cell value='VICTE'></e-cell> <e-cell value='3'></e-cell> <e-cell value='Victuailles en stock'></e-cell> <e-cell value='Lyon'></e-cell>  <e-cell value='2, rue du Commerce'></e-cell> </e-cells> </e-row> <e-row> <e-cells> <e-cell value='10252'></e-cell>  <e-cell value='SUPRD'></e-cell>   <e-cell value='4'></e-cell><e-cell value='Suprêmes délices'></e-cell><e-cell value='Charleroi'></e-cell><e-cell value='Boulevard Tirou, 255'></e-cell></e-cells></e-row></e-rows><e-columns><e-column [width]=110></e-column><e-column [width]=115></e-column><e-column [width]=110></e-column> <e-column [width]=130></e-column> <e-column [width]=140></e-column><e-column [width]=150></e-column> </e-columns></e-sheet></e-sheets><e-rows></e-rows></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
}

```

{% endtab %}

> The cell data binding also supports formula, style, number format, and more.

## Dynamic data binding and Datasource change event

You can dynamically change the datasource of the spreadsheet by changing the model which is bound to the `dataSource` property or by changing the `dataSource` property of the `range` object of the `sheet` directly. The `dataSourceChanged` event handler will be triggered when editing, inserting, and deleting a row in the datasource range. This event will be triggered with a parameter named `action` which indicates the `edit`, `add` and `delete` actions for the respective ones.

The following table defines the arguments of the `dataSourceChanged` event.

| Property | Type | Description |
|-----|-----|-------|
| action | string | Indicates the type of action such as `edit`, `add`, and `delete` performed in the datasource range. |
| data | object[] | Modified data for `edit` action; New data for `add` action; Deleted data for `delete` action. |
| rangeIndex | number | Specifies the range index of the datasource. |
| sheetIndex | number | Specifies the sheet index of the datasource. |

> For `add` action, the value for all the fields will be `null` in the data. In the case that you do not want the primary key field to be null which needs to be updated in the backend service, you can use `edit` action after updating the primary key field to update in the backend service. <br><br>
> For inserting a row at the end of the datasource range, you should insert a row below at the end of the range to trigger the `dataSourceChanged` event with action `add`.

{% tab template="spreadsheet/dynamic-data-binding", sourceFiles="app/**/*.ts", iframeHeight="725px" %}

```javascript
import { Component, OnInit,ViewChild, ViewEncapsulation } from '@angular/core';
import { SpreadsheetComponent } from '@syncfusion/ej2-angular-spreadsheet';
import { DataSourceChangedEventArgs } from '@syncfusion/ej2-spreadsheet';
import { data, itemData } from './datasource';

@Component({
    selector: 'app-container',
    template: `<div>
    <div>
    <button class='e-btn' style="margin-bottom: 10px;" (click)='changeDataSource()'>Change Datasource</button>
    <ejs-spreadsheet #spreadsheet (dataSourceChanged)='dataSourceChanged($event)' [showRibbon]='false'>
    <e-sheets>
     <e-sheet>
        <e-ranges><e-range [dataSource]='data'></e-range></e-ranges>
        <e-columns><e-column [width]=90></e-column><e-column [width]=100></e-column><e-column [width]=96></e-column><e-column [width]=120></e-column><e-column [width]=130></e-column><e-column [width]=120></e-column></e-columns>
      </e-sheet>
      </e-sheets>
      </ejs-spreadsheet>
         </div>
         <div>
            <h4><b>Event Trace</b></h4>
            <div id="evt">
               <div style="height:173px;overflow: auto;min-width: 250px;">
                  <span #EventLog class="EventLog" id="EventLog" style="word-break: normal;"></span>
                </div>
                <button class='e-btn' (click)='clearTrace($event)'>Clear</button>
                </div>
            </div>
        </div>`
        styles: [`
       #EventLog b {
         color: #388e3c;
        }
       #evt {
         border: 1px solid #dcdcdc;
         padding: 10px;
       }
        `],
        encapsulation: ViewEncapsulation.None

})
export class AppComponent {
    public data: object[] = data;
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
    @ViewChild('EventLog') EventLogEle: any;

    dataSourceChanged(args: DataSourceChangedEventArgs): void {
        this.appendElement("Data source changed with" + "<b>&nbsp;" + args.action + "</b> action<hr>");
    }

    changeDataSource(): void {
      this.data = itemData;
      // You can also change the datasource of the range by changing dataSource property of the range by using below line of code.
      // this.spreadsheetObj.sheets[0].ranges[0].dataSource = itemData;
    }

    clearTrace(event): void {
      this.EventLogEle.nativeElement.innerHTML = "";
    }

   appendElement(html: string): void {
     let span: HTMLElement = document.createElement("span");
     span.innerHTML = html;
     let log: HTMLElement = this.EventLogEle.nativeElement;
     log.insertBefore(span, log.firstChild);
   }
  };
}
```

{% endtab %}

## Note

You can refer to our [Angular Spreadsheet](https://www.syncfusion.com/angular-ui-components/angular-spreadsheet) feature tour page for its groundbreaking feature representations. You can also explore our [Angular Spreadsheet example](https://ej2.syncfusion.com/angular/demos/#/material/spreadsheet/default) to knows how to present and manipulate data.

## See Also

* [Filtering](./filter)
* [Sorting](./sort)
* [Hyperlink](./link)
* [`Collaborative Editing`](use-cases/collaborative-editing)