---
title: "ListView Grouping"
component: "ListView"
description: "Angular listView component supports grouping feature that helps group the logically related items under a category."
---

# Grouping

ListView supports to wrap the nested element into a group based on category.

The category of each list item can be mapped with groupBy field in the data table, which also supports single-level navigation.

In below sample, Cars are grouped based on its category using groupBy field.

{% tab template="listview/grouping", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component} from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<ejs-listview id='sample-list' [dataSource]='data' [fields]='fields' ></ejs-listview>`
})

export class AppComponent {
    public data: Object = [
    {
        'text': 'Audi A4',
        'id': '9bdb',
        'category': 'Audi'
    },
    {
        'text': 'Audi A5',
        'id': '4589',
        'category': 'Audi'
    },
    {
        'text': 'BMW 501',
        'id': 'f849',
        'category': 'BMW'
    },
    {
        'text': 'BMW 502',
        'id': '7aff',
        'category': 'BMW'
    }
    ];

    public fields: Object = { groupBy: 'category', tooltip: 'text' };

}

```

{% endtab %}

## Customization

The grouping header can be customized by using groupTemplate property for both inline and fixed group header.