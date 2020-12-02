---
title: " Bullet Chart Target Bar | Angular "

component: "Bullet Chart"

description: "The line marker that runs perpendicular to the orientation of the graph is known as the `Comparative Measure`. "
---
<!-- markdownlint-disable MD036 -->

# Target Bar

The line marker that runs perpendicular to the orientation of the graph is known as the `Comparative Measure` and is used as a target marker to compare against the Feature Measure value. This is also called as `Target Bar` of the bullet chart. Also, if you want to display the target bar you should map the `targetField` name from the dataSource.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' [tooltip]='tooltip'>
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

## Target Bar Types

You can customize the shape of the target bar or comparative bar using the `targetTypes` property of the bullet chart. Target bar contains `Circle`, `Cross`, and `Rect` shapes. The default type of target bar is `Rect`.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' [targetTypes]='targetTypes' [tooltip]='tooltip'>
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
  public targetTypes: string[] = ['Circle'];
  public animation: AnimationModel = { enable: false };
  public tooltip: Object = { enable: false };
}
```

{% endtab %}

## Customization

**Color Customization**

Using the `targetColor` property of the bullet chart, you can customize the fill color of the target bar.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' targetColor='red' [tooltip]='tooltip'>
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

**Width Customization**

You can customize the width of the target bar using the `targetWidth` property of the bullet chart.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart targetField='target' [minimum]='minimum' [maximum]='maximum'
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