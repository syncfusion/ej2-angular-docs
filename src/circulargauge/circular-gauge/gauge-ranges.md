
# Ranges

You can categories certain interval on gauge axis using
[`ranges`](../api/circular-gauge/range/#properties) property.

## Start and End

Start and end value of a range in an axis can be customized by using
[`start`](../api/circular-gauge/range/#start-number) and [`end`](../api/circular-gauge/range/#end-number) properties.

{% tab template="circulargauge/gauge-ranges", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container">
        <e-axes>
            <e-axis>
                <e-ranges>
                    <e-range start=40 end=80></e-range>
                </e-ranges>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
        // Initialize objects.
    }
}

```

{% endtab %}

## Customization

Color and thickness of the range can be customized by using
[`color`](../api/circular-gauge/range/#color-string),
[`startWidth`](../api/circular-gauge/range/#startwidth-number) and
[`endWidth`](../api/circular-gauge/range/#endwidth-number) property.

{% tab template="circulargauge/gauge-ranges", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container">
        <e-axes>
            <e-axis minimum=0 maximum=100 [majorTicks]="majorTicks" [minorTicks]="minorTicks">
                <e-ranges>
                    <e-range start=40 end=80 startWidth=15 endWidth=15 color="#ff5985"></e-range>
                </e-ranges>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public majorTicks: object;
    public minorTicks: object;
    ngOnInit(): void {
        // Initialize objects.
        this.majorTicks = {
            interval: 10
        };
        this.minorTicks = {
            interval: 5
        };
    }
}

```

{% endtab %}

<!-- markdownlint-disable MD036 -->

## Radius

You can place the range inside or outside of the axis by using
[`radius`](../api/circular-gauge/range/#radius-string) property.
The radius of the range can takes value either in percentage or in pixels.
By default, ranges take 100% of the axis radius.

**In Pixel**

You can set the radius of the range in pixel as demonstrated below,

{% tab template="circulargauge/gauge-ranges", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container">
        <e-axes>
            <e-axis>
                <e-ranges>
                    <e-range start=40 end=80 radius='100'></e-range>
                </e-ranges>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
        // Initialize objects.
    }
}

```

{% endtab %}

<!-- markdownlint-disable MD036 -->

**In Percentage**

By setting value in percentage, range gets its dimension with respect to its axis radius.
For example, when the radius is ‘50%’, range renders to half of the axis radius.

{% tab template="circulargauge/gauge-ranges", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container">
        <e-axes>
            <e-axis>
                <e-ranges>
                    <e-range start=40 end=80 radius='50%'></e-range>
                </e-ranges>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
        // Initialize objects.
    }
}

```

{% endtab %}

<!-- markdownlint-disable MD010 -->

## Dragging Range

The ranges can be dragged on the axis line by clicking and dragging the same. To enable or disable the range drag, use the [`enableRangeDrag`](../api/circular-gauge/circularGaugeModel/#enablerangedrag) property.

{% tab template="circulargauge/gauge-pointers", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" enableRangeDrag='true' height='250px' width='250px'>
        <e-axes>
            <e-axis>
                <e-pointers>
                    <e-pointer value=50></e-pointer>
                </e-pointers>
				 <e-ranges>
                    <e-range start=0 end=100 startWidth=8 endWidth=8 color="#30B32D" radius='108%'></e-range>
                </e-ranges>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public animation: object;
    ngOnInit(): void { }
}

```

{% endtab %}

## Multiple Ranges

You can add multiple ranges to an axis with the above customization as demonstrated below.

>Note: You can set the range color to axis ticks and labels by enabling `useRangeColor` property in [`majorTicks`](../api/circular-gauge/tick),
[`minorTicks`](../api/circular-gauge/tick) and [`labelStyle`](../api/circular-gauge/label) object.

{% tab template="circulargauge/gauge-ranges", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container">
        <e-axes>
            <e-axis [majorTicks]="majorTicks" [minorTicks]="minorTicks" [labelStyle]="labelStyle">
                <e-ranges>
                    <e-range start=0 end=25 radius='108%'></e-range>
                    <e-range start=25 end=50 radius='70%'></e-range>
                    <e-range start=50 end=75 radius='70%'></e-range>
                    <e-range start=75 end=100 radius='108%'></e-range>
                </e-ranges>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public majorTicks: object;
    public minorTicks: object;
    public labelStyle: object;
    ngOnInit(): void {
        // Initialize objects.
        this.majorTicks = {
            useRangeColor: true
        };
        this.minorTicks = {
            useRangeColor: true
        };
        this.labelStyle = {
            useRangeColor: true
        };
    }
}

```

{% endtab %}

## Rounded corner radius

You can customize the corner radius using the `roundedCornerRadius` property in `ranges`.

{% tab template="circulargauge/gauge-ranges", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container">
        <e-axes>
            <e-axis>
                <e-ranges>
                    <e-range start=40 end=80 radius='50%' roundedCornerRadius=6></e-range>
                </e-ranges>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
        // Initialize objects.
    }
}

```

{% endtab %}

## Gradient Color

Gradient support allows to add multiple colors in the ranges and pointers of the circular gauge. The following gradient types are supported in the circular gauge.

* Linear Gradient
* Radial Gradient

### Linear Gradient

Using linear gradient, colors will be applied in a linear progression. The start value of the linear gradient will be set using the [`startValue`](../api/circular-gauge/linearGradient/#startvalue) property. The end value of the linear gradient will be set using the [`endValue`](../api/circular-gauge/linearGradient/#endvalue) property. The color stop values such as color, opacity and offset are set using [`colorStop`](../api/circular-gauge/linearGradient/#colorstop) property.

To apply linear gradient to the range, follow the below code sample.

{% tab template="circulargauge/gauge-ranges", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
  selector: 'app-container',
  template: `
    <ejs-circulargauge style="display:block;">
      <e-axes>
        <e-axis minimum="0" radius="80%" maximum="100" startAngle="200" endAngle="160" [majorTicks]="majorTicks" [labelStyle]="labelStyle" [lineStyle]="lineStyle" [minorTicks]="minorTicks">
          <e-ranges>
            <e-range start="0" end="100" startWidth="30" endWidth="30" color="#E0E0E0" [roundedCornerRadius]="rounderCornerRadius" [linearGradient]="rangeLinearGradient"></e-range>
          </e-ranges>
          <e-pointers>
            <e-pointer pointerWidth="0" color="#007DD1" [cap]="pointerCap"></e-pointer>
          </e-pointers>
        </e-axis>
      </e-axes>
    </ejs-circulargauge>
  `
})
export class AppComponent {
    public rangeLinearGradient: object = {
        startValue: '0%',
        endValue: '100%',
        colorStop: [
           { color: '#9E40DC', offset: '0%', opacity: 0.9 },
           { color: '#E63B86', offset: '70%', opacity: 0.9 }
        ]
    };
    public rounderCornerRadius: number =20;
    public lineStyle: object = {
        width: 0
    };
    public labelStyle: object = {
       font: {
          size: '0px'
       }
    };
    public majorTicks: object = {
        height: 0
    };
    public minorTicks: object = {
        height: 0
    };
    public pointerCap: object = {
        radius: 0
    };
}

```

{% endtab %}

### Radial Gradient

Using radial gradient, colors will be applied in circular progression. The inner circle position of the radial gradient will be set using the [`innerPosition`](../api/circular-gauge/radialGradient/#innerposition) property. The outer circle position of the radial gradient can be set using the [`outerPosition`](../api/circular-gauge/radialGradient/#outerposition) property. The color stop values such as color, opacity and offset are set using [`colorStop`](../api/circular-gauge/radialGradient/#colorstop) property.

To apply radial gradient to the range, follow the below code sample.

{% tab template="circulargauge/gauge-ranges", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
  selector: 'app-container',
  template: `
    <ejs-circulargauge style="display:block;">
      <e-axes>
        <e-axis minimum="0" radius="80%" maximum="100" startAngle="200" endAngle="160" [majorTicks]="majorTicks" [labelStyle]="labelStyle" [lineStyle]="lineStyle" [minorTicks]="minorTicks">
          <e-ranges>
            <e-range start="0" end="100" startWidth="30" endWidth="30" color="#E0E0E0" [roundedCornerRadius]="rounderCornerRadius" [radialGradient]="rangeRadialGradient"></e-range>
          </e-ranges>
          <e-pointers>
            <e-pointer pointerWidth="0" color="#007DD1" [cap]="pointerCap"></e-pointer>
          </e-pointers>
        </e-axis>
      </e-axes>
    </ejs-circulargauge>
  `
})
export class AppComponent {
    public rangeRadialGradient: object = {
        radius: '50%',
        innerPosition: { x: '50%', y: '50%' },
        outerPosition: { x: '50%', y: '50%' },
        colorStop: [
            { color: '#9E40DC', offset: '90%', opacity: 0.9 },
            { color: '#E63B86', offset: '160%', opacity: 0.9 }
       ]
    };
    public rounderCornerRadius: number =20;
    public lineStyle: object = {
        width: 0
    };
    public labelStyle: object = {
       font: {
          size: '0px'
       }
    };
    public majorTicks: object = {
        height: 0
    };
    public minorTicks: object = {
        height: 0
    };
    public pointerCap: object = {
        radius: 0
    };
}

```

{% endtab %}

## See also

* [Tooltip for Ranges](https://ej2.syncfusion.com/angular/documentation/circular-gauge/gauge-user-interaction/#tooltip-for-ranges/)
