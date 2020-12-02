# Appearance

<!-- markdownlint-disable MD013 -->

## Gauge Area Customization

<!-- markdownlint-disable MD036 -->

**Customize the Linear Gauge Background**

Using [`background`](../api/linear-gauge/linearGaugeModel/#background-string) and
[`border`](../api/linear-gauge/linearGaugeModel/#border-bordermodel) properties, you can change the background color and border of the linear gauge.

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" background='skyblue' [border]='Border'>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Border:Object;
    ngOnInit(): void {
        this.Border = { color: "#FF0000", width: 2 };
    }
}
```

{% endtab %}

**Gauge Margin**

You can set margin for the lineargauge through [`margin`](../api/linear-gauge/marginModel) property.

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" background='skyblue' [border]='Border' [margin]='Margin'>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Border:Object;
    public margin:Object;
    ngOnInit(): void {
        this.Border = { color: "#FF0000", width: 2 };
        this.Margin = { left: 40, right: 40, top: 40, bottom: 40 };
    }
}
```

{% endtab %}

## Gauge Title

You can give the title using [`title`](../api/linear-gauge/linearGaugeModel/#title-string) property to show the information about the linear gauge. Its appearance can be customized by using the [`titleStyle`](../api/linear-gauge/linearGaugeModel/#titlestyle-fontmodel) property.

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" title='Speedometer' [titleStyle]='TitleStyle'>
    </ejs-lineargauge>`
})
export class AppComponent {
    public Border:Object;
    public margin:Object;
    ngOnInit(): void {
        this.TitleStyle = {
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

## Gauge Container

The area used to render the ranges and pointers at the center position of the gauge is called [`container`](../api/linear-gauge/containerModel). It can be customized by using [`type`](../api/linear-gauge/containerModel/#type-string), [`offset`](../api/linear-gauge/containerModel/#offset-number), [`width`](../api/linear-gauge/containerModel/#width-number), [`height`](../api/linear-gauge/containerModel/#height-number) and [`backgroundColor`](../api/linear-gauge/containerModel/#backgroundcolor-string) properties in [`container`](../api/linear-gauge/containerModel). It is of three types namely,

* Normal
* Rounded Rectangle
* Thermometer

**Normal**

The normal type will render the container as rectangle and this is the default container type.

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-lineargauge id="gauge-container" [container]='Container'></ejs-lineargauge>`
})

export class AppComponent implements OnInit {
    public Container: string;
    ngOnInit(): void {
        this.Container = {
        height:300,
        width:30
      };
}
```

{% endtab %}

**Rounded Rectangle**

The rounded rectangle type will render the container as rectangle with rounded corners.

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-lineargauge id="gauge-container" [container]='Container'></ejs-lineargauge>`
})

export class AppComponent implements OnInit {
    public Container: string;
    ngOnInit(): void {
        this.Container = {
        height:300,
        width:30,
        type:'RoundedRectangle'
      };
}
```

{% endtab %}

**Thermometer**

This type is used to render the container similar to the thermometer appearance.

{% tab template= "linear-gauge/appearance", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-lineargauge id="gauge-container" [container]='Container'></ejs-lineargauge>`
})

export class AppComponent implements OnInit {
    public Container: string;
    ngOnInit(): void {
        this.Container = {
        height:300,
        width:30,
        type:'Thermometer'
      };
}
```

{% endtab %}