---
title: " Bullet Chart Appearance | Angular "

component: "Bullet Chart"

description: "We can set bullet-chart size manually by using width and height properties. We can set percentage or pixel size values to the bullet-chart."
---

# Bullet Chart Dimensions

## Size for Container

The bullet chart can be rendered to its container’s size. You can set the size using inline or CSS as shown below.

```html
    <div style="width:650px; height:350px;">
        <ejs-bulletchart id="app-container"></ejs-bulletchart>
    </div>
```

```javascript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<div style="width:650px; height:350px;">
        <ejs-bulletchart id="app-container"></ejs-bulletchart>
    </div>`
})
export class AppComponent {
    constructor(){
        /*
        */
    }
}
```

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' width='650px' height='350px'>
  <e-bullet-range-collection>
    <e-bullet-range end='20' color='#ebebeb'></e-bullet-range>
    <e-bullet-range end='25' color='#d8d8d8'></e-bullet-range>
    <e-bullet-range end='30' color='#7f7f7f'></e-bullet-range>
  </e-bullet-range-collection>
</ejs-bulletchart>`
})
export class AppComponent {
 public minimum: number = 0;
  public maximum: number = 30;
  public interval: number = 5;
  public data: Object[] = [
      { value: 23, target: 22 }
    ];
  public animation: AnimationModel = { enable: false };
}
```

{% endtab %}
<!-- markdownlint-disable MD036 -->

## Size for Bullet Chart

<!-- markdownlint-disable MD036 -->

You can also set the size for bullet chart directly using the [`width`](../api/bullet-chart/bulletChartModel/#width) and [`height`](../api/bullet-chart/bulletChartModel/#height) properties.

**In Pixel**

You can set the size of a chart in pixels as shown below.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' width='650' height='350'>
  <e-bullet-range-collection>
    <e-bullet-range end='20' color='#ebebeb'></e-bullet-range>
    <e-bullet-range end='25' color='#d8d8d8'></e-bullet-range>
    <e-bullet-range end='30' color='#7f7f7f'></e-bullet-range>
  </e-bullet-range-collection>
</ejs-bulletchart>`
})
export class AppComponent {
 public minimum: number = 0;
  public maximum: number = 30;
  public interval: number = 5;
  public data: Object[] = [
      { value: 23, target: 22 }
    ];
  public animation: AnimationModel = { enable: false };
}
```

{% endtab %}

**In Percentage**

By setting a value in percentage, the bullet chart gets its dimension with respect to its container. For example, when the height is ‘50%’, the bullet chart renders to half of the container’s height.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' width='70%' height='60%'>
  <e-bullet-range-collection>
    <e-bullet-range end='20' color='#ebebeb'></e-bullet-range>
    <e-bullet-range end='25' color='#d8d8d8'></e-bullet-range>
    <e-bullet-range end='30' color='#7f7f7f'></e-bullet-range>
  </e-bullet-range-collection>
</ejs-bulletchart>`
})
export class AppComponent {
 public minimum: number = 0;
  public maximum: number = 30;
  public interval: number = 5;
  public data: Object[] = [
      { value: 23, target: 22 }
    ];
  public animation: AnimationModel = { enable: false };
}
```

{% endtab %}

>Note: When you do not specify the size, it takes `126px` as its height and window size as its width.