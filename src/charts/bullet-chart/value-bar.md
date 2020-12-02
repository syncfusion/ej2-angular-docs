---
title: " Bullet Chart Value Bar | TypeScript "

component: "Bullet Chart"

description: "The main data value is encoded by a length of the main bar in the middle of the chart, known as the Feature Measure. "
---
<!-- markdownlint-disable MD036 -->

# Feature Bar

The main data value is encoded by a length of the main bar in the middle of the chart, known as the `Feature Measure`. This is also called as `value Bar`. Also, if you want to display the target bar you should map the `valueField` name from the dataSource.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' targetWidth=15 [tooltip]='tooltip'>
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
      { value: 55, target: 75 }
    ];
  public animation: AnimationModel = { enable: false };
  public tooltip: Object = { enable: false };
}
```

{% endtab %}

## Feature Bar Types

You can customize the shape of the feature bar or value bar using the `type` property of the bullet chart. Feature bar contains `Rect` and `Dot` shapes. The default type of feature bar is `Rect`.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' type= 'Dot' [tooltip]='tooltip'>
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
      { value: 55, target: 75 }
    ];
  public animation: AnimationModel = { enable: false };
  public tooltip: Object = { enable: false };
}
```

{% endtab %}

## Customization

**Border Customization**

Using the `valueBorder` property of the bullet chart, you can customize the border `color` and `width` of the feature bar.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation'[valueBorder]='valueBorder' [tooltip]='tooltip'>
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
      { value: 55, target: 75 }
    ];
  public animation: AnimationModel = { enable: false };
  public valueBorder: Object =  { color: 'red', width: 3 };
  public tooltip: Object = { enable: false };
}
```

{% endtab %}

**Fill color and height Customization**

You can customize the fill color and height of the feature bar using the `valueFill` and `valueHeight` properties of the bullet chart.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' valueFill='blue' [tooltip]='tooltip'
  [valueHeight]='valueHeight'>
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
      { value: 55, target: 75 }
    ];
  public animation: AnimationModel = { enable: false };
  public valueBorder: Object =  { color: 'red', width: 3 };
  public tooltip: Object = { enable: false };
  public valueHeight: number = 15;
}
```

{% endtab %}