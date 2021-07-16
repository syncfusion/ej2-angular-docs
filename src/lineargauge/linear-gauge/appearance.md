---
title: " Appearance in Angular Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about the Appearance of Syncfusion Angular Linear Gauge component and more."
---

# Appearance in Angular Linear Gauge

<!-- markdownlint-disable MD013 -->

## Customizing the Linear Gauge area

The following properties are available in the [`ejs-lineargauge`](../api/linear-gauge/) to customize the Linear Gauge area.

* [`background`](api/linear-gauge/#background) - Applies the background color for the Linear gauge.
* [`border`](api/linear-gauge/#border) - To customize the color and width of the border in Linear Gauge.
* [`margin`](api/linear-gauge/#margin) - To customize the margins of the Linear Gauge.

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" background='skyblue' [border]='border' [margin]='margin'>
    </ejs-lineargauge>`
})
export class AppComponent {
    public border: Object;
    public margin: Object;
    ngOnInit(): void {
      this.border = { color: "#FF0000", width: 2 };
      this.margin = { left: 20, top: 20, right: 20, bottom: 20}
    }
}
```

{% endtab %}

## Setting up the Linear Gauge title

The title for the Linear Gauge can be set using [`title`](api/linear-gauge/#title) property in [`ejs-lineargauge`](../api/linear-gauge). Its appearance can be customized using the [`titleStyle`](api/linear-gauge/#titlestyle) with the below properties.

* [`color`](../api/linear-gauge/labelModel/#color) - Specifies the text color of the title.
* [`fontFamily`](../api/linear-gauge/font/#fontfamily) - Specifies the font family of the title.
* [`fontStyle`](../api/linear-gauge/font/#fontstyle) - Specifies the font style of the title.
* [`fontWeight`](../api/linear-gauge/font/#fontweight) - Specifies the font weight of the title.
* [`opacity`](../api/linear-gauge/font/#opacity) - Specifies the opacity of the title.
* [`size`](../api/linear-gauge/font/#size) - Specifies the font size of the title.

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" title='Speedometer' [titleStyle]='titleStyle'>
    </ejs-lineargauge>`
})
export class AppComponent {
    public titleStyle: Object;
    ngOnInit(): void {
      this.titleStyle = {
        fontFamily: "Arial",
        fontStyle: 'italic',
        fontWeight: 'regular',
        color: "#E27F2D",
        size: '23px'
      };
    }
}
```

{% endtab %}

## Customizing the Linear Gauge container

The area used to render the ranges and pointers at the center position of the gauge is called container. It is of three types namely,

* Normal
* Rounded Rectangle
* Thermometer

The  type of the container can be modified by using the [`type`](../api/linear-gauge/containerModel/#type) property in [`container`](../api/linear-gauge/containerModel). The container can be customized by using the following properties in [`container`](../api/linear-gauge/containerModel).

* [`offset`](../api/linear-gauge/containerModel/#offset) - To place the container with the specified distance from the axis of the Linear Gauge.
* [`width`](../api/linear-gauge/containerModel/#width) - To set the thickness of the container.
* [`height`](../api/linear-gauge/containerModel/#height) - To set the length of the container.
* [`backgroundColor`](../api/linear-gauge/containerModel/#backgroundcolor) - To set the background color of the container.
* [`border`](../api/linear-gauge/container/#border) - To set the color and width for the border of the container.

### Normal

The "**Normal**" type will render the container as a rectangle and this is the default container type.

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" [container]='container'>
      <e-axes>
        <e-axis>
          <e-pointers>
            <e-pointer type="Bar" value=50>
            </e-pointer>
          </e-pointers>
        </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})

export class AppComponent implements OnInit {
    public container: Object;
    ngOnInit(): void {
        this.container = {
          width:30
      };
    }
}
```

{% endtab %}

### Rounded Rectangle

The "**RoundedRectangle**" type will render the container as a rectangle with rounded corner radius. The rounded corner radius of the container can be customized using the [`roundedCornerRadius`](../api/linear-gauge/container/#roundedcornerradius) property in [`container`](../api/linear-gauge/containerModel).

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" [container]='container'>
      <e-axes>
        <e-axis>
          <e-pointers>
            <e-pointer type="Bar" value=50>
            </e-pointer>
          </e-pointers>
        </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})

export class AppComponent implements OnInit {
    public container: string;
    ngOnInit(): void {
        this.container = {
            width:30,
            type: "RoundedRectangle"
        };
    }
}
```

{% endtab %}

### Thermometer

The "**Thermometer**" type will render the container similar to the appearance of thermometer.

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
     <ejs-lineargauge id="gauge-container" [container]='container'>
      <e-axes>
        <e-axis>
          <e-pointers>
            <e-pointer type="Bar" value=50>
            </e-pointer>
          </e-pointers>
        </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})

export class AppComponent implements OnInit {
    public container: Object;
    ngOnInit(): void {
      this.container = {
        width:30,
        type: "Thermometer"
      };
    }
}
```

{% endtab %}

## Fitting the Linear Gauge to the control

The Linear Gauge component is rendered with margin by default. To remove the margin around the Linear Gauge, the [`allowMargin`](api/linear-gauge/#allowmargin) property in [`ejs-lineargauge`](../api/linear-gauge) is set as "**false**".

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
     <ejs-lineargauge id="gauge-container" [margin]='margin' [allowMargin]='isMargin'  orientation="Horizontal" background="skyblue" [border]='border'>
      <e-axes>
        <e-axis>
          <e-pointers>
            <e-pointer type="Bar" value=50>
            </e-pointer>
          </e-pointers>
        </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})

export class AppComponent implements OnInit {
    public border: Object;
    public margin: Object;
    public isMargin: boolean;
    ngOnInit(): void {
      this.isMargin = false;
      this.margin = {
        left: 0,
        right: 0,
        top: 0,
        bottom: 0
      },
      this.border = {
        width:3,
        color: "red"
      };
    }
}
```

{% endtab %}

> Note: To use this feature, set the [`allowMargin`](api/linear-gauge/#allowmargin) property to "**false**", the [`width`](api/linear-gauge/#width) property to "**100%**" and the properties of [`margin`](api/linear-gauge/#margin) to "**0**".