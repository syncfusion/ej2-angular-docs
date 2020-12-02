---
title: "Autocomplete Filtering"
component: "AutoComplete"
description: "This section for Syncfusion angular autocomplete component explains the built-in filtering support with a rich set of filtering configurations."
---

# Filtering

The AutoComplete has built-in support to filter data items. The filter operation
starts as soon as you start typing characters in the component.

## Change the filter type

Determines on which filter type, the component needs to be considered on search action.
The available [`filterType`](../api/auto-complete/#filtertype) and its supported data types are

| **Filter Type** | **Description** | **Supported Types** |
| --- | --- |
| StartsWith | Checks whether a value begins with the specified value. | String |
| EndsWith | Checks whether a value ends with specified value. | String |
| Contains | Checks whether a value contains with specified value. | String |

The following examples shows the data filtering is done with `StartsWith` type.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
//import DataManager related classes
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='sportsData' [fields]='fields' [placeholder]='text' [query]='query' [filterType]='filterType' [sortOrder]='sorting'></ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    //bind the DataManager instance to dataSource property
    public sportsData: DataManager = new DataManager({
            url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Customers',
            adaptor: new ODataV4Adaptor,
            crossDomain: true
        });
    // maps the appropriate column to fields property
    public fields: Object = { value: 'ContactName' };
    //bind the Query instance to query property
    public query: Query = new Query().select(['ContactName', 'CustomerID']).take(6);
    //set the placeholder to AutoComplete input
    public text: string = "Find a customer";
    //set the filterType to searching operation
    public filterType: string='StartsWith';
    //sort the result items
    public sorting: string = 'Ascending';
}

```

{% endtab %}

## Filter item count

You can specify the filter suggestion item count through
[`suggestionCount`](../api/auto-complete/#suggestioncount) property of AutoComplete.

The following examples, to restrict the suggestion list item counts as 5.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
//import DataManager related classes
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='sportsData' [fields]='fields' [placeholder]='text' [query]='query' [filterType]='filterType' [sortOrder]='sorting' [suggestionCount]='suggestionCount'></ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    //bind the DataManager instance to dataSource property
    public sportsData: DataManager = new DataManager({
            url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Customers',
            adaptor: new ODataV4Adaptor,
            crossDomain: true
        });
    // maps the appropriate column to fields property
    public fields: Object = { value: 'ContactName' };
    //bind the Query instance to query property
    public query: Query = new Query().select(['ContactName', 'CustomerID']);
    //set the placeholder to AutoComplete input
    public text: string = "Find a customer";
    //set the filterType to searching operation
    public filterType: string='StartsWith';
    //sort the result items
    public sorting: string = 'Ascending';
    //set the suggestionCount to show the maximum suggestion list item
    public suggestionCount: Number= 5;
}

```

{% endtab %}

## Limit the minimum filter character

You can set the limit for the character count to filter the data on the AutoComplete. This can be done by
set the [`minLength`](../api/auto-complete/#minlength) property to AutoComplete.

In the following example, the remote request doesn't fetch the search data, until the search key contains three characters.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
//import DataManager related classes
import { Query, DataManager, ODataV4Adaptor } from '@syncfusion/ej2-data';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='sportsData' [fields]='fields' [placeholder]='text' [query]='query' [filterType]='filterType' [sortOrder]='sorting' [minLength]='minLength'></ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    //bind the DataManager instance to dataSource property
    public sportsData: DataManager = new DataManager({
            url: 'https://services.odata.org/V4/Northwind/Northwind.svc/Customers',
            adaptor: new ODataV4Adaptor,
            crossDomain: true
        });
    // maps the appropriate column to fields property
    public fields: Object = { value: 'ContactName' };
    //bind the Query instance to query property
    public query: Query = new Query().select(['ContactName', 'CustomerID']);
    //set the placeholder to AutoComplete input
    public text: string = "Find a customer";
    //set the filterType to searching operation
    public filterType: string='StartsWith';
    //sort the result items
    public sorting: string = 'Ascending';
    //set the minLength to restrict the remote request until search key contains 3 characters.
    public minLength: Number = 3;
}

```

{% endtab %}

## Case sensitive filtering

Data items can be filtered either with or without case sensitivity using the DataManager.
This can be done by setting the [`ignoreCase`](../api/auto-complete/#ignorecase) property of AutoComplete.

The following sample depicts how to filter the data with case-sensitive.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='data' [placeholder]='text' [filterType]='filterType' [sortOrder]='sorting' [ignoreCase]='ignoreCase'></ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    //bind the DataManager instance to dataSource property
    public data: string[] = ['Badminton', 'Basketball', 'Cricket', 'Football', 'Golf', 'Gymnastics', 'Hockey', 'Tennis'];
    //set the placeholder to AutoComplete input
    public text: string = "Find a game Eg: FootBall";
    //set the filterType to searching operation
    public filterType: string='StartsWith';
    //sort the result items
    public sorting: string = 'Ascending';
    //set the minLength to restrict the remote request until search key contains 3 characters.
    public ignoreCase: Boolean = false;
}

```

{% endtab %}

## Diacritics Filtering

An AutoComplete supports diacritics filtering which will ignore the [diacritics](https://en.wikipedia.org/wiki/Diacritic) and
makes it easier to filter the results in international characters lists
when the [ignoreAccent](../api/auto-complete/#ignoreaccent) is enabled.

In the following sample,data with diacritics are bound as dataSource for AutoComplete.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: ` <ejs-autocomplete id='diacritics' [dataSource]='data' [ignoreAccent]='true' placeholder='e.g. aero'>
        </ejs-autocomplete>`
})
export class AppComponent {
    constructor() {
    }
    // create local data
      public data: string[] = [
        'Aeróbics',
        'Aeróbics en Agua',
        'Aerografía',
        'Aeromodelaje',
        'Águilas',
        'Ajedrez',
        'Ala Delta',
        'Álbumes de Música',
        'Alusivos',
        'Análisis de Escritura a Mano'];
}
```

{% endtab %}

## See Also

* [How to achieve autofill while filtering](./how-to/autofill/)
* [How to group the data using header](./grouping/)
* [How to highlight the search data](./how-to/custom-search/)