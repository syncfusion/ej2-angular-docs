---
title: "Columns"
component: "QueryBuilder"
description: "Documentation on column step, format, labels, operators, validations, template in the Essential JS 2 QueryBuilder control."
---

# Columns

The column definitions are used as the [`dataSource`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/#datasource) schema in the Query Builder. This plays a vital role in rendering column values. The query builder operations such as create or delete conditions and create or delete group they are performed based on the column definitions. The [`field`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/columnsModel/#field) property of the columns is necessary to map the data source values in the query builder columns.

> If the column field is not specified in the [dataSource](https://ej2.syncfusion.com/angular/documentation/api/query-builder/#datasource), the column values will be empty.

## Auto generation

The [`columns`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/#columns) are automatically generated when the [`columns`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/#columns) declaration is empty or undefined while initializing the query builder. All the columns in the [dataSource](https://ej2.syncfusion.com/angular/documentation/api/query-builder/#datasource) are bound as the query builder columns.

{% tab template="query-builder/filtering", isDefaultActive=true,sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { employeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="70%" [dataSource]="data">
               </ejs-querybuilder>`
})

export class AppComponent implements OnInit {

    public data: Object[];
    ngOnInit(): void {
        this.data = employeeData;
    }
}

```

{% endtab %}

> When columns are auto-generated, the column type will be determined from the first record of the [`dataSource`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/#datasource).

## Labels

By default, the column label is displayed from the column [`field`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/columnsModel/#field) value. To override the default label, you have to define the [`label`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/columnsModel/#label) value.

## Operators

The operator for a column can be defined in the [`operators`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/columnsModel/#operators) property.
The available operators and its supported data types are:

| Operators | Description | Supported Types |
| ------------ | ----------------------- | ------------------ |
| startswith  | Checks whether the value begins with the specified value. | String |
| endswith  | Checks whether the value ends with the specified value. | String |
| contains | Checks whether the value contains the specified value. | String |
| equal | Checks whether the value is equal to the specified value. | String Number Date Boolean |
| notequal | Checks whether the value is not equal to the specified value. | String Number Date Boolean |
| greaterthan | Checks whether the value is greater than the specified value. | Date Number |
| greaterthanorequal | Checks whether a value is greater than or equal to the specified value. | Date Number |
| lessthan | Checks whether the value is less than the specified value.| Date Number |
| lessthanorequal | Checks whether the value is less than or equal to the specified value. | Date Number |
| between | Checks whether the value is between the two-specific value. | Date  Number |
| notbetween | Checks whether the value is not between the two-specific value. | Date  Number |
| in | Checks whether the value is one of the specific values. | String  Number |
| notin | Checks whether the value is not in the specific values. | String  Number |

## Step

The Query Builder allows you to set the step values to the number fields. So that you can easily access the numeric textbox. Use the [`step`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/columnsModel/#step) property, to set the step value for number values.

## Format

The Query Builder formats date and number values. Use the [`format`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/columnsModel/#format) property to format date and number values.

{% tab template="query-builder/filtering",sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit } from '@angular/core';
import { RuleModel } from '@syncfusion/ej2-angular-querybuilder';
import { employeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="70%" [dataSource]="data" [rule]="importRules">
                <e-columns>
                  <e-column field="EmployeeID" label="Employee ID" type="number" step="10" [operators]="employeeOperators"></e-column>
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
    public employeeOperators: Object[];
    ngOnInit(): void {
        this.data = employeeData;
        this.importRules = {
        'condition': 'and',
        'rules': [{
            'label': 'Employee ID',
            'field': 'EmployeeID',
            'type': 'number',
            'operator': 'equal',
            'value': 1001
        },
        {
            'label': 'Hire Date',
            'field': 'HireDate',
            'type': 'date',
            'operator': 'equal',
            'value': '07/05/1991'
        }]
    };
    this.employeeOperators =  [
        { value: 'equal', key: 'Equal' },
        { value: 'notequal', key: 'Not Equal' },
        { value: 'in', key: 'In' },
        { value: 'notin', key: 'Not In' }
    ];
    }
}

```

{% endtab %}

## Validations

Validation allows you to validate the conditions and it display errors for invalid fields while using  the `validateFields` method.  To enable validation in the query builder , set the allowValidation to true. Column fields are validated after setting [`allowValidation`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/#allowvalidation) as to true. So, you should manually configure the validation for Operator and, Value fields through [`validation`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/columnsModel/#validation).

{% tab template="query-builder/filtering",sourceFiles="app/**/*.ts" isDefaultActive=true %}

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { RuleModel, QueryBuilderComponent } from '@syncfusion/ej2-angular-querybuilder';
import { employeeData } from './datasource';

@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="70%" [dataSource]="data" allowValidation="true">
                <e-columns>
                  <e-column field="EmployeeID" label="Employee ID" type="number" validation="validateRule"></e-column>
                  <e-column field="FirstName" label="First Name" type="string"></e-column>
                  <e-column field="TitleOfCourtesy" label="Title Of Courtesy" type="boolean" [values]="values"></e-column>
                  <e-column field="Title" label="Title" type="string"></e-column>
                  <e-column field="HireDate" label="Hire Date" type="date" format="dd/MM/yyyy"></e-column>
                  <e-column field="Country" label="Country" type="string"></e-column>
                  <e-column field="City" label="City" type="string"></e-column>
                </e-columns>
              </ejs-querybuilder>
              <button class="e-btn e-primary e-qb-button" (click)="validate()" >Validate Field</button>`
})

export class AppComponent implements OnInit {
    public data: Object[];
    public importRules: RuleModel;
     @ViewChild('querybuilder')
    public qryBldrObj: QueryBuilderComponent;
    public validateRule: { [key: string]: Boolean } = { isRequired: true };
    public values: string[] = ['Mr.', 'Mrs.'];
    ngOnInit(): void {
        this.data = employeeData;
    }
    validate(): void {
        this.qryBldrObj.validateFields();
    }

}

```

{% endtab %}

> Set [`isRequired`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/validation/#isrequired) validation for `Operator` and `Value` fields.
> Set [`max`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/validation/#max), [`min`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/validation/#min) values for number values.