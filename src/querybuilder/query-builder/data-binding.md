---
title: "Data Binding"
component: "QueryBuilder"
description: "Learn how to bind local data in the Essential JS 2 QueryBuilder control."
---

# Data Binding

The Query Builder uses `DataManager`, which supports both RESTful JSON data services binding and local JavaScript object array binding. The [`dataSource`](https://ej2.syncfusion.com/vue/documentation/api/query-builder/#datasource) property can be assigned either with the instance of `DataManager` or JavaScript object array collection. It supports two kinds of binding:

* Local data
* Remote data

## Local data

To bind local data to the query builder, you can assign the [`dataSource`](https://ej2.syncfusion.com/vue/documentation/api/query-builder/#datasource) property  with a JavaScript object array. The local data source can also be provided as an instance of the `DataManager`.

{% tab template="query-builder/filtering", isDefaultActive=true, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { RuleModel } from '@syncfusion/ej2-angular-querybuilder';
import { employeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="70%" [dataSource]="data" [rule]="importRules">
                <e-columns>
                  <e-column field="EmployeeID" label="Employee ID" type="number"></e-column>
                  <e-column field="FirstName" label="First Name" type="string"></e-column>
                  <e-column field="TitleOfCourtesy" label="Title Of Courtesy" type="boolean" [values]="values"></e-column>
                  <e-column field="Title" label="Title" type="string"></e-column>
                  <e-column field="HireDate" label="Hire Date" type="date" format="dd/MM/yyyy"></e-column>
                  <e-column field="Country" label="Country" type="string"></e-column>
                  <e-column field="City" label="City" type="string"></e-column>
                </e-columns>
              </ejs-querybuilder>`
})

export class AppComponent implements OnInit {

    public data: Object[];
    public importRules: RuleModel;
    public values: string[] = ['Mr.', 'Mrs.'];
    ngOnInit(): void {
        this.data = employeeData;
        this.importRules = {
        'condition': 'and',
        'rules': [{
                'label': 'Employee ID',
                'field': 'EmployeeID',
                'type': 'number',
                'operator': 'equal',
                'value': 1
            },
            {
                'label': 'Title',
                'field': 'Title',
                'type': 'string',
                'operator': 'equal',
                'value': 'Sales Manager'
            }]
        };
    }
}

```

{% endtab %}

> By default, `DataManager` uses `JsonAdaptor` for local data-binding.

## Remote data

To bind remote  data to the query builder, assign service data as an instance of  `DataManager` to the [`dataSource`](https://ej2.syncfusion.com/documentation/api/query-builder/#datasource) property. To interact with remote data source, provide the endpoint `url`.

{% tab template="query-builder/default",sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component } from '@angular/core';
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="70%" [dataSource]="data" [rule]="importRules">
                <e-columns>
                  <e-column field="EmployeeID" label="Employee ID" type="number"></e-column>
                  <e-column field="FirstName" label="First Name" type="string"></e-column>
                  <e-column field="TitleOfCourtesy" label="Title Of Courtesy" type="boolean" [values]="values"></e-column>
                  <e-column field="Title" label="Title" type="string"></e-column>
                  <e-column field="HireDate" label="Hire Date" type="date" format="dd/MM/yyyy"></e-column>
                  <e-column field="Country" label="Country" type="string"></e-column>
                  <e-column field="City" label="City" type="string"></e-column>
                </e-columns>
              </ejs-querybuilder>`
})

export class AppComponent implements OnInit {

    public data: DataManager;
    ngOnInit(): void {
        this.data = new DataManager({
        url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders/',
        adaptor: new ODataAdaptor,
        });
        this.importRules = {
          'condition': 'and',
          'rules': [{
                'label': 'Employee ID',
                'field': 'EmployeeID',
                'type': 'number',
                'operator': 'equal',
                'value': 1
            },
            {
                'label': 'Title',
                'field': 'Title',
                'type': 'string',
                'operator': 'equal',
                'value': 'Sales Manager'
            }]
        };
    }
}
```

{% endtab %}

> By default, `DataManager` uses `ODataAdaptor` for remote data-binding.

### Binding with OData services

[`OData`](https://www.odata.org/documentation/odata-version-3-0/) is a standardized protocol for creating and consuming data. You can retrieve data from OData service using the DataManager. Refer to the following code example for remote Data binding using OData service.

{% tab template="query-builder/default",sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component } from '@angular/core';
import { DataManager, ODataAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="70%" [dataSource]="data" [rule]="importRules">
                <e-columns>
                  <e-column field="EmployeeID" label="Employee ID" type="number"></e-column>
                  <e-column field="FirstName" label="First Name" type="string"></e-column>
                  <e-column field="TitleOfCourtesy" label="Title Of Courtesy" type="boolean" [values]="values"></e-column>
                  <e-column field="Title" label="Title" type="string"></e-column>
                  <e-column field="HireDate" label="Hire Date" type="date" format="dd/MM/yyyy"></e-column>
                  <e-column field="Country" label="Country" type="string"></e-column>
                  <e-column field="City" label="City" type="string"></e-column>
                </e-columns>
              </ejs-querybuilder>`
})

export class AppComponent implements OnInit {

    public data: DataManager;
    public values: string[] = ['Mr.', 'Mrs.'];
    ngOnInit(): void {
        this.data = new DataManager({
        url: 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders/',
        adaptor: new ODataAdaptor,
        crossDomain: true
        });
        this.importRules = {
          'condition': 'and',
          'rules': [{
                'label': 'Employee ID',
                'field': 'EmployeeID',
                'type': 'number',
                'operator': 'equal',
                'value': 1
            },
            {
                'label': 'Title',
                'field': 'Title',
                'type': 'string',
                'operator': 'equal',
                'value': 'Sales Manager'
            }]
        };
    }
}
```

{% endtab %}

### Binding with OData v4 services

The ODataV4 is an improved version of OData protocols, and the `DataManager` can also retrieve and consume OData v4 services. For more details on OData v4 services, refer to the [`odata documentation`](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752197). To bind OData v4 service, use the `ODataV4Adaptor`.

{% tab template="query-builder/default",sourceFiles="app/app.component.ts,app/app.module.ts,app/main.ts" %}

```typescript
import { Component } from '@angular/core';
import { DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="70%" [dataSource]="data" [rule]="importRules">
                <e-columns>
                  <e-column field="EmployeeID" label="Employee ID" type="number"></e-column>
                  <e-column field="FirstName" label="First Name" type="string"></e-column>
                  <e-column field="TitleOfCourtesy" label="Title Of Courtesy" type="boolean" [values]="values"></e-column>
                  <e-column field="Title" label="Title" type="string"></e-column>
                  <e-column field="HireDate" label="Hire Date" type="date" format="dd/MM/yyyy"></e-column>
                  <e-column field="Country" label="Country" type="string"></e-column>
                  <e-column field="City" label="City" type="string"></e-column>
                </e-columns>
              </ejs-querybuilder>`
})

export class AppComponent implements OnInit {

    public data: DataManager;
    public values: string[] = ['Mr.', 'Mrs.'];
    ngOnInit(): void {
        this.data = new DataManager({
        url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Orders/',
        adaptor: new ODataV4Adaptor
        });
        this.importRules = {
          'condition': 'and',
          'rules': [{
                'label': 'Employee ID',
                'field': 'EmployeeID',
                'type': 'number',
                'operator': 'equal',
                'value': 1
            },
            {
                'label': 'Title',
                'field': 'Title',
                'type': 'string',
                'operator': 'equal',
                'value': 'Sales Manager'
            }]
        };
    }
}
```

{% endtab %}

### Web API

You can use `WebApiAdaptor` to bind query builder with Web API created using OData endpoint.

```typescript
import { Component } from '@angular/core';
import { DataManager, WebApiAdaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="70%" [dataSource]="data" [rule]="importRules">
                <e-columns>
                  <e-column field="EmployeeID" label="Employee ID" type="number"></e-column>
                  <e-column field="FirstName" label="First Name" type="string"></e-column>
                  <e-column field="TitleOfCourtesy" label="Title Of Courtesy" type="boolean" [values]="values"></e-column>
                  <e-column field="Title" label="Title" type="string"></e-column>
                  <e-column field="HireDate" label="Hire Date" type="date" format="dd/MM/yyyy"></e-column>
                  <e-column field="Country" label="Country" type="string"></e-column>
                  <e-column field="City" label="City" type="string"></e-column>
                </e-columns>
              </ejs-querybuilder>`
})
export class AppComponent implements OnInit {

    public data: DataManager;

    ngOnInit(): void {
        this.data = new DataManager({
            url: 'api/OrderAPI',
            adaptor: new WebApiAdaptor
        });
        this.importRules = {
          'condition': 'and',
          'rules': [{
                'label': 'Employee ID',
                'field': 'EmployeeID',
                'type': 'number',
                'operator': 'equal',
                'value': 1
            },
            {
                'label': 'Title',
                'field': 'Title',
                'type': 'string',
                'operator': 'equal',
                'value': 'Sales Manager'
            }]
        };
    }
}

```

## Data Manager

You can use the created conditions in DataManager through the getPredicate method. This method creates predicates which is used as conditions in DataManager.

{% tab template="query-builder/filtering", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { RuleModel, QueryBuilderComponent } from '@syncfusion/ej2-angular-querybuilder';
import { employeeData  } from './datasource';
import { DataManager, Query } from '@syncfusion/ej2-data';
@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="70%" [dataSource]="data" [rule]="importRules">
                <e-columns>
                  <e-column field="EmployeeID" label="Employee ID" type="number"></e-column>
                  <e-column field="FirstName" label="First Name" type="string"></e-column>
                  <e-column field="TitleOfCourtesy" label="Title Of Courtesy" type="boolean" [values]="values"></e-column>
                  <e-column field="Title" label="Title" type="string"></e-column>
                  <e-column field="HireDate" label="Hire Date" type="date" format="dd/MM/yyyy"></e-column>
                  <e-column field="Country" label="Country" type="string"></e-column>
                  <e-column field="City" label="City" type="string"></e-column>
                </e-columns>
              </ejs-querybuilder>
              <button class="e-btn e-primary e-qb-button" (click)="refreshTable()" >Get Data</button>
              <table id='datatable'class='e-table'>
                <tr><th>EmployeeID</th><th>Title</th><th>City</th></tr>
                <tr *ngFor="let item of items">
                <td>{{item.EmployeeID}}</td><td>{{item.Title}}</td><td>{{item.City}}</td>
                </tr>
                </table>`
})

export class AppComponent implements OnInit {

    public data: Object[];
    public importRules: RuleModel;
     @ViewChild('querybuilder')
    public qryBldrObj: QueryBuilderComponent;
    public values: string[] = ['Mr.', 'Mrs.'];
    public items: Object[];
    public  dataManagerQuery:Query;
    ngOnInit(): void {
        this.data = employeeData ;
        this.importRules = {
        'condition': 'and',
        'rules': [{
                'label': 'Employee ID',
                'field': 'EmployeeID',
                'type': 'number',
                'operator': 'equal',
                'value': 1
            }]
        };
    }
      refreshTable(): void {
        this.dataManagerQuery = new Query().select(['EmployeeID', 'Title', 'City']).where(this.qryBldrObj.getPredicate(this.qryBldrObj.rule)).take(8);
        this.items = [];
        this.items = new DataManager(<JSON[]>this.data).executeLocal(this.dataManagerQuery);
    }

}

```

{% endtab %}

## Complex Data Binding

Complex Data Binding allows you to create subfield for columns. To implement complex data binding, either bind the complex data in nested columns or specify complex data source and separator must be given in querybuilder.

In the following sample, complex data was bound in nested columns.

{% tab template="query-builder/complex-data-binding", sourceFiles="app/app.component.ts,app/template-driven.html,app/app.module.ts,app/main.ts,app/datasource.ts", isDefaultActive=true %}

```typescript

import { Component, ViewChild, OnInit } from '@angular/core';
import { QueryBuilderComponent } from '@syncfusion/ej2-angular-querybuilder';
import {  RuleModel, RuleChangeEventArgs, ColumnsModel } from '@syncfusion/ej2-querybuilder';
import { RadioButton, ChangeEventArgs } from '@syncfusion/ej2-buttons';
import { getComponent} from '@syncfusion/ej2-base';
import { MultiSelect, CheckBoxSelection } from '@syncfusion/ej2-dropdowns';
import { RadioButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
  selector: 'app-root',
  templateUrl: `app/template-driven.html`
})
export class AppComponent implements OnInit {
  @ViewChild('querybuilder') qryBldrObj: QueryBuilderComponent;
  public importRules: RuleModel;
  public columns1: ColumnsModel[];
  public columns2: ColumnsModel[];
  public columns3: ColumnsModel[];
  ngOnInit(): void {
    this.importRules = {
      condition: 'and',
      rules: [{
        label: 'ID',
        field: 'Employee.ID',
        type: 'string',
        operator: 'equal',
        value: 0
      },
      {
        label: 'Last Name',
        field: 'Name.LastName',
        type: 'string',
        operator: 'contains',
        value: 'malan'
      },
      {
        condition: 'or',
        rules: [{
            label: 'City',
            field: 'Country.State.City',
            operator: 'startswith',
            type: 'string',
            value: 'U'
        },
        {
            label: 'Region',
            field: 'Country.Region',
            operator: 'endswith',
            type: 'string',
            value: 'c'
        },
        {
            label: 'Name',
            field: 'Country.Name',
            operator: 'isnotempty'
        }]
      }]
    };
    this.columns1 = [
      { field: 'ID', label: 'ID', type: 'number'},
      { field: 'DOB', label: 'Date of birth', type: 'date'},
      { field: 'HireDate', label: 'Hire Date', type: 'date'},
      { field: 'Salary', label: 'Salary', type: 'number'},
      { field: 'Age', label: 'Age', type: 'number'},
      { field: 'Title', label: 'Title', type: 'string'}
    ]
    this.columns2 = [
      { field: 'FirstName', label: 'First Name', type: 'string'},
      { field: 'LastName', label: 'Last Name', type: 'string'}
    ]
    this.columns3 = [
      { field: 'State', label: 'State', columns : [
        { field: 'City', label: 'City', type: 'string'},
        { field: 'Zipcode', label: 'Zip Code', type: 'number'}] },
    { field: 'Region', label: 'Region', type: 'string'},
    { field: 'Name', label: 'Name', type: 'string'}
    ]
  }
  
  onReset(e: Event): void {
    this.qryBldrObj.reset();
  }
  onSetSqlRules(e:Event): void {
    this.qryBldrObj.setRulesFromSql("Employee.ID = 0 AND Name.LastName LIKE ('%malan%') AND (Country.State.City LIKE ('U%') AND Country.Region LIKE ('%c') AND Country.Name IS NOT EMPTY)");
  }
  onSetRules(e:Event): void {
    this.qryBldrObj.setRules(this.importRules);
  }
  
}


```

{% endtab %}