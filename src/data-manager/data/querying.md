---
title: "Angular DataManager | Querying | Syncfusion"
component: "DataManager"
description: "Learn how to build queries to be executed by the Angular DataManager by using the Query class to select fields, sort, filter, and group rows of a data source"
---

# Querying

In this section, you will see in detail about how to build query using [`Query`](https://ej2.syncfusion.com/documentation/api/data/query/) class and consume
the data source.

## Specifying resource name using `from`

The [`from`](https://ej2.syncfusion.com/documentation/api/data/query/#from) method is used to specify the resource name or table name from where the data should be retrieved.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ODataAdaptor, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI =  'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor()})
        .executeQuery(new Query().from('Orders').take(8)).then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}

## Projection using `select`

The [`select`](https://ej2.syncfusion.com/documentation/api/data/query/#select) method is used to select particular fields or columns from the data source.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ODataAdaptor, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI =  'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor()})
        .executeQuery(new Query().select(['OrderID', 'CustomerID', 'EmployeeID']).take(8))
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}

## Eager loading navigation properties

You can use the [`expand`](https://ej2.syncfusion.com/documentation/api/data/query/#expand) method to eagerly load navigation properties. The navigation properties
values are accessed using appropriate field names separated by dot(.) sign.

{% tab template="data/expand", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI = 'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        new DataManager({ url: SERVICE_URI })
        .executeQuery(new Query().expand('Employee').select(['OrderID', 'CustomerID', 'Employee.FirstName']).take(8))
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}

## Sorting

You can use the [`sortBy`](https://ej2.syncfusion.com/documentation/api/data/query/#sortby) method to perform sort operation in the
data source. Default sorting order is **ascending**. To change the sort order, either you can
specify the second argument of [`sortBy`](https://ej2.syncfusion.com/documentation/api/data/query/#sortby) as **descending** or use the
[`sortByDesc`](https://ej2.syncfusion.com/documentation/api/data/query/#sortbydesc) method.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ODataAdaptor, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI: string =  'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor})
        .executeQuery(new Query().sortBy('CustomerID', 'descending').take(8))
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}
```

{% endtab %}

> Multi sorting can be performed by simply chaining the multiple `sortBy` methods.

## Filtering

You can use the [`where`](https://ej2.syncfusion.com/documentation/data/api-query.html#where) method to build filter criteria which allows you to get reduced view of
records. The [`where`](https://ej2.syncfusion.com/documentation/data/api-query.html#where) method can also be chained to form multiple filter criteria.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ODataAdaptor, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI =  'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor()})
        .executeQuery(new Query().sortBy('CustomerID', 'descending').take(8))
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}

### Filter Operators

Filter operators are generally used to specify the filter type. The various filter operators
supported by [`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) is listed below.

* greaterthan
* greaterthanorequal
* lessthan
* lessthanorequal
* equal
* notequal
* startswith
* endswith
* contains

> These filter operators are used for creating filter query using
[`where`](https://ej2.syncfusion.com/documentation/api/data/query/#where) method and [`Predicate`](https://ej2.syncfusion.com/documentation/api/data/predicate/) class.

### Build complex filter criteria using `Predicate`

Sometimes chaining [`where`](https://ej2.syncfusion.com/documentation/api/data/query/#where) method is not sufficient to create very
complex filter criteria, in such cases we can use [`Predicate`](https://ej2.syncfusion.com/documentation/api/data/predicate/) class to create composite filter criteria.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ODataAdaptor, Predicate, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI =  'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        let predicate: Predicate = new Predicate('EmployeeID', 'equal', 3);
        predicate = predicate.or('EmployeeID', 'equal', 2);

        new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor()})
        .executeQuery(new Query().where(predicate).take(8))
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}

## Searching

You can use the [`search`](https://ej2.syncfusion.com/documentation/api/data/query/#search) method to create search criteria, it
differs from the filter in the way that search criteria will applied to all fields in the data
source whereas filter criteria will be applied to a particular field.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ReturnOption } from '@syncfusion/ej2-data';
import { data } from './datasource';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        new DataManager(data as JSON[])
        .executeQuery(new Query().search('VI', ['CustomerID']))
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}

> You can search particular fields by passing the field name collection in the second argument of [`search`](https://ej2.syncfusion.com/documentation/api/data/query/#search) method.

## Grouping

[`DataManager`](https://ej2.syncfusion.com/documentation/api/data/dataManager/) allow you to group records by category. The
[`group`](https://ej2.syncfusion.com/documentation/api/data/query/#group) method is used to add group query.

{% tab template="data/group", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ODataAdaptor, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI =  'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor()})
        .executeQuery(new Query().group('CustomerID').take(8))
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}

> Multiple grouping can be done by simply chaining the [`group`](https://ej2.syncfusion.com/documentation/api/data/query/#group) method.

## Paging

You can query paged data using [`page`](https://ej2.syncfusion.com/documentation/data/api-query.html#page) method. This allow you to query
particular set of records based on the page size and index.

{% tab template="data/getting-started/default", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ODataAdaptor, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI =  'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor()})
        .executeQuery(new Query().page(2, 6))
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}

## Aggregation

The [`aggregate`](https://ej2.syncfusion.com/react/documentation/data/querying/#aggregation) method allows you to get aggregated value for a field based on the type.

The built-in aggregate types are,

* sum
* average
* min
* max
* count
* truecount
* falsecount

{% tab template="data/aggregate", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ODataAdaptor, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI =  'https://js.syncfusion.com/demos/ejServices/Wcf/Northwind.svc/Orders';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];
    public min = 0;

    public ngOnInit(): void {
        new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor()})
        .executeQuery(new Query().take(5).requiresCount().aggregate('min', 'EmployeeID'))
        .then((e: ReturnOption) => { this.items = e.result as object[];  this.min = e.aggregates['EmployeeID - min']; }).catch((e) => true);
    }
}

```

{% endtab %}

## Hierarchical query

You can use the [`hierarchy`](https://ej2.syncfusion.com/documentation/api/data/query/#hierarchy) method to build nested query.
The hierarchical queries are commonly required when you use foreign key binding.

The [`foreignKey`](https://ej2.syncfusion.com/documentation/api/data/query/#foreignkey) method is used to specify the key field of the
foreign table and the second argument of the [`hierarchy`](https://ej2.syncfusion.com/documentation/api/data/query/#hierarchy) method
accepts a selector function which selects the records from the foreign table.

{% tab template="data/hierarchy", sourceFiles="app/**/*.ts,app/**/*.html" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { DataManager, Query, ODataAdaptor, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI = 'http://mvc.syncfusion.com/Services/Northwnd.svc/';

@Component({
    selector: 'app-root',
    templateUrl: 'app.template.html',
    styles: [`
            .e-table {
                border: solid 1px #e0e0e0;
                border-collapse: collapse;
                font-family: Roboto;
            }

            .e-table td, .e-table th {
                border-style: solid;
                border-width: 1px 0 0;
                border-color: #e0e0e0;
                display: table-cell;
                font-size: 14px;
                line-height: 20px;
                overflow: hidden;
                padding: 8px 21px;
                vertical-align: middle;
                white-space: nowrap;
                width: auto;
            }
    `]
})
export class AppComponent implements OnInit {

    public items: object[];

    public ngOnInit(): void {
        new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor()})
        .executeQuery(new Query().from('Orders').take(3).hierarchy(
                    new Query()
                        .foreignKey('OrderID')
                        .from('Order_Details')
                        .sortBy('Quantity'),
                    () => [10248, 10249, 10250] // Selective loading of child elements
                ))
        .then((e: ReturnOption) => this.items = e.result as object[]).catch((e) => true);
    }
}

```

{% endtab %}