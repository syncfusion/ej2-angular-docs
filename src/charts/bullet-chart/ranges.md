---
title: " Bullet Chart Ranges | Angular "

component: "Bullet Chart"

description: "Bullet Chart scale can be rendered by using different types of end values. They are used to represnt the status of each data. "
---
<!-- markdownlint-disable MD036 -->

# Ranges

`Ranges` are represents the quality of a specific range in bullet-chart scale like good, bad and satisfactory. The `end` property specifies the ending point of the qualitative range. `Minimum` value of quantitative scale is considered as the starting point of first range and previous end points are considered as starting point for other ranges.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart targetField='target' valueField='value' categoryField='category' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' height='400' [categoryLabelStyle]='categoryLabelStyle'
title='Sales Rate'>
  <e-bullet-range-collection>
    <e-bullet-range end='35' color='#ebebeb'></e-bullet-range>
    <e-bullet-range end='70' color='#d8d8d8'></e-bullet-range>
    <e-bullet-range end='100' color='#7f7f7f'></e-bullet-range>
  </e-bullet-range-collection>
</ejs-bulletchart>`
})
export class AppComponent {
   public minimum: number = 0;
  public maximum: number = 100;
  public interval: number = 20;
  public data: Object[] = [
    { value: 55, target: 75, category: 'Year 1'  },
    { value: 70, target: 70, category: 'Year 2'  },
    { value: 85, target: 75, category: 'Year 3'  }
    ];
  public animation: AnimationModel = { enable: false };
  public categoryLabelStyle: Object = { color: 'red', size: '13', fontWeight: 'bold'};
}
```

{% endtab %}

## Color Customization

Color for each qualitative range is customized using `color` property based on end values. Also you can customize the opacity of the each range color.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart targetField='target' valueField='value' categoryField='category' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' height='400' [categoryLabelStyle]='categoryLabelStyle'
title='Sales Rate'>
  <e-bullet-range-collection>
    <e-bullet-range end='35' color='darkred'></e-bullet-range>
    <e-bullet-range end='50' color='red'></e-bullet-range>
    <e-bullet-range end='75' color='blue'></e-bullet-range>
    <e-bullet-range end='90' color='lightgreen'></e-bullet-range>
    <e-bullet-range end='100' color='green'></e-bullet-range>
  </e-bullet-range-collection>
</ejs-bulletchart>`
})
export class AppComponent {
  public minimum: number = 0;
  public maximum: number = 100;
  public interval: number = 20;
  public data: Object[] = [
    { value: 55, target: 75, category: 'Year 1'  },
    { value: 70, target: 70, category: 'Year 2'  },
    { value: 85, target: 75, category: 'Year 3'  }
    ];
  public animation: AnimationModel = { enable: false };
  public categoryLabelStyle: Object = { color: 'red', size: '13', fontWeight: 'bold'};
}
```

{% endtab %}