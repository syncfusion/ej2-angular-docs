
# Linear Gauge Dimensions

<!-- markdownlint-disable MD013 -->

## Size for Container

Linear gauge can render to its container size. You can set the size via inline or CSS as demonstrated below.

{% tab template= "linear-gauge/dimensions", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-lineargauge id="gauge-container" width='650' height='350'></ejs-lineargauge>`
})
export class AppComponent {
    constructor(){
        /*
        */
    }
}
```

{% endtab %}

## Size for gauge

You can also set size for linear gauge directly through [`width`](../api/linear-gauge/linearGaugeModel/#width-string) and [`height`](../api/linear-gauge/linearGaugeModel/#height-string) properties.

<!-- markdownlint-disable MD036 -->
**In Pixel**
<!-- markdownlint-disable MD036 -->

You can set the size of linear gauge in pixel as demonstrated below.

{% tab template= "linear-gauge/dimensions", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-lineargauge id="gauge-container" width='650px' height='350px'></ejs-lineargauge>`
})
export class AppComponent {
    constructor(){
        /*
        */
    }
}
```

{% endtab %}

**In Percentage**

By setting value in percentage, linear gauge gets its dimension with respect to its container. For example, when the height is ‘50%’, linear gauge renders to half of the container height.

{% tab template= "linear-gauge/dimensions", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-lineargauge id="gauge-container" width='100%' height='50%'></ejs-lineargauge>`
})
export class AppComponent {
    constructor(){
        /*
        */
    }
}
```

{% endtab %}

> Note:  When you do not specify the size, it takes `450px` as the height and window size as its width.