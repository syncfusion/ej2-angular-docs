# Tooltip

Tooltip is used to display details about the items in tree map when the mouse hovers over the item.

## Default tooltip

By default, tooltip is not visible. You can enable the tooltip by setting the `enable` property to true and injecting the `TreeMapTooltip` module using the `TreeMap.Inject(TreeMapTooltip)`.

The following example shows the default tooltip.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;'  [dataSource]='data' weightValuePath='count'
    [leafItemSettings]='leafItemSettings' [tooltipSettings]='tooltipSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [{ fruit:'Apple', count:5000 },
                       { fruit:'Mango', count:3000 },
                       { fruit:'Orange', count:2300 },
                       { fruit:'Banana', count:500 },
                       { fruit:'Grape', count:4300 },
                       { fruit:'Papaya', count:1200 },
                       { fruit:'Melon', count:4500 }
    ];
    public leafItemSettings: object = {
        labelPath: 'fruit'
    };
    public tooltipSettings: object = {
            visible: true
    },
}

```

{% endtab %}

## Format tooltip

By default, tooltip shows information about weight value of current item. In addition, to show more information in tooltip, format the tooltip as `${datafield}` from data source.

The following example shows formatting the tooltip.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;'  [dataSource]='data' weightValuePath='count'
    [leafItemSettings]='leafItemSettings' [tooltipSettings]='tooltipSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [{ fruit:'Apple', count:5000 },
                       { fruit:'Mango', count:3000 },
                       { fruit:'Orange', count:2300 },
                       { fruit:'Banana', count:500 },
                       { fruit:'Grape', count:4300 },
                       { fruit:'Papaya', count:1200 },
                       { fruit:'Melon', count:4500 }
    ];
    public leafItemSettings: object = {
        labelPath: 'fruit'
    };
    public tooltipSettings: object = {
            visible: true,
            format:'Name:${fruit} - TotalCount:${count}'
    },
}

```

{% endtab %}

## Tooltip template

Any HTML element can be displayed in tooltip using the ‘template’ property. You can use `${datafield}` as placeholder in HTML element to display the values from data source.

The following example shows tootip template.
{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;'  [dataSource]='data' weightValuePath='count'
    [leafItemSettings]='leafItemSettings' [tooltipSettings]='tooltipSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [{ fruit:'Apple', count:5000 },
                       { fruit:'Mango', count:3000 },
                       { fruit:'Orange', count:2300 },
                       { fruit:'Banana', count:500 },
                       { fruit:'Grape', count:4300 },
                       { fruit:'Papaya', count:1200 },
                       { fruit:'Melon', count:4500 }
    ];
    public leafItemSettings: object = {
        labelPath: 'fruit'
    };
    public tooltipSettings: object = {
            visible: true,
            template:'<div><p>Name: ${fruit}</p><p>Total Count: ${count}</p></div>'
    },
}

```

{% endtab %}
