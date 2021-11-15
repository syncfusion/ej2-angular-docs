---
title: "Axis in Angular Linear Gauge Component | Syncfusion"

component: "Linear Gauge"

description: "Learn here all about Axis feature of Syncfusion Angular Linear Gauge component and more."
---

# Axis in Angular Linear Gauge

<!-- markdownlint-disable MD013 -->

Axis is used to indicate the numeric values in the linear scale. The Linear Gauge component can have any number of axes. The sub-elements of an axis are line, ticks, labels, ranges, and pointers.

## Setting the start value and end value of the axis

The start value and end value for the Linear Gauge can be set using the [`minimum`](../api/linear-gauge/axisModel/#minimum) and [`maximum`](../api/linear-gauge/axisModel/#maximum) properties in the [`e-axis`](../api/linear-gauge/axisModel/) respectively. By default, the start value of the axis is **0** and the end value of the axis is **100**.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis minimum=20 maximum=200>
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

## Line Customization

The following properties in the [`line`](../api/linear-gauge/lineModel) can be used to customize the axis line in the Linear Gauge.

* [`height`](../api/linear-gauge/lineModel/#height) - To set the length of the axis line.
* [`width`](../api/linear-gauge/lineModel/#width) - To set the thickness of the axis line.
* [`color`](../api/linear-gauge/lineModel/#color) - To set the color of the axis line.
* [`offset`](../api/linear-gauge/lineModel/#offset) - To render the axis line with the specified distance from the Linear Gauge.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [line]='line'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public line:Object;
    ngOnInit(): void {
        this.line = {
            height: 150,
            width: 2,
            color: '#4286f4',
            offset: 2
        };
    }
}
```

{% endtab %}

## Ticks Customization

Ticks are used to specify the interval in the axis. Ticks are of two types, major ticks and minor ticks. The following properties in the [`majorTicks`](../api/linear-gauge/axisModel/#majorticks) and [`minorTicks`](../api/linear-gauge/axisModel/#minorticks) can be used to customize the major ticks and minor ticks respectively.

* [`height`](../api/linear-gauge/tickModel/#height) - To set the length of the major and minor ticks in pixel values.
* [`color`](../api/linear-gauge/tickModel/#color) - To set the color of the major and minor ticks of the Linear Gauge.
* [`width`](../api/linear-gauge/tickModel/#width) - To set the thickness of the major and minor ticks in pixel values.
* [`interval`](../api/linear-gauge/tickModel/#interval) - To set the interval for the major ticks and minor ticks in the Linear Gauge.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis minimum=20 maximum=140 [majorTicks]='major' [minorTicks]='minor'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public major:Object;
    public minor:Object;
    ngOnInit(): void {
        this.major = {
            interval: 20,
            color: "Orange"
        };
        this.minor = {
             interval: 5,
            color: 'red'
        };
    }
}
```

{% endtab %}

### Positioning the ticks

The minor and major ticks can be positioned by using the [`offset`](../api/linear-gauge/tickModel/#offset) and [`position`](../api/linear-gauge/tickModel/#position) properties. The [`offset`](../api/linear-gauge/tickModel/#offset) is used to render the ticks with the specified distance from the axis. By default, the offset value is **0**. The possible values of the [`position`](../api/linear-gauge/tickModel/#position) property are **Inside**, **Outside**, **Cross**, and **Auto**. By default, the ticks will be placed inside the axis.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis minimum=20 maximum=140 [majorTicks]='major' [minorTicks]='minor'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public major:Object;
    public minor:Object;
    ngOnInit(): void {
        this.major = {
            interval: 20,
            color: "Orange",
            position: "Outside"
        };
        this.minor = {
             interval: 5,
            color: 'red',
            position: "Cross"
        };
    }
}
```

{% endtab %}

## Labels Customization

The style of the labels can be customized using the following properties in the [`font`](../api/linear-gauge/labelModel/#font) property in [`labelStyle`](../api/linear-gauge/labelModel).

* [`color`](../api/linear-gauge/font/#color) - To set the color of the axis label.
* [`fontFamily`](../api/linear-gauge/font/#fontfamily) - To set the font family of the axis label.
* [`fontStyle`](../api/linear-gauge/font/#fontstyle) - To set the font style of the axis label.
* [`fontWeight`](../api/linear-gauge/font/#fontweight) - To set the font weight of the axis label.
* [`opacity`](../api/linear-gauge/font/#opacity) - To set the opacity of the axis label.
* [`size`](../api/linear-gauge/font/#size) - To set the size of the axis label.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [labelStyle]='label'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public label:Object;
    ngOnInit(): void {
        this.label =  {
            font: {
              color: 'red'
          }
        };
    }
}
```

{% endtab %}

### Positioning the axis label

Labels can be positioned by using [`offset`](../api/linear-gauge/labelModel/#offset) and [`position`](../api/linear-gauge/labelModel/#position) properties in the [`labelStyle`](../api/linear-gauge/labelModel). The [`offset`](../api/linear-gauge/labelModel/#offset) defines the distance between the labels and ticks. By default, the offset value is **0**. The possible values of the [`position`](../api/linear-gauge/labelModel/#position) property are **Inside**, **Outside**, **Cross**, and **Auto**. By default, the labels will be placed inside the axis.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [labelStyle]='label'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public label:Object;
    ngOnInit(): void {
        this.label =  {
            position: "Cross"
        };
    }
}
```

{% endtab %}

### Customizing the display of the last label

If the last label is not in the visible range, it will be hidden by default. The last label can be made visible by setting the [`showLastLabel`](../api/linear-gauge/axis/#showlastlabel) property as **true** in the [`e-axis`](../api/linear-gauge/axisModel/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [showLastLabel]='isLabel' [maximum]='maximum'>
                <e-pointers>
                    <e-pointer value=20></e-pointer>
                </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public maximum: number;
    public isLabel: boolean;
    ngOnInit(): void {
        this.maximum = 115;
        this.isLabel = true;
    }
}
```

{% endtab %}

<!-- markdownlint-disable MD036 -->

### Label Format

Axis labels in the Linear Gauge control can be formatted using the [`format`](../api/linear-gauge/labelModel/#format) property in the [`labelStyle`](../api/linear-gauge/axis/#labelstyle). It is used to render the axis labels in a certain format or to add a user-defined unit in the label. It works with the help of placeholder like **{value}°C**, where **value** represents the axis value. For example, 20°C.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [labelStyle]='label'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public label:Object;
    ngOnInit(): void {
        this.label =  {
            format: '{value}°C'
        };
    }
}
```

{% endtab %}

### Displaying numeric format in labels

The numeric formats such as currency, percentage, and so on can be displayed in the labels of the Linear Gauge using the [`format`](../api/linear-gauge/labelModel/#format) property in the [`ejs-lineargauge`](../api/linear-gauge/linearGaugeModel/). The following table describes the result of applying some commonly used label formats on numeric values.

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Label Value</b></td>
<td><b>Label Format property value</b></td>
<td><b>Result </b></td>
<td><b>Description </b></td>
</tr>
<tr>
<td>1000</td>
<td>n1</td>
<td>1000.0</td>
<td>The number is rounded to 1 decimal place.</td>
</tr>
<tr>
<td>1000</td>
<td>n2</td>
<td>1000.00</td>
<td>The number is rounded to 2 decimal place.</td>
</tr>
<tr>
<td>1000</td>
<td>n3</td>
<td>1000.000</td>
<td>The number is rounded to 3 decimal place.</td>
</tr>
<tr>
<td>0.01</td>
<td>p1</td>
<td>1.0%</td>
<td>The number is converted to percentage with 1 decimal place.</td>
</tr>
<tr>
<td>0.01</td>
<td>p2</td>
<td>1.00%</td>
<td>The number is converted to percentage with 2 decimal place.</td>
</tr>
<tr>
<td>0.01</td>
<td>p3</td>
<td>1.000%</td>
<td>The number is converted to percentage with 3 decimal place.</td>
</tr>
<tr>
<td>1000</td>
<td>c1</td>
<td>$1,000.0</td>
<td>The currency symbol is appended to number and number is rounded to 1 decimal place.</td>
</tr>
<tr>
<td>1000</td>
<td>c2</td>
<td>$1,000.00</td>
<td>The currency symbol is appended to number and number is rounded to 2 decimal place.</td>
</tr>
</table>

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" format="c">
        <e-axes>
            <e-axis minimum=20 maximum=140>
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

## Orientation

By default, the Linear Gauge is rendered vertically. To change its orientation, the [`orientation`](../api/linear-gauge/linearGaugeModel/#orientation) property must be set to "**Horizontal**".

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" orientation='Horizontal'>
        <e-axes>
            <e-axis minimum=20 maximum=140>
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

## Inverted Axis

The axis of the Linear Gauge component can be inversed by setting the [`isInversed`](../api/linear-gauge/axis/#isinversed) property to **true** in the [`e-axis`](../api/linear-gauge/axisModel/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis isInversed=true>
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

## Opposed Axis

To place an axis opposite from its original position, [`opposedPosition`](../api/linear-gauge/axis/#opposedposition) property in the [`e-axis`](../api/linear-gauge/axisModel/) must be set as **true**.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis opposedPosition=true>
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

## Multiple Axes

Multiple axes can be added to the Linear Gauge by adding multiple [`e-axis`](../api/linear-gauge/axisModel/) in the [`e-axes`](../api/linear-gauge/linearGaugeModel/#axes) and customization can be done with the [`e-axis`](../api/linear-gauge/axisModel/). Each axis can be customized separately as shown in the following example.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [labelStyle]='label1'>
            </e-axis>
            <e-axis opposedPosition=true [labelStyle]='label2'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public label1:Object;
    public label2:Object;
    ngOnInit(): void {
        this.label1 =  {
            format: '{value}°C'
        };
        this.label2 =  {
            format: '{value}°F'
        };
    }
}
```

{% endtab %}
