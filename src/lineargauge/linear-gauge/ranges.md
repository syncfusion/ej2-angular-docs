---
title: "Ranges in Angular Linear Gauge component | Syncfusion"

component: "Linear Gauge"

description: "Learn here all about the Ranges feature of Syncfusion Angular Linear Gauge component and more."
---

# Ranges in Angular Linear Gauge

<!-- markdownlint-disable MD013 -->
Range is the set of values in the axis. The range can be defined using the [`start`](../api/linear-gauge/rangeModel/#start) and [`end`](../api/linear-gauge/rangeModel/#end) properties in the [`e-range`](../api/linear-gauge/rangeModel/). Any number of ranges can be added to the Linear Gauge using the [`e-ranges`](../api/linear-gauge/axisModel/#ranges).

{% tab template= "linear-gauge/ranges", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
         <e-axis>
           <e-ranges>
             <e-range start=50 end=80></e-range>
           </e-ranges>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    ngOnInit(): void {
    }
}
```

{% endtab %}

## Customizing the range

Ranges can be customized using the following properties in [`e-range`](../api/linear-gauge/rangeModel/).

* [`startWidth`](../api/linear-gauge/rangeModel/#startwidth) - Customize the range thickness at the start axis value.
* [`endWidth`](../api/linear-gauge/rangeModel/#endwidth) - Customize the range thickness at the end axis value.
* [`color`](../api/linear-gauge/rangeModel/#color) - Customize the range color.
* [`position`](../api/linear-gauge/rangeModel/#position) - To place the range. By default, the range is placed outside of the axis. To change the position, this property can be set as "**Inside**", "**Outside**", "**Cross**", or "**Auto**".
* [`Offset`](../api/linear-gauge/rangeModel/#offset) - To place the range with specified distance from the axis.
* [`border`](../api/linear-gauge/rangeModel/#border) - Customize color and width of range border.

{% tab template= "linear-gauge/ranges", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
         <e-axis>
           <e-ranges>
             <e-range start=50 end=80 startWidth=15 endWidth=15 color="Orange"></e-range>
           </e-ranges>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    ngOnInit(): void {
    }
}
```

{% endtab %}

## Setting the range color for the labels

To set the color of the labels like the range color, set the [`useRangeColor`](../api/linear-gauge/labelModel/#userangecolor) property as **true** in the [`labelStyle`](../api/linear-gauge/axisModel/#labelstyle).

{% tab template= "linear-gauge/ranges", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
         <e-axis [labelStyle]='labelStyle'>
           <e-ranges>
             <e-range start=50 end=80 startWidth=15 endWidth=15 color="red"></e-range>
           </e-ranges>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
  public labelStyle: Object;
  ngOnInit(): void {
    this.labelStyle = {
      useRangeColor: true
    };
  }
}
```

{% endtab %}

## Multiple ranges

Multiple ranges can be added to the Linear Gauge by adding collections of [`e-range`](../api/linear-gauge/rangeModel/) in the [`e-ranges`](../api/linear-gauge/axisModel/#ranges) and customization of ranges can be done with [`e-range`](../api/linear-gauge/rangeModel/).

{% tab template= "linear-gauge/ranges", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
         <e-axis>
           <e-ranges>
             <e-range start=0 end=30 startWidth=10 endWidth=10 color='#41f47f'></e-range>
             <e-range start=30 end=50 startWidth=10 endWidth=10 color='#f49441'></e-range>
             <e-range start=50 end=100 startWidth=10 endWidth=10  color='#cd41f4'></e-range>
           </e-ranges>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
      ngOnInit(): void {
    }
}
```

{% endtab %}

## Gradient Color

Gradient support allows the addition of multiple colors in the range. The following gradient types are supported in the Linear Gauge.

* Linear Gradient
* Radial Gradient

### Linear Gradient

Using linear-gradient, colors will be applied in a linear progression. The start value of the linear gradient can be set using the [`startValue`](../api/linear-gauge/linearGradient/#startvalue) property. The end value of the linear gradient will be set using the [`endValue`](../api/linear-gauge/linearGradient/#endvalue) property. The color stop values such as [`color`](../api/linear-gauge/colorStopModel/#color), [`opacity`](../api/linear-gauge/colorStopModel/#opacity), and [`offset`](../api/linear-gauge/colorStopModel/#offset) to be defined in [`colorStop`](../api/linear-gauge/linearGradient/#colorstop).

{% tab template= "linear-gauge/ranges", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
     <ejs-lineargauge id="gauge-container" [container]='container' orientation='horizontal' [axes]='axes'>
    </ejs-lineargauge>`
})
export class AppComponent {
  public container: Object;
  public axes: Object[];
    ngOnInit(): void {
      // Initialize objects
      this.container = { width: 30, offset: 30 }
      this.axes = [{
        minimum: 0,
        maximum: 100,
        line: {
          width: 0
        },
        majorTicks: {
          interval: 25,
          height: 0
        },
        minorTicks: {
          height: 0
        },
        labelStyle: {
          font: {
          color: '#424242',
          }, offset: 55
        },
        pointers: [{
          value: 80, height: 25,
          width: 35, placement: 'Near',
          offset: -44, markerType: 'Triangle',
          color: '#f54ea2'
        }],
        ranges: [{
          start: 0, end: 80,
          startWidth: 30, endWidth: 30,
          offset: 30,
          linearGradient: {
            startValue: '0%',
            endValue: '100%',
            colorStop: [
              { color: '#fef3f9', offset: '0%', opacity: 1 },
              { color: '#f54ea2', offset: '100%', opacity: 1 }]
          }
        }]
      }];
    }
}
```

{% endtab %}

### Radial Gradient

Using radial gradient, colors will be applied in circular progression. The inner circle position of the radial gradient will be set using the [`innerPosition`](../api/linear-gauge/radialGradient/#innerposition) property. The outer circle position of the radial gradient can be set using the [`outerPosition`](../api/linear-gauge/radialGradient/#outerposition) property. The color stop values such as [`color`](../api/linear-gauge/colorStopModel/#color), [`opacity`](../api/linear-gauge/colorStopModel/#opacity), and [`offset`](../api/linear-gauge/colorStopModel/#offset) to be defined in [`colorStop`](../api/linear-gauge/radialGradient/#colorstop).

{% tab template= "linear-gauge/ranges", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
     <ejs-lineargauge id="gauge-container" [container]='container' orientation='Horizontal' [axes]='axes'>
    </ejs-lineargauge>`
})
export class AppComponent {
  public container: Object;
  public axes: Object[];
    ngOnInit(): void {
      // Initialize objects
      this.container = { width: 30, offset: 30 }
      this.axes = [{
        minimum: 0,
        maximum: 100,
        line: {
          width: 0
        },
        majorTicks: {
          interval: 25,
          height: 0
        },
        minorTicks: {
          height: 0
        },
        labelStyle: {
          font: {
          color: '#424242',
          }, offset: 55
        },
        pointers: [{
          value: 80, height: 25,
          width: 35, placement: 'Near',
          offset: -44, markerType: 'Triangle',
          color: '#f54ea2'
        }],
        ranges: [{
          start: 0, end: 80,
          startWidth: 30, endWidth: 30,
          offset: 30,
          radialGradient: {
            radius: '65%',
            outerPosition: { x: '50%', y: '70%' },
            innerPosition: { x: '60%', y: '60%' },
            colorStop: [
            { color: '#fff5f5', offset: '5%', opacity: 0.9 },
            { color: '#f54ea2', offset: '100%', opacity: 0.9 }]
            }
        }]
      }];
    }
}
```

{% endtab %}

>If we set both gradients for the range, only the linear gradient gets rendered. If we set the [`startValue`](../api/linear-gauge/linearGradient/#startvalue) and [`endValue`](../api/linear-gauge/linearGradient/#endvalue) property of the [`linearGradient`](../api/linear-gauge/linearGradient/) as empty strings, then the radial gradient gets rendered in the range of the Linear Gauge.
