---
title: "Virtual Scrolling"
component: "Pivot Table"
description: "Virtual Scrolling allows user to load large amount of data without performance degradation."
---

<!-- markdownlint-disable MD036 -->

# Virtual Scrolling

## Virtual Scrolling

The virtual scrolling option allows you to load the large amounts of data without performance degradation by rendering rows and columns only in the content viewport. The data will refresh dynamically on vertical or horizontal scroll. This feature can be enabled by setting the [`enableVirtualization`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#enablevirtualization) property to **true**.

To use the virtual scrolling feature, inject the `VirtualScroll` module in to the pivot table.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, PivotView, VirtualScrollService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [VirtualScrollService],
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings enableVirtualization='true' height='350'></ejs-pivotview>`
})

export class AppComponent implements OnInit  {
public dataSourceSettings: IDataOptions;
public date1: number;
public date2: number;
data(count: number) {
  let result: Object[] = [];
  let dt: number = 0;
  for (let i: number = 1; i < count + 1; i++) {
    dt++;
    let round: string;
    let toString: string = i.toString();
    if (toString.length === 1) {
      round = "0000" + i;
    } else if (toString.length === 2) {
      round = "000" + i;
    } else if (toString.length === 3) {
      round = "00" + i;
    } else if (toString.length === 4) {
      round = "0" + i;
    } else {
      round = toString;
    }
    result.push({
      ProductID: "PRO-" + round,
      Year: "FY " + (dt + 2013),
      Price: Math.round(Math.random() * 5000) + 5000,
      Sold: Math.round(Math.random() * 80) + 10
    });
    if (dt / 4 == 1) {
        dt = 0;
    }
  }
  return result;
}
    ngOnInit(): void {
        this.dataSourceSettings = {
        dataSource: this.data(1000) as IDataSet[],
        enableSorting: false,
        expandAll: true,
        formatSettings: [{ name: 'Price', format: 'C0' }],
        rows: [{ name: 'ProductID' }],
        columns: [{ name: 'Year' }],
        values: [{ name: 'Price', caption: 'Unit Price' }, { name: 'Sold', caption: 'Unit Sold' }]
        };
    }
}

```

{% endtab %}

**Limitations for virtual scrolling**

* In virtual scrolling, the `columnWidth` property in `gridSettings` should be in pixel and percentage values are not accepted.
* Resizing columns, setting width to individual columns which affects the calculation used to pick the correct page on scrolling.
* Grouping, which takes additional time to splitting the raw items into the provided format.
* Date Formatting, which takes additional time to convert date format.
* Date Formatting with sorting, here additionally full date time format should be framed to perform sorting along with the provided date format which lags the performance.

## Data Compression

> This property is applicable only for the relational data source.

When we bind one million raw data, the pivot table will process all raw data to generate aggregated data during initial rendering and report manipulation. But in data compression, the data will be compressed based on the uniqueness of the raw data, and unique records will be provided as input for the Pivot Table. The compressed data will be used for further operations at all times, reducing the looping complexity and improving the performance of the pivot table. For example, if the pivot table  is connected to one million raw data aggregated to 1,000 unique data means, it will be rendered within 3 seconds rather than 10 seconds. You can enable this option by using the [`allowDataCompression`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#allowdatacompression) property along with [`enableVirtualization`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#enablevirtualization) property.

> This options will only function when the virtual scrolling is enabled.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { IDataOptions, PivotView, VirtualScrollService } from '@syncfusion/ej2-angular-pivotview';
import { Pivot_Data } from './datasource.ts';

@Component({
  selector: 'app-container',
  providers: [VirtualScrollService],
  // specifies the template string for the pivot table component
  template: `<ejs-pivotview #pivotview id='PivotView' [dataSourceSettings]=dataSourceSettings allowDataCompression='true' enableVirtualization='true' height='350'></ejs-pivotview>`
})

export class AppComponent implements OnInit  {
public dataSourceSettings: IDataOptions;
public date1: number;
public date2: number;
data(count: number) {
  let result: Object[] = [];
  let dt: number = 0;
  for (let i: number = 1; i < count + 1; i++) {
    dt++;
    let round: string;
    let toString: string = i.toString();
    if (toString.length === 1) {
      round = "0000" + i;
    } else if (toString.length === 2) {
      round = "000" + i;
    } else if (toString.length === 3) {
      round = "00" + i;
    } else if (toString.length === 4) {
      round = "0" + i;
    } else {
      round = toString;
    }
    result.push({
      ProductID: 'PRO-' + (i % 1000),
      Year: "FY " + (dt + 2013),
      Price: Math.round(Math.random() * 5000) + 5000,
      Sold: Math.round(Math.random() * 80) + 10
    });
    if (dt / 4 == 1) {
        dt = 0;
    }
  }
  return result;
}
    ngOnInit(): void {
        this.dataSourceSettings = {
        dataSource: this.data(1000000) as IDataSet[],
        enableSorting: false,
        expandAll: true,
        formatSettings: [{ name: 'Price', format: 'C0' }],
        rows: [{ name: 'ProductID' }],
        columns: [{ name: 'Year' }],
        values: [{ name: 'Price', caption: 'Unit Price' }, { name: 'Sold', caption: 'Unit Sold' }]
        };
    }
}

```

{% endtab %}

**Limitations during data compression**

* The following aggregation types will not be supported.
    * Average
    * Populationstdev
    * Samplestdev
    * Populationvar
    * Samplevar
* If you use any of the aggregations above, it will result in an aggregation type **"Sum"**.
* Distinctcount will act as **"Count"** aggregation type.
* In the calculated field, an existing field can be inserted without altering its default aggregation type Even if we change it, it would use the default aggregation type back for calculation.

## Virtual scrolling for static field list

Virtual scrolling automatically works with "Popup" field list on setting the [`enableVirtualization`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#enablevirtualization) property in the Pivot Table to **true**. Incase of static field list, which act as a separate component, user need to enable [`enableVirtualization`](https://ej2.syncfusion.com/angular/documentation/api/pivotview/#enablevirtualization) property in the Pivot Table and also pass the report information to pivot table instance via the [`load`](https://ej2.syncfusion.com/angular/documentation/api/pivotview#load) event of the field list.

{% tab template="pivot-grid/getting-started", sourceFiles="app/app.component.ts,app/app.module.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { PivotFieldListComponent, PivotViewComponent, FieldListService, IDataOptions, IDataSet,
    EnginePopulatedEventArgs, VirtualScrollService } from '@syncfusion/ej2-angular-pivotview';
import { Browser, setStyleAttribute, prepend } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-container',
  providers: [FieldListService, VirtualScrollService],
  styleUrls: ['app/app.component.css'],
  template: `<ejs-pivotfieldlist #pivotfieldlist id='PivotFieldList' [dataSourceSettings]=dataSourceSettings renderMode="Fixed" (enginePopulated)='afterPopulate($event)' allowCalculatedField='true' (load)='onLoad()' (dataBound)='ondataBound()'></ejs-pivotfieldlist>
  <ejs-pivotview #pivotview id='PivotViewFieldList' width='99%' height='530' enableVirtualization='true '(enginePopulated)='afterEnginePopulate($event)'></ejs-pivotview>`
})

export class AppComponent {
    public dataSourceSettings: IDataOptions;
    data(count: number) {
      let result: Object[] = [];
      let dt: number = 0;
      for (let i: number = 1; i < count + 1; i++) {
        dt++;
        let round: string;
        let toString: string = i.toString();
        if (toString.length === 1) {
          round = "0000" + i;
        } else if (toString.length === 2) {
          round = "000" + i;
        } else if (toString.length === 3) {
          round = "00" + i;
        } else if (toString.length === 4) {
          round = "0" + i;
        } else {
          round = toString;
        }
        result.push({
          ProductID: "PRO-" + round,
          Year: "FY " + (dt + 2013),
          Price: Math.round(Math.random() * 5000) + 5000,
          Sold: Math.round(Math.random() * 80) + 10
        });
        if (dt / 4 == 1) {
          dt = 0;
        }
      }
      return result;
    }

    @ViewChild('pivotview', {static: false})
    public pivotObj: PivotViewComponent;

    @ViewChild('pivotfieldlist')
    public fieldListObj: PivotFieldListComponent;

    afterPopulate(arge: EnginePopulatedEventArgs): void {
      if (this.fieldListObj && this.pivotObj) {
          this.fieldListObj.updateView(this.pivotObj);
      }
    }
    afterEnginePopulate(args: EnginePopulatedEventArgs): void {
      if (this.fieldListObj && this.pivotObj) {
          this.fieldListObj.update(this.pivotObj);
      }
    }
    onLoad(): void {
      if (Browser.isDevice) {
          this.fieldListObj.renderMode = 'Popup';
          this.fieldListObj.target = '.control-section';
          document.getElementById('PivotFieldList').removeAttribute('style');
          setStyleAttribute(document.getElementById('PivotFieldList'), {
              'height': 0,
              'float': 'left'
          });
      }
      this.pivotGridMdule = this.pivotObj;
      //Assigning report to pivot table component
      this.pivotObj.dataSourceSettings = this.fieldListObj.dataSourceSettings;
      //Generating page settings based on pivot table component’s size.
      this.pivotObj.updatePageSettings(true);
      //Assigning page settings to field list component.
      fieldListObj.pageSettings = pivotObj.pageSettings;
    }

    ondataBound(): void {
      if (Browser.isDevice) {
          prepend([document.getElementById('PivotFieldList')], document.getElementById('PivotView'));
      }
    }

    ngOnInit(): void {
      this.dataSourceSettings = {
          dataSource: this.data(1000) as IDataSet[],
          enableSorting: false,
          expandAll: true,
          formatSettings: [{ name: 'Price', format: 'C0' }],
          rows: [{ name: 'ProductID' }],
          columns: [{ name: 'Year' }],
          values: [{ name: 'Price', caption: 'Unit Price' }, { name: 'Sold', caption: 'Unit Sold' }]
      };
    }
 }

```

{% endtab %}