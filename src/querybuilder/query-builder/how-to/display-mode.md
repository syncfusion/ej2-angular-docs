---
title: "Change display mode"
component: "Query Builder"
description: "Learn how to change display mode in the Essential JS 2 QueryBuilder control."
---

# Change display mode

Display options allow you to view the Query Builder in Vertically or Horizontally. For this, you should use the [`displayMode`](https://ej2.syncfusion.com/vue/documentation/api/query-builder/#displaymode) property.

{% tab template="query-builder/filtering", isDefaultActive=true, sourceFiles="app/**/*.ts", iframeHeight="600px" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { RuleModel } from '@syncfusion/ej2-angular-querybuilder';
import { employeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="40%" [dataSource]="data" [rule]="importRules" displayMode="Vertical">
                <e-columns>
                  <e-column field="EmployeeID" label="Employee ID" type="number" ></e-column>
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
    ngOnInit(): void {
        this.data = employeeData;
        this.importRules =  {
        'condition': 'and',
        'rules': [{
            'label': 'EmployeeID',
            'field': 'EmployeeID',
            'type': 'number',
            'operator': 'equal',
            'value': 1001
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

> The default view the query builder component is Horizontal.
> The default view the query builder component in Vertical.
