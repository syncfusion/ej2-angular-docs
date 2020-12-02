---
title: "BulletChart Tooltip | Angular "

component: "BulletChart"

description: "Tooltip is used to show the data value when mouse hover on the chart.We can able to customize format,template and appearance."
---

# Tooltip

<!-- markdownlint-disable MD036 -->

BulletChart will display details about the actual and target values through tooltip, when the mouse is moved over the target and feature bar.

## Default Tooltip

By setting [`enable`](https://ej2.syncfusion.com/documentation/api/bullet-chart/bulletTooltipSettingsModel/#enable)property to true and by injecting `BulletTooltip` module
using `BulletChart.Inject(BulletTooltip)`. By default tooltip is visible in bullet-chart.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate' subtitle='(in dollars $)'
  labelFormat='${value}' [tooltip]='tooltip'>
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
      { value: 55, target: 45 }
    ];
  public animation: AnimationModel = { enable: false };
  public tooltip: Object = { enable: true };
}
```

{% endtab %}

## Tooltip Template

Any HTML elements can be displayed in the tooltip by using the `template` property of the tooltip. You can use the ${target} and ${value} as place holders in the HTML element to display the value and target values of the corresponding data point.

{% tab template="bullet-chart/user-interaction/tooltipTemplate", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate' subtitle='(in dollars $)'
  labelFormat='${value}K' [tooltip]='tooltip' height='110px'>
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
      { value: 55, target: 45 }
    ];
  public animation: AnimationModel = { enable: false };
  public tooltip: Object = { enable: true, template : '#Tooltip' };
}
```

{% endtab %}

## Customize the Appearance of Tooltip

The [`fill`](./https://ej2.syncfusion.com/documentation/api/bullet-chart/bulletTooltipSettingsModel/#fill) and [`border`](./https://ej2.syncfusion.com/documentation/api/bullet-chart/bulletTooltipSettingsModel/#border) properties are used to customize the background color and border of the tooltip respectively. The [`textStyle`](./https://ej2.syncfusion.com/documentation/api/bullet-chart/bulletTooltipSettingsModel/#textstyle) property in the tooltip is used to customize the font of the tooltip text.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate' subtitle='(in dollars $)'
  labelFormat='${value}' [tooltip]='tooltip'>
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
      { value: 55, target: 45 }
    ];
  public animation: AnimationModel = { enable: false };
  public tooltip: Object = { enable: true, fill: 'red', border:{ color: 'green', width: 10 } };
}
```

{% endtab %}