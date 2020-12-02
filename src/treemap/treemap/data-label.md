# Data Label

Data labels are used to identify the name of items or groups in the tree map control. Data Labels will be shown by given specified path in the data source field.

The following options are available to customize labels in the tree map control.

## Format

You can customize the labels for each item using the [`labelFormat`] property in leafItemSettings.

The label format is shown in the following code example.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;' height='350px' [dataSource]='data' weightValuePath='count'
    [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
        { Car:'Mustang', Brand:'Ford', count:232 },
                       { Car:'EcoSport', Brand:'Ford', count:121 },
                       { Car:'Swift', Brand:'Maruti', count:143 },
                       { Car:'Baleno', Brand:'Maruti', count:454 },
                       { Car:'Vitara Brezza', Brand:'Maruti', count:545 },
                       { Car:'A3 Cabriolet', Brand:'Audi',count:123 },
                       { car:'RS7 Sportback', Brand:'Audi', count:523 }
    ];
    public leafItemSettings: object = {
        labelPath: 'Car',
        format:'${Car}-${Brand}'
    };
}

```

{% endtab %}

## Template

The template supports customizing labels of each leaf node using the [`labelTemplate`] property. It uses Essential JS2 Template engine to render elements. You can position templates using the [`templatePosition`] property.

The template concepts are shown in the following code example.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;' height='350px' [dataSource]='data' weightValuePath='count'
    [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
                       { Car:'Mustang', Brand:'Ford', count:232 },
                       { Car:'EcoSport', Brand:'Ford', count:121 },
                       { Car:'Swift', Brand:'Maruti', count:143 },
                       { Car:'Baleno', Brand:'Maruti', count:454 },
                       { Car:'Vitara Brezza', Brand:'Maruti', count:545 },
                       { Car:'A3 Cabriolet', Brand:'Audi',count:123 },
                       { car:'RS7 Sportback', Brand:'Audi', count:523 }
    ];
    public leafItemSettings: object = {
        labelPath: 'Car',
        labelTemplate:'<div>{{:Car}}-{{:Brand}}</div>',
        templatePosition:'Center'
    };
}

```

{% endtab %}

## InterSectAction

You can avoid overlapping by customizing labels in each item when they exceed their actual size using the [`interSectAction`] property in leafItemSettings.

The intersect action concepts are illustrated in the following code example.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;' height='350px' [dataSource]='data' weightValuePath='count'
    [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
                       { Car:'Mustang', Brand:'Ford', count:232 },
                       { Car:'EcoSport', Brand:'Ford', count:121 },
                       { Car:'Swift', Brand:'Maruti', count:143 },
                       { Car:'Baleno', Brand:'Maruti', count:454 },
                       { Car:'Vitara Brezza', Brand:'Maruti', count:545 },
                       { Car:'A3 Cabriolet', Brand:'Audi',count:123 },
                       { car:'RS7 Sportback', Brand:'Audi', count:523 }
    ];
    public leafItemSettings: object = {
        labelPath: 'Car',
        format:'${Car}-${Brand}',
        interSectAction:'WrapByWord'
    };
}

```

{% endtab %}
