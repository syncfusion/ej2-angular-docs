---
title: " Bullet Chart Customization | Angular "

component: "Bullet Chart"

description: "Bullet Chart have different customizable features like different orientation, flow directions and animation features"
---
<!-- markdownlint-disable MD036 -->

# Orientation

Bullet Chart can be rendered in different mode as `Horizontal` or `vertical` by using `orientation` property of the bullet-chart. By default bullet-chart rendered in horizontal mode.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart targetField='target' valueField='value' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' labelFormat='${value}'  title='Sales Rate in dollars'
  subtitle='(in dollars $)'  width='25%' orientation='Vertical'>
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
}
```

{% endtab %}

## Flow Direction

Using `enableRtl` boolean property of the bullet-chart, you can render bullet-chart in right to left or left to right direction.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart targetField='target' valueField='value' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' labelFormat='${value}'  title='Sales Rate in dollars'
  subtitle='(in dollars $)' enableRtl=true>
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
}
```

{% endtab %}

## Animation

By setting `animation` property value as `true`, you can enable the linear animation of the feature and target bars.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation'>
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
  public animation: AnimationModel = { enable: true };
}
```

{% endtab %}

## Theme

Bullet chart also support different types of themes. Using `theme` property of the bullet-chart, you can customize the theme styles.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart targetField='target' valueField='value' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate in dollars'
  subtitle='(in dollars $)'  theme='HighContrast'>
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
}
```

{% endtab %}