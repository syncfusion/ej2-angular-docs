# Appearance

## Gauge Title

Circular gauge can be given a title by using
[`title`](../api/circular-gauge/#title-string) property, to show the information about the gauge.
Title can be customized by using [`titleStyle`](../api/circular-gauge/#titlestyle-fontmodel)
property in gauge.

{% tab template="circulargauge/gauge-appearance", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" title="Speedometer" [titleStyle]="titleStyle">
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public titleStyle: object;
    ngOnInit(): void {
        // Initialize objects.
        this.titleStyle = {
            color: '#27d5ff'
        };
    }
}

```

{% endtab %}

## Gauge Position

<!-- markdownlint-disable MD036 -->

Gauge can be positioned anywhere in the container with the help of
[`centerX`](../api/circular-gauge/#centerx-string) and
[`centerY`](../api/circular-gauge/#centery-string)
property and it accepts values either in percentage or in pixels.
The default value of the [`centerX`](../api/circular-gauge/#centerx-string) and
[`centerY`](../api/circular-gauge/#centery-string) property is 50%, which means gauge will get rendered to the centre of the container.

**In Pixel**

You can set the mid point of the gauge in pixel as demonstrated below,

{% tab template="circulargauge/gauge-appearance", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" centerX='20' centerY='20'>
        <e-axes>
            <e-axis [lineStyle]="lineStyle" startAngle=90 endAngle=180>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public lineStyle: object;
    ngOnInit(): void {
        // Initialize objects.
        this.lineStyle = {
            width: 2,
            color: '#F8F8F8'
        };
    }
}

```

{% endtab %}
<!-- markdownlint-disable MD036 -->

**In Percentage**

By setting the value in percentage, gauge gets its mid point with respect to its plot area.
For example, when the [`centerX`](../api/circular-gauge/#centerx-string)
value as '0%' and [`centerY`](../api/circular-gauge/#centery-string) value is ‘50%’,
gauge will get positioned at the top left corner of the plot area.

{% tab template="circulargauge/gauge-appearance", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" centerX='10%' centerY='50%'>
        <e-axes>
            <e-axis [lineStyle]="lineStyle" startAngle=0 endAngle=180>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public lineStyle: object;
    ngOnInit(): void {
        // Initialize objects.
        this.lineStyle = {
            width: 2,
            color: '#F8F8F8'
        };
    }
}

```

{% endtab %}
<!-- markdownlint-disable MD036 -->

## Area Customization

**Customize the gauge background**

Using [`background`](../api/circular-gauge/#background-string) and
[`border`](../api/circular-gauge/#border-bordermodel) properties, you can change the background color and border of the circular gauge.

{% tab template="circulargauge/gauge-appearance", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" background='skyblue' [border]='gaugeBorder'>
        <e-axes>
            <e-axis [lineStyle]="lineStyle" [majorTicks]="majorTicks" [minorTicks]="minorTicks" startAngle=230 endAngle=130 radius="90%" maximum=120>
                <e-pointers>
                    <e-pointer value=60 radius="60%"></e-pointer>
                </e-pointers>
                <e-ranges>
                    <e-range start=0 end=70 radius="110%" strokeWidth=10></e-range>
                    <e-range start=70 end=110 radius="110%" strokeWidth=10></e-range>
                    <e-range start=110 end=120 radius="110%" strokeWidth=10></e-range>
                </e-ranges>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public gaugeBorder: object;
    public majorTicks: object;
    public minorTicks: object;
    public lineStyle: object;
    ngOnInit(): void {
        // Initialize objects.
        this.gaugeBorder = { color: "#FF0000", width: 2 };
        this.majorTicks = { width: 1, color: '#8c8c8c' };
        this.minorTicks = { width: 1, color: '#8c8c8c' };
        this.lineStyle = { width: 2};
    }
}

```

{% endtab %}

**Gauge Margin**

You can set margin for gauge from its container through
[`margin`](../api/circular-gauge/#margin-marginmodel) property.

{% tab template="circulargauge/gauge-appearance", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" background='skyblue' [margin]="margin" [border]='gaugeBorder'>
        <e-axes>
            <e-axis [lineStyle]="lineStyle" [majorTicks]="majorTicks" [minorTicks]="minorTicks" startAngle=230 endAngle=130 radius="90%" maximum=120>
                <e-pointers>
                    <e-pointer value=60 radius="60%"></e-pointer>
                </e-pointers>
                <e-ranges>
                    <e-range start=0 end=70 radius="110%" strokeWidth=10></e-range>
                    <e-range start=70 end=110 radius="110%" strokeWidth=10></e-range>
                    <e-range start=110 end=120 radius="110%" strokeWidth=10></e-range>
                </e-ranges>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public gaugeBorder: object;
    public majorTicks: object;
    public minorTicks: object;
    public lineStyle: object;
    public gaugeMargin: object;
    ngOnInit(): void {
        // Initialize objects.
        this.gaugeBorder = { color: "#FF0000", width: 2 };
        this.majorTicks = { width: 1, color: '#8c8c8c' };
        this.minorTicks = { width: 1, color: '#8c8c8c' };
        this.lineStyle = { width: 2 };
        this.margin = { left: 40, right: 40, top: 40, bottom: 40 };
    }

}

```

{% endtab %}

## Radius calculation based on angles

Render semi or quarter circular gauges by modifying the start and end angles. By enabling the radius based on angle option, the radius of circular gauge will be calculated based on the start and end angles to avoid excess white space.

{% tab template="circulargauge/gauge-appearance", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" centerX='10%' centerY='50%'>
        <e-axes>
            <e-axis [lineStyle]="lineStyle" startAngle=270 endAngle=90>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public lineStyle: object;
    ngOnInit(): void {
        // Initialize objects.
        this.lineStyle = {
            width: 2,
            color: '#F8F8F8'
        };
    }
}

```

{% endtab %}