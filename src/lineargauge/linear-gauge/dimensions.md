---
title: "Dimensions in Angular Linear Gauge component | Syncfusion"

component: "Linear Gauge"

description: "Learn here all about the Dimensions of Syncfusion Angular Linear Gauge component and more."
---

# Dimensions in Angular Linear Gauge

<!-- markdownlint-disable MD013 -->

## Size for Linear Gauge

The height and width of the Linear Gauge can be set using the [`width`](https://ej2.syncfusion.com/angular/documentation/api/linear-gauge/#width) and [`height`](https://ej2.syncfusion.com/angular/documentation/api/linear-gauge/#height) properties in [`ejs-lineargauge`](https://ej2.syncfusion.com/angular/documentation/api/linear-gauge/).

### In Pixel

<!-- markdownlint-disable MD036 -->

The size of the Linear Gauge can be set in pixel as demonstrated below.

{% tab template= "linear-gauge/dimensions", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-lineargauge id="gauge-container" width='350px' height='100px'></ejs-lineargauge>`
})
export class AppComponent {
}
```

{% endtab %}

### In Percentage

By setting value in percentage, Linear Gauge receives its dimension matching to its parent. For example, when the height is set as **50%**, Linear Gauge renders to half of the parent height. The Linear Gauge will be responsive when the width is set as **100%**.

{% tab template= "linear-gauge/dimensions", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-lineargauge id="gauge-container" width='100%' height='50%'></ejs-lineargauge>`
})
export class AppComponent {
}
```

{% endtab %}

> Note: When the component's size is not specified, the height will be **450px** and the width will be the same as the parent element's width.
