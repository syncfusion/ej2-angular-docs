---
title: "Slider Ticks"
component: "Slider"
description: "Angular slider visually represents the slider values with small and large ticks placed before, after, or both, of the slider bar."
---

# Ticks

The Ticks in Slider supports you to easily identify the current value/values of the Slider. It contains `smallStep` and
`largeStep`. The value of the major ticks alone will be displayed in the slider. In order to enable/disable the small ticks,
use the `showSmallTicks` property.

{% tab template="slider/ticks-01", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
  public value: number =30;
  public tooltip: Object = { placement: 'Before', isVisible: true, showOn: 'Always' };
  public ticks: Object = { placement: 'After', largeStep: 20, smallStep: 10, showSmallTicks: true };
}

```

{% endtab %}

## Step

When the Slider is moved, it increases/decreases the value
based on the step value. By default, the value is increased/decreased by 1. Use the `step` property to change the increment step value.

{% tab template="slider/ticks-02", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
  public value: number = 30;
  public tooltip: Object = { placement: 'Before', isVisible: true, showOn: 'Always' };
  public ticks: Object = { placement: 'After', largeStep: 20, smallStep: 10, showSmallTicks: true };
  public step: number = 10;
}

```

{% endtab %}

## Min and Max

Enables the minimum/starting and maximum/ending value of the Slider, by using the `min` and `max`
property. By default, the minimum value is 1 and maximum value is 100. In the following sample the slider is rendered with
the min value as 100 and max value as 1000.

{% tab template="slider/ticks-03", sourceFiles="app/**/*,index.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    templateUrl: 'app/template.html',
    styleUrls:['index.css']
})

export class AppComponent {
    public min: number = 0;
    public max: number = 100;
    public value: number = 30;
    public ticks: Object =  { placement: 'After', largeStep: 20, smallStep: 10, showSmallTicks: true };
    public tooltip: Object = { placement: 'Before', isVisible: true, showOn: 'Always' };
}

```

{% endtab %}
