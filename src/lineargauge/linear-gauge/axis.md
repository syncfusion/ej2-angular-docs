# Axes

<!-- markdownlint-disable MD013 -->

Axes is a collection of linear axis which can be used to indicate the numeric values. Line, ticks, labels, ranges and pointers are the sub elements of an axis.

## Line Customization

The [`line`](../api/linear-gauge/lineModel) property of an axis provides options to customize the [`height`](../api/linear-gauge/lineModel/#height-number), [`width`](../api/linear-gauge/lineModel/#width-number), [`color`](../api/linear-gauge/lineModel/#color-string) and [`offset`](../api/linear-gauge/lineModel/#offset-number) of the axis line.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [line]='Line'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Line:Object;
    ngOnInit(): void {
        this.Line = {
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

You can customize the [`height`](../api/linear-gauge/tickModel/#height-number), [`color`](../api/linear-gauge/tickModel/#color-string) and [`width`](../api/linear-gauge/tickModel/#width-number) of major and minor ticks, by using [`majorTicks`](../api/linear-gauge/tickModel) and [`minorTicks`](../api/linear-gauge/tickModel) property. By default, interval for major ticks will be calculated automatically and also you can customize the interval for major and minor ticks using interval property.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis minimum=20 maximum=140 [majorTicks]='Major' [minorTicks]='Minor'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Major:Object;
    public Minor:Object;
    ngOnInit(): void {
        this.Major = {
            interval: 20
        };
        this.Minor = {
             interval: 5,
            color: 'red'
        };
    }
}
```

{% endtab %}

## Labels Customization

The [`labelStyle`](../api/linear-gauge/labelModel) property of an axis provides options to
customize the [`offset`](../api/linear-gauge/labelModel/#offset-number), [`format`](../api/linear-gauge/labelModel/#format-string), [`color`](../api/linear-gauge/labelModel/#color-string) and [`font`](../api/linear-gauge/labelModel/#font-fontmodel) of the axis labels.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [labelStyle]='Label'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Label:Object;
    ngOnInit(): void {
        this.Label =  {
            font: {
              color: 'red'
          }
        };
    }
}
```

{% endtab %}

<!-- markdownlint-disable MD036 -->

**Customize the display of the last label**

If the last label is not in the visible range, it will be hidden by default. If you want to show the last label, set the [`showLastLabel`](../api/linear-gauge/axis/#showlastlabel) property to **true** in the axes property of linear gauge.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [line]='Line' showLastLabel='true' [maximum]='Maximum'>
                <e-pointers>
                    <e-pointer value=20 [height]='height' [width]='width' color='#757575' offset=30></e-pointer>
                </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Line:Object;
    public height: number;
    public width: number;
    public Maximum: number;
    ngOnInit(): void {
        this.Line =  {
              color: '#9E9E9E'
        };
        this.height = 15;
        this.width= 15;
        this.Maximum = 115;
    }
}
```

{% endtab %}

<!-- markdownlint-disable MD036 -->

**Label Format**

Axis labels can be formatted by using the [`format`](../api/linear-gauge/labelModel/#format-string) property in [`labelStyle`](../api/linear-gauge/axis/#labelstyle-labelmodel) and it supports all the globalized formats.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [labelStyle]='Label'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Label:Object;
    ngOnInit(): void {
        this.Label =  {
            format: 'c'
        };
    }
}
```

{% endtab %}

The following table describes the result of applying some commonly used label formats on numeric values.

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
<td>The Number is rounded to 1 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>n2</td>
<td>1000.00</td>
<td>The Number is rounded to 2 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>n3</td>
<td>1000.000</td>
<td>The Number is rounded to 3 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p1</td>
<td>1.0%</td>
<td>The Number is converted to percentage with 1 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p2</td>
<td>1.00%</td>
<td>The Number is converted to percentage with 2 decimal place</td>
</tr>
<tr>
<td>0.01</td>
<td>p3</td>
<td>1.000%</td>
<td>The Number is converted to percentage with 3 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>c1</td>
<td>$1,000.0</td>
<td>The Currency symbol is appended to number and number is rounded to 1 decimal place</td>
</tr>
<tr>
<td>1000</td>
<td>c2</td>
<td>$1,000.00</td>
<td>The Currency symbol is appended to number and number is rounded to 2 decimal place</td>
</tr>
</table>

**Custom Label Format**

Axis also supports custom label format using placeholder like {value}°C, in which the value represents the axis label e.g. 20°C.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis minimum=20 maximum=140 [labelStyle]='Label'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Label:Object;
    ngOnInit(): void {
        this.Label =  {
            format: '{value}°C'
        };
    }
}
```

{% endtab %}

## Orientation

By default, the linear gauge is rendered vertically. To change its orientation, the [`orientation`](../api/linear-gauge/linearGaugeModel/#orientation) property must be set to **"Horizontal"**

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" [axes]='Axes' [orientation]='Orientation'>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Orientation: string
    public Axes: Object[] = [{
        minimum: 20,
        maximum: 140
    }];
    ngOnInit(): void {
        this.Orientation = "Horizontal";
    }
}
```

{% endtab %}

## Inverted Axes

[`isInversed`](../api/linear-gauge/axis/#isinversed-boolean) property is used to choose the rendering of axis either bottom to top or top to bottom direction.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [line]='Line' [isInversed]='Direction'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Direction:boolean;
    ngOnInit(): void {
        this.Direction = true;
    }
}
```

{% endtab %}

## Opposed Axes

To place an axis opposite from its original position, set [`opposedPosition`](../api/linear-gauge/axis/#opposedposition-boolean) property as true in the axis.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [opposedPosition]='position'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public position:boolean;
    ngOnInit(): void {
       this.position = true;
    }
}
```

{% endtab %}

## Multiple Axes

You can render any number of axis for a linear gauge by using array of axis objects.
Each axis will have its own ranges, pointers, annotations and customization options.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container">
        <e-axes>
            <e-axis [labelStyle]='Label1'>
            </e-axis>
            <e-axis opposedPosition=true [labelStyle]='Label2'>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Label1:Object;
    public Label2:Object;
    ngOnInit(): void {
        this.Label1 =  {
            format: '{value}°C'
        };
        this.Label2 =  {
            format: '{value}°F'
        };
    }
}
```

{% endtab %}