---
title: "Data Binding"
component: "Pivot Table"
description: "Learn about how to bind local and remote data source to the pivot table."
---
# Data Binding

## JSON

For JSON data binding, the `type` property under [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/) needs to be set as `JSON`. By default, the default value is assumed as `JSON`.

### Binding JSON data via local

In-order to bind local JSON data to the pivot table user can assign the local variable holding the JSON data to the [`dataSource`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#datasource) property under [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/).

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;

    ngOnInit(): void {

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: []
        };

        this.width = '100%';
    }
}

```

{% endtab %}

Using local variable, the JSON data can also be bound to the pivot table using [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) option with the help of `JsonAdaptor`. Here the instance of [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) holding JSON data is assigned to [`dataSource`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#datasource) property under [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/). The use of [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) is optional here.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { DataManager, JsonAdaptor } from '@syncfusion/ej2-data';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
  public dataSourceSettings: IDataOptions;
  public data: DataManager;
  public width: string;

  ngOnInit(): void {

    this.data = new DataManager({
      json: Pivot_Data,
      // tslint:disable-next-line:new-parens
      adaptor: new JsonAdaptor
    });

    this.dataSourceSettings = {
      dataSource: this.data,
      expandAll: false,
      drilledMembers: [{ name: 'Country', items: ['France'] }],
      columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
      values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
      rows: [{ name: 'Country' }, { name: 'Products' }],
      formatSettings: [{ name: 'Amount', format: 'C0' }],
      filters: []
    };
    this.width = '100%';
  }
}

```

{% endtab %}

In the meantime, the JSON data from the local *.json file type can also be connected to the pivot table via the file uploader option. Here, the resulting string after uploading the file needs to be converted to JSON data that can be assigned to the [`dataSource`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#datasource) property under [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/). The following code example illustrates the same.

```javascript

import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { Uploader } from '@syncfusion/ej2-inputs';

@Component({
    selector: 'app-container',
    template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;
    public uploadObj: Uploader;

    ngOnInit(): void {
      // Step 1: Initiate the file uploader
      this.uploadObj: Uploader = new Uploader({
      });
      this.uploadObj.appendTo('#fileupload');

      let input = document.querySelector('input[type="file"]');
      // Step 2: Add the event listener which fires when the *.JSON file is uploaded.
      input.addEventListener('change', function (e: Event) {
      // Step 3: Initiate the file reader
      let reader: FileReader = new FileReader();
      reader.onload = function () {
      // Step 4: Getting the string output which is to be parsed as JSON.
      let result: any =JSON.parse(reader.result as string);
      this.dataSourceSettings = {
            // Step 5: The JSON result to be bound as data source.
            dataSource: result
            // Step 6: The appropriate report needs to be provided here.
      };
    };
    reader.readAsText((input as any).files[0]);
    }
}

```

### Binding JSON data via remote

In-order to bind remote JSON data, mention the endpoint [`URL`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#url) under [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/) property. The [`URL`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#url) property supports both direct downloadable file (*.json) and web service URL.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
  public dataSourceSettings: IDataOptions;
  public width: string;

  ngOnInit(): void {
    this.width = '100%';
    this.dataSourceSettings = {
      url: 'https://cdn.syncfusion.com/data/sales-analysis.json',
      expandAll: false,
      rows: [
        { name: 'EnerType', caption: 'Energy Type' }
      ],
      columns: [
        { name: 'EneSource', caption: 'Energy Source' }
      ],
      values: [
        { name: 'PowUnits', caption: 'Units (GWh)' },
        { name: 'ProCost', caption: 'Cost (MM)' }
      ],
      filters: []
    };
  }
}


```

{% endtab %}

## CSV

For CSV data binding, the `type` property under [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/) needs to be set as `CSV` mandatorily.

> The CSV format is considered to be the most compact format compared to JSON since it is half the size of JSON. This helps to reduce the bandwidth while transferring to the browser.

### Binding CSV data via local

In-order to bind local CSV data to the pivot table, user needs to convert it as string array and then directly assign it to the [`dataSource`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#datasource) property under [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/).

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { isNullOrUndefined } from '@syncfusion/ej2-base';
import { csvdata } from './datasource.ts';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
  public dataSourceSettings: IDataOptions;
  public width: string;

  ngOnInit(): void {

    this.dataSourceSettings = {
      dataSource: this.getCSVData(),
      type: 'CSV',
      expandAll: false,
      enableSorting: true,
      // tslint:disable-next-line:max-line-length
      formatSettings: [{ name: 'Total Cost', format: 'C0' }, { name: 'Total Revenue', format: 'C0' }, { name: 'Total Profit', format: 'C0' }],
      drilledMembers: [{ name: 'Item Type', items: ['Baby Food'] }],
      rows: [
        { name: 'Region' },
        { name: 'Country' }
      ],
      columns: [
        { name: 'Item Type' },
        { name: 'Sales Channel' }
      ],
      values: [
        { name: 'Total Cost' },
        { name: 'Total Revenue' },
        { name: 'Total Profit' }
      ],
      filters: []
    };

    this.width = '100%';
  }
  getCSVData(): string[][] {
    const dataSource: string[][] = [];
    const jsonObject: string[] = csvdata.split(/\r?\n|\r/);
    // tslint:disable-next-line:prefer-for-of
    for (let i = 0; i < jsonObject.length; i++) {
      if (!isNullOrUndefined(jsonObject[i]) && jsonObject[i] !== '') {
        dataSource.push(jsonObject[i].split(','));
      }
    }
    return dataSource;
  }
}

```

{% endtab %}

In the meantime, the CSV data from the local *.csv file type can also be connected to the pivot table via the file uploader option. Here, the resulting string after uploading the file needs to be converted to string array that can be assigned to the [`dataSource`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#datasource) property under [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/). The following code example illustrates the same.

```javascript

import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { Uploader } from '@syncfusion/ej2-inputs';

@Component({
    selector: 'app-container',
    template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public uploadObj: Uploader;

    ngOnInit(): void {
        // Step 1: Initiate the file uploader
        this.uploadObj: Uploader = new Uploader({
        });
        this.uploadObj.appendTo('#fileupload');
        // Step 2: Add the event listener which fires when the *.CSV file is uploaded.
        let input = document.querySelector('input[type="file"]');
        input.addEventListener('change', function (e: Event) {
            // Step 3: Initiate the file reader
            let reader: FileReader = new FileReader();
            reader.onload = function () {
                // Step 4: Getting the string output which is to be converted as string[][].
                let result: string[][] = (reader.result as string).split('\n').map(function (line) {
                    return line.split(',');
                });
                this.dataSourceSettings = {
                    // Step 5: The string[][] result to be bound as data source
                    dataSource: result,
                    type: 'CSV',
                    // Step 6: The appropriate report needs to be provided here.
                };
            };
            reader.readAsText((input as any).files[0]);
        }
    }
}
```

### Binding CSV data via remote

In-order to bind remote CSV data, mention the endpoint [`URL`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#url) under [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/) property. The [`URL`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#url) property supports both direct downloadable file (*.csv) and web service URL.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { DataManager } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
  public dataSourceSettings: IDataOptions;
  public data: DataManager;
  public width: string;

  ngOnInit(): void {
    this.width = '100%';
    this.dataSourceSettings = {
      url: 'https://bi.syncfusion.com/productservice/api/sales',
      type: 'CSV',
      expandAll: false,
      enableSorting: true,
      // tslint:disable-next-line:max-line-length
      formatSettings: [{ name: 'Total Cost', format: 'C0' }, { name: 'Total Revenue', format: 'C0' }, { name: 'Total Profit', format: 'C0' }],
      drilledMembers: [{ name: 'Item Type', items: ['Baby Food'] }],
      rows: [
        { name: 'Region' },
        { name: 'Country' }
      ],
      columns: [
        { name: 'Item Type' },
        { name: 'Sales Channel' }
      ],
      values: [
        { name: 'Total Cost' },
        { name: 'Total Revenue' },
        { name: 'Total Profit' }
      ],
      filters: []
    };
  }
}

```

{% endtab %}

## Remote Data Binding

To interact with remote data source, provide the endpoint `url` within `DataManager` along with appropriate [`adaptor`](https://ej2.syncfusion.com/angular/documentation/data/adaptors.html). By default, `DataManager` uses `ODataAdaptor` for remote data-binding.

### Binding with OData services

OData is a standardized protocol for creating and consuming data. User can retrieve data from OData service using the `DataManager`. Refer to the following code example for remote data binding using OData service.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, IDataSet, PivotView } from '@syncfusion/ej2-angular-pivotview';
import { DataManager, ODataAdaptor, Query, ReturnOption } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
  public dataSourceSettings: IDataOptions;
  public data: DataManager;
  public width: string;

    ngOnInit(): void {

        this.data= new DataManager({
          url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders/',
          adaptor: new ODataAdaptor,
          crossDomain: true
        }).executeQuery(new Query().take(8)).then((e: ReturnOption) => {
          this.dataSourceSettings = {
            dataSource: e.result as IDataSet[],
            expandAll: true,
            filters: [],
            columns: [{ name: 'OrderDate'}, { name: 'ShipCity' }],
            rows: [{ name: 'OrderID' }, { name: 'CustomerID' }],
            values: [{ name: 'Freight' }]
          }
        });

        this.width = '100%';
    }
}

```

{% endtab %}

### Binding with OData V4 services

The OData V4 is an improved version of OData protocols, and the `DataManager` can be used to retrieve and consume OData V4 services. For more details on OData V4 services, refer to the [OData documentation](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752197). To bind OData V4 service, use the [`ODataV4Adaptor`](https://ej2.syncfusion.com/documentation/data/adaptors/#odatav4-adaptor).

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, IDataSet, PivotView } from '@syncfusion/ej2-angular-pivotview';
import { DataManager, ODataV4Adaptor, Query, ReturnOption } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
  public dataSourceSettings: IDataOptions;
  public data: DataManager;
  public width: string;

    ngOnInit(): void {

        this.data = new DataManager({
            adaptor: new ODataV4Adaptor,
            url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Orders/?$top=7',
            crossDomain: true
        });
        this.width = '100%';
        this.dataSourceSettings = {
            dataSource: this.data,
            expandAll: true,
            filters: [],
            columns: [{ name: 'OrderDate'}, { name: 'ShipCity' }],
            rows: [{ name: 'OrderID' }, { name: 'CustomerID' }],
            values: [{ name: 'Freight' }]
        };
    }
}

```

{% endtab %}

### Web API

User can use [`WebApiAdaptor`](https://ej2.syncfusion.com/documentation/data/adaptors/#web-api-adaptor) to bind pivot table with Web API created using OData endpoint.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, IDataSet, PivotView } from '@syncfusion/ej2-angular-pivotview';
import { DataManager, WebApiAdaptor, Query, ReturnOption } from '@syncfusion/ej2-data';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings width=width></ejs-pivotview>`
})
export class AppComponent implements OnInit {
  public dataSourceSettings: IDataOptions;
  public data: DataManager;
  public width: string;

    ngOnInit(): void {

        this.data = new DataManager({
            url: 'https://bi.syncfusion.com/northwindservice/api/orders',
            adaptor: new WebApiAdaptor,
            crossDomain: true
        });
        this.width = '100%';
        this.dataSourceSettings = {
            dataSource: this.data,
            expandAll: true,
            filters: [],
            columns: [{ name: 'ProductName', caption: 'Product Name' }],
            rows: [{ name: 'ShipCountry', caption: 'Ship Country' }, { name: 'ShipCity', caption: 'Ship City' }],
            formatSettings: [{ name: 'UnitPrice', format: 'C0' }],
            values: [{ name: 'Quantity' }, { name: 'UnitPrice', caption: 'Unit Price' }]
        };
    }
}

```

{% endtab %}

## Mapping

One can define field information like alias name (caption), data type, aggregation type, show and hide subtotals etc. using the [`fieldMapping`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#fieldmapping) property under [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/). The available options are,

* [`name`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#name) - It is to specify the appropriate field name.
* [`caption`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#caption) - It is to set the alias name (caption) to the specific field. Instead of actual field name, the alias name (caption) will be set in the UI of the pivot table.
* [`type`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#type) - It is to display values in the pivot table with appropriate aggregation such as sum, product, count, average, minimum, maximum, etc. Its default value is **sum**. This option is applicable only for relational data source.
* [`axis`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#axis) - It will help to display the field in specified axis such as row/column/value/filter axis of the pivot table.
* [`showNoDataItems`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#shownodataitems) - It is to show all the members of a specific field to the pivot table, even if there are no data in the intersection of the row and column. The default value is **false**. This option is applicable only for relational data source.
* [`baseField`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#basefield) - For the aggregate types like "DifferenceFrom" or "PercentageOfDifferenceFrom" or "PercentageOfParentTotal", selective field is assigned for comparison via this property.
* [`baseItem`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#baseitem) For the aggregate types like "DifferenceFrom" or "PercentageOfDifferenceFrom" or "PercentageOfParentTotal", selective member in a field is assigned for comparison via this property.
* [`showSubTotals`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#showsubtotals) - It is to show or hide sub-totals of a specific field in row and column axis of the pivot table. The default value is **true**.
* [`isNamedSet`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#isnamedset) - It is to set whether the specified field is named set or not. In general, the named set is a set of dimension members or a set expression (MDX query) to be created as a dimension in the SSAS OLAP cube itself. The default value is **false** and this option is applicable only for OLAP data source.
* [`isCalculatedField`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#iscalculatedfield) - It is to set whether the specified field is a calculated field or not. In general, a calculated field is created from the bound data source or using simple formula with basic arithmetic operators in the pivot table. The default value is **false** and this option is applicable only for OLAP data source.
* [`showFilterIcon`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#showfiltericon) - It is to show or hide the filter icon of a specific field which will be displayed on the button of the grouping bar and field list UI. This filter icon is used to filter the members of a specified field at runtime in the pivot table. The default value is **true**.
* [`showSortIcon`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#showsorticon) - It is to show or hide the sort icon of a specific field which will be displayed on the button of the grouping bar and field list UI. This sort icon is used to order members of a specified field either in ascending or descending at runtime. The default value is **true**.
* [`showRemoveIcon`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#showremoveicon) - It is to show or hide the remove icon of a specific field which will be displayed on the button of the grouping bar and field list UI. This remove icon is used to remove the specified field during runtime. The default value is **true**.
* [`showValueTypeIcon`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#showvaluetypeicon) - It is to show or hide the value type icon of a specific field which will be displayed on the button of the grouping bar and field list UI. This value type icon helps to select the appropriate aggregation type to specified value field at runtime. The default value is **true**.
* [`showEditIcon`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#showediticon) - It is to show or hide the edit icon of a specific field which will be displayed on the button of the grouping bar and field list UI. This edit icon is used to modify caption, formula, and format of a specified calculated field at runtime. The default value is **true**.
* [`allowDragAndDrop`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#allowdraganddrop) - It is to restrict specific field's button from being dragged on runtime in the grouping bar and field list UI. This will prevent from altering the current report. The default value is **true**.
* [`dataType`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldOptionsModel/#datatype) - It is to specify the type of the field like 'string', 'number', 'datetime', 'date', and 'boolean'.

The main purpose of these mapping options is to configure each field that is not part of the initial pivot report. Even if any field that is part of this mapping is defined here, the value set in the initial report will have the highest preceding.

> This option is applicable only for relational data source.
In the below code sample, visibility of the field button icons are configured.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component } from '@angular/core';
import { IDataOptions, PivotView, GroupingBarService, FieldListService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [GroupingBarService, FieldListService],
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' height='350' [dataSourceSettings]=dataSourceSettings showGroupingBar='true' showFieldList='true' width=width></ejs-pivotview>`
})

export class AppComponent {

    public width: string;
    public dataSourceSettings: IDataOptions;

    ngOnInit(): void {

        this.width = "100%";

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            allowLabelFilter: true,
            allowValueFilter: true,
            columns: [{ name: 'Year', caption: 'Production Year' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }],
            rows: [{ name: 'Country' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: [],
            fieldMapping: [
            { name: 'Quarter', showSortIcon: false },
            { name: 'Products', showFilterIcon: false, showRemoveIcon: false },
            { name: 'Amount', showValueTypeIcon: false, caption: 'Sold Amount' },
        ]
        };
    }
 }

```

{% endtab %}

## Values in row axis

By default, the value fields are plotted in column axis. To plot those fields in row axis, use the [`valueAxis`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#valueaxis) property by setting its value as **row**. By default, it holds the value **column**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings width=width height='350'></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;
    public height: number;
    ngOnInit(): void {
        this.width = '100%';

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: [],
            valueAxis: 'row'
        };
    }
}

```

{% endtab %}

## Show 'no data' items

By default, the pivot table only shows the field item if it has data in its row or column combination. To show all items that do not have data in row and column combination in the pivot table, use the [`showNoDataItems`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/fieldListFieldOptions/#shownodataitems) property by settings its value to **true** for the desired fields. In the following code sample, rows of the "Country" and "State" fields do not have data in all combination with "Date" column field.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { noData } from './datasource.ts';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings width=width height='350'></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;
    public height: number;
    ngOnInit(): void {
        this.width = '100%';

        this.dataSourceSettings = {
        dataSource: noData,
        expandAll: true,
        formatSettings: [{ name: 'Amount', format: 'C0' }],
        columns: [{ name: 'Date', showNoDataItems: true}],
        values: [{ name: 'Quantity', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
        rows: [{ name: 'Country', showNoDataItems: true }, { name: 'State', showNoDataItems: true }],
        filters: []
        };
    }
}

```

{% endtab %}

## Show value headers always

To show value header always in pivot table, even if it holds a single value, use the [`alwaysShowValueHeader`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#alwaysshowvalueheader) property by settings its value as **true**.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings width=width height='350'></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;
    public height: number;
    ngOnInit(): void {
        this.width = '100%';

        this.dataSourceSettings = {
            dataSource: Pivot_Data,
            expandAll: false,
            drilledMembers: [{ name: 'Country', items: ['France'] }],
            columns: [{ name: 'Year', caption: 'Production Year' }, { name: 'Quarter' }],
            values: [{ name: 'Sold', caption: 'Units Sold' }],
            rows: [{ name: 'Country' }, { name: 'Products' }],
            formatSettings: [{ name: 'Amount', format: 'C0' }],
            filters: [],
            alwaysShowValueHeader: true
        };
    }
}

```

{% endtab %}

## Customize empty value cells

User can show custom string in empty value cells using the [`emptyCellsTextContent`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/#emptycellsTextcontent) property in [`dataSourceSettings`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/dataSourceSettings/) of the pivot table. Since the property is of string data type, user can fill empty value cells with any value like "0", "-", "*", "(blank)", etc. Its common for all value fields and can be configured through code behind.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions } from '@syncfusion/ej2-angular-pivotview';
import { noData } from './datasource.ts';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings width=width height='350'></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;
    public height: number;
    ngOnInit(): void {
        this.width = '100%';

        this.dataSourceSettings = {
        dataSource: noData,
        expandAll: true,
        formatSettings: [{ name: 'Amount', format: 'C0' }],
        columns: [{ name: 'Date', showNoDataItems: true}],
        values: [{ name: 'Quantity', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
        rows: [{ name: 'Country'}, { name: 'State'}],
        filters: [],
        emptyCellsTextContent:'**'
        };
    }
}

```

{% endtab %}

## Event

### Load

The event [`load`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#load) fires before initiate rendering of pivot table. It holds following parameters like`dataSourceSettings`, `FieldsType` and `PivotView`. In this event user can customize data source settings before initiating pivot table render module.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, LoadEventArg } from '@syncfusion/ej2-angular-pivotview';
import { noData } from './datasource.ts';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings width=width height='350' (load)='load($event)'></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;
    public height: number;
    load(args: LoadEventArg) {
        args.dataSourceSettings.emptyCellsTextContent = "###";
        args.dataSourceSettings.columns[0].caption = "Full Year";
        args.dataSourceSettings.expandAll = false;
    }
    ngOnInit(): void {
        this.width = '100%';

        this.dataSourceSettings = {
        dataSource: noData,
        expandAll: true,
        formatSettings: [{ name: 'Amount', format: 'C0' }],
        columns: [{ name: 'Date', showNoDataItems: true}],
        values: [{ name: 'Quantity', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
        rows: [{ name: 'Country'}, { name: 'State'}],
        filters: []
        };
    }
}

```

{% endtab %}

### EnginePopulated

The event [`enginePopulated`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#enginepopulated) is triggered after engine is populated. It has following parameters - `dataSourceSettings`, `pivotFieldList` and `pivotValues`.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, EnginePopulatedEventArgs } from '@syncfusion/ej2-angular-pivotview';
import { noData } from './datasource.ts';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings width=width height='350' (enginePopulated)='enginePopulated($event)'></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;
    public height: number;
    enginePopulated(args: EnginePopulatedEventArgs) {
        //trigger after engine is populated
    }
    ngOnInit(): void {
        this.width = '100%';

        this.dataSourceSettings = {
        dataSource: noData,
        expandAll: true,
        formatSettings: [{ name: 'Amount', format: 'C0' }],
        columns: [{ name: 'Date', showNoDataItems: true}],
        values: [{ name: 'Quantity', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
        rows: [{ name: 'Country'}, { name: 'State'}],
        filters: []
        };
    }
}

```

{% endtab %}

### EnginePopulating

The event [`enginePopulating`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#enginepopulating) triggers  before the pivot engine starts to populate and allows to customize the pivot datasource settings. It has following parameter `dataSourceSettings`.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, EnginePopulatingEventArgs } from '@syncfusion/ej2-angular-pivotview';
import { noData } from './datasource.ts';

@Component({
  selector: 'app-container',
  template: `<ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings width=width height='350' (enginePopulating)='enginePopulating($event)'></ejs-pivotview>`
})
export class AppComponent implements OnInit {
    public dataSourceSettings: IDataOptions;
    public width: string;
    public height: number;
    enginePopulating(args: EnginePopulatingEventArgs) {
        //trigger before engine starts to populate
        args.dataSourceSettings.columns[0].caption = 'Full Year';
        args.dataSourceSettings.emptyCellsTextContent = '###'
    }
    ngOnInit(): void {
        this.width = '100%';

        this.dataSourceSettings = {
        dataSource: noData,
        expandAll: true,
        formatSettings: [{ name: 'Amount', format: 'C0' }],
        columns: [{ name: 'Date', showNoDataItems: true}],
        values: [{ name: 'Quantity', caption: 'Units Sold' }, { name: 'Amount', caption: 'Sold Amount' }],
        rows: [{ name: 'Country'}, { name: 'State'}],
        filters: []
        };
    }
}

```

{% endtab %}

## See Also

* [Aggregation](./aggregation)
* [Show/Hide Totals](./summary-customization)
* [Customize number, date, and time values](./how-to/customize-number-date-and-time-values)