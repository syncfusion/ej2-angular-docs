---
title: "Filtering"
component: "QueryBuilder"
description: "Learn how to filtering in the Essential JS 2 QueryBuilder control."
---

# Filtering

Query Builder allows you to create or delete conditions and groups. You can use [`showButtons`](https://ej2.syncfusion.com/vue/documentation/api/query-builder/#showbuttons) to enable/disable these buttons.

You can create or delete conditions by interacting through the user interface and methods.

* Use the [`addRules`](https://ej2.syncfusion.com/vue/documentation/api/query-builder/#addrules), and [`deleteRules`](https://ej2.syncfusion.com/vue/documentation/api/query-builder/#deleterules) methods to create/delete conditions.
* Use [`addGroups`](https://ej2.syncfusion.com/vue/documentation/api/query-builder/#addgroups), and [`deleteGroups`](https://ej2.syncfusion.com/vue/documentation/api/query-builder/#deletegroups) methods to create/delete groups.

{% tab template="query-builder/filtering", isDefaultActive=true, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { RuleModel, QueryBuilderComponent } from '@syncfusion/ej2-angular-querybuilder';
import { employeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="70%" [dataSource]="data" [rule]="importRules" [showButtons]="showButtons">
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
              <button class="e-btn e-primary e-qb-button" (click)="addRule()" >Add Rule</button>
              <button class="e-btn e-primary e-qbr-button" (click)="addGroup()" >Add Group</button>
              <button class="e-btn e-primary e-qbr-button" (click)="deleteGroup()" >Delete Group</button>`
})

export class AppComponent implements OnInit {

    public data: Object[];
    public importRules: RuleModel;
     @ViewChild('querybuilder')
    public qryBldrObj: QueryBuilderComponent;
    public showButtons: Object = {ruleDelete: true, groupInsert: true, groupDelete: true};
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
    addRule(): void {
        this.qryBldrObj.addRules([{'label': 'City','field': 'City','type': 'string','operator': 'equal','value': 'US'}], 'group0');
    }

    addGroup(): void {
        this.qryBldrObj.addGroups([{'condition': 'and','rules': [{'label': 'First Name','field': 'FirstName','type': 'string','operator': 'startswith','value': 'v' }]}], 'group0');
    }

    deleteGroup(): void {
        this.qryBldrObj.deleteGroups(['group1']);
    }

}

```

{% endtab %}
