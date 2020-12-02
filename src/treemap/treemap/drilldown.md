# Drill-down

The tree map control supports drill-down to expose the hierarchy achieved by clicking a node. If you click an item in tree map, the tree map will be moved to the next level or sub level and returned back to the previous level by clicking the node header. A single level of the tree map is visible at a time.

## Perform drill-down action

The tree map elements can be drilled down by setting the enableDrillDown property to true. You can view the hierarchy of the tree map by clicking the tree map items and move to the previous level by clicking the drill-down header.

The drill-down concepts are shown in the following code example.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;' [dataSource]='data' weightValuePath='EmployeesCount' enableDrillDown= true
    [levels]='levels' [palette]='palette'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
        { Category: 'Employees', Country: 'USA', JobDescription: 'Sales', JobGroup: 'Executive', EmployeesCount: 20 },
    { Category: 'Employees', Country: 'USA', JobDescription: 'Sales', JobGroup: 'Analyst', EmployeesCount: 30 },
    { Category: 'Employees', Country: 'USA', JobDescription: 'Marketing', EmployeesCount: 40 },
    { Category: 'Employees', Country: 'USA', JobDescription: 'Management', EmployeesCount: 80 },
    { Category: 'Employees', Country: 'India', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 100 },
    { Category: 'Employees', Country: 'India', JobDescription: 'HR Executives', EmployeesCount: 30 },
    { Category: 'Employees', Country: 'India', JobDescription: 'Accounts', EmployeesCount: 40 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Sales', JobGroup: 'Executive', EmployeesCount: 50 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Sales', JobGroup: 'Analyst', EmployeesCount: 60 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Marketing', EmployeesCount: 70 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 80 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Management', EmployeesCount: 10 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Accounts', EmployeesCount: 20 },
    { Category: 'Employees', Country: 'UK', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 30 },
    { Category: 'Employees', Country: 'UK', JobDescription: 'HR Executives', EmployeesCount: 50 },
    { Category: 'Employees', Country: 'UK', JobDescription: 'Accounts', EmployeesCount: 60 },
    { Category: 'Employees', Country: 'France', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 70 },
    { Category: 'Employees', Country: 'France', JobDescription: 'Marketing', EmployeesCount: 100 }
    ];
    public palette: object= ["#f44336", "#29b6f6", "#ab47bc", "#ffc107", "#5c6bc0", "#009688"],
    public levels: object = [
        { groupPath: 'Country', border: { color: 'black', width: 0.5 } },
        { groupPath: 'JobDescription', border: { color: 'black', width: 0.5 } },
        { groupPath: 'JobGroup', border: { color: 'black', width: 0.5 } },
    ]
}

```

{% endtab %}

## On-demand data loading

In normal drill-down process, all the child items are rendered in DOM, and they are visible at initial time of TreeMap rendering. But, on-demand data loading, it will not render child items at initial time. The child nodes will be rendered at the drill-down process only. By setting the `drillDownView` property to true, you can enable this feature.

In the following sample, on-demand data loading is shown.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;' [dataSource]='data' weightValuePath='EmployeesCount' enableDrillDown= true drillDownView= true
    [levels]='levels' [palette]='palette'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
        { Category: 'Employees', Country: 'USA', JobDescription: 'Sales', JobGroup: 'Executive', EmployeesCount: 20 },
    { Category: 'Employees', Country: 'USA', JobDescription: 'Sales', JobGroup: 'Analyst', EmployeesCount: 30 },
    { Category: 'Employees', Country: 'USA', JobDescription: 'Marketing', EmployeesCount: 40 },
    { Category: 'Employees', Country: 'USA', JobDescription: 'Management', EmployeesCount: 80 },
    { Category: 'Employees', Country: 'India', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 100 },
    { Category: 'Employees', Country: 'India', JobDescription: 'HR Executives', EmployeesCount: 30 },
    { Category: 'Employees', Country: 'India', JobDescription: 'Accounts', EmployeesCount: 40 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Sales', JobGroup: 'Executive', EmployeesCount: 50 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Sales', JobGroup: 'Analyst', EmployeesCount: 60 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Marketing', EmployeesCount: 70 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 80 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Management', EmployeesCount: 10 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Accounts', EmployeesCount: 20 },
    { Category: 'Employees', Country: 'UK', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 30 },
    { Category: 'Employees', Country: 'UK', JobDescription: 'HR Executives', EmployeesCount: 50 },
    { Category: 'Employees', Country: 'UK', JobDescription: 'Accounts', EmployeesCount: 60 },
    { Category: 'Employees', Country: 'France', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 70 },
    { Category: 'Employees', Country: 'France', JobDescription: 'Marketing', EmployeesCount: 100 }
    ];
    public palette: object= ["#f44336", "#29b6f6", "#ab47bc", "#ffc107", "#5c6bc0", "#009688"],
    public levels: object = [
        { groupPath: 'Country', border: { color: 'black', width: 0.5 } },
        { groupPath: 'JobDescription', border: { color: 'black', width: 0.5 } },
        { groupPath: 'JobGroup', border: { color: 'black', width: 0.5 } },
    ]
}

```

{% endtab %}

## Breadcrumb support

Using breadcrumb navigation, you can directly drill up to any level of parent, and it displays the level from root parent to the current level at the top layout of TreeMap.

You can show or hide the breadcrumb using the `enableBreadcrumb` API. You can also customize the breadcrumb connector using the property `breadcrumbConnector` property. By default, `-` is the connector.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;' [dataSource]='data' weightValuePath='EmployeesCount' enableDrillDown= true  enableBreadcrumb= true breadcrumbConnector= ' -> '
    [levels]='levels' [palette]='palette'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
        { Category: 'Employees', Country: 'USA', JobDescription: 'Sales', JobGroup: 'Executive', EmployeesCount: 20 },
    { Category: 'Employees', Country: 'USA', JobDescription: 'Sales', JobGroup: 'Analyst', EmployeesCount: 30 },
    { Category: 'Employees', Country: 'USA', JobDescription: 'Marketing', EmployeesCount: 40 },
    { Category: 'Employees', Country: 'USA', JobDescription: 'Management', EmployeesCount: 80 },
    { Category: 'Employees', Country: 'India', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 100 },
    { Category: 'Employees', Country: 'India', JobDescription: 'HR Executives', EmployeesCount: 30 },
    { Category: 'Employees', Country: 'India', JobDescription: 'Accounts', EmployeesCount: 40 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Sales', JobGroup: 'Executive', EmployeesCount: 50 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Sales', JobGroup: 'Analyst', EmployeesCount: 60 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Marketing', EmployeesCount: 70 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 80 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Management', EmployeesCount: 10 },
    { Category: 'Employees', Country: 'Germany', JobDescription: 'Accounts', EmployeesCount: 20 },
    { Category: 'Employees', Country: 'UK', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 30 },
    { Category: 'Employees', Country: 'UK', JobDescription: 'HR Executives', EmployeesCount: 50 },
    { Category: 'Employees', Country: 'UK', JobDescription: 'Accounts', EmployeesCount: 60 },
    { Category: 'Employees', Country: 'France', JobDescription: 'Technical', JobGroup: 'Testers', EmployeesCount: 70 },
    { Category: 'Employees', Country: 'France', JobDescription: 'Marketing', EmployeesCount: 100 }
    ];
    public palette: object= ["#f44336", "#29b6f6", "#ab47bc", "#ffc107", "#5c6bc0", "#009688"],
    public levels: object = [
        { groupPath: 'Country', border: { color: 'black', width: 0.5 } },
        { groupPath: 'JobDescription', border: { color: 'black', width: 0.5 } },
        { groupPath: 'JobGroup', border: { color: 'black', width: 0.5 } },
    ]
}

```

{% endtab %}