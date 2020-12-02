---
title: " Bullet Chart Title and SubTitle | Angular "

component: "Bullet Chart"

description: "The title and sub-title is very useful to understand the bullet chart in efficient way. It describes what kind of data which represtend by the bullet-chart. "
---
<!-- markdownlint-disable MD036 -->

# Title

A title can be given to a bullet chart using the `title` property to show information about the data plotted.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate'>
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
}
```

{% endtab %}

## SubTitle

A subtitle can also be given to a bullet chart using the `subtitle` property to show additional information about the data plotted.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate' subtitle='(in dollars $)'
  labelFormat='${value}'>
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
}
```

{% endtab %}

## Title and SubTitle Position

You can place the title and subtitle in different positions. By using the `titlePosition` property of the bullet chart, you can place the title and subtitles in different positions like `left`, `right`, `top`, and `bottom`.

**Position as Left**

By setting the `titlePosition` to `Left`, you can display the title and subtitle at the left side of the chart.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate' subtitle='(in dollars $)'
  labelFormat='${value}'  titlePosition='Left'>
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
}
```

{% endtab %}

**Position as Right**

By setting the `titlePosition` to `Right`, you can display the title and subtitle at the right side of the chart.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate' subtitle='(in dollars $)'
  labelFormat='${value}'  titlePosition='Right'>
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
}
```

{% endtab %}

**Position as Top**

By setting the `titlePosition` to `Top`, you can display the title and subtitle at the top of the chart. The default title and subtitle positions of the bullet chart is `Top`.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate' subtitle='(in dollars $)'
  labelFormat='${value}'  titlePosition='Top'>
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
}
```

{% endtab %}

**Position as Bottom**

By setting the `titlePosition` to `Bottom`, you can display the title and subtitle at the bottom of the chart.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate' subtitle='(in dollars $)'
  labelFormat='${value}'  titlePosition='Bottom'>
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
}
```

{% endtab %}

## Title Customization

You can customize the bullet chart title’s `fontStyle`, `size`, `color`, `fontWeight`, and `fontFamily` using the `titleStyle` property.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate' subtitle='(in dollars $)'
  labelFormat='${value}' [titleStyle]='titleStyle'>
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
  public titleStyle: Object =  { size: '22px', color: 'red', fontFamily: 'cursive', fontWeight: 'Bold'};
}
```

{% endtab %}

## SubTitle Customization

You can customize the bullet chart subtitle’s `fontStyle`, `size`, `color`, `fontWeight`, and `fontFamily` using the `subtitleStyle` property.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart valueField='value' targetField='target' [minimum]='minimum' [maximum]='maximum'
  [interval]='interval' [dataSource]='data' [animation]='animation' title='Sales Rate' subtitle='(in dollars $)'
  labelFormat='${value}' [subtitleStyle]='subtitleStyle'>
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
  public subtitleStyle: Object =  { size: '22px', color: 'red', fontFamily: 'cursive', fontWeight: 'Bold'};
}
```

{% endtab %}