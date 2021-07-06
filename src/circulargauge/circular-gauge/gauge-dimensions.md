
# Circular Gauge Dimensions

## Size for Container

You can set width and height to the element of the container. It determines the gauge size. Also, you can set the size via inline or CSS as demonstrated below.

```html
    <div id='container'>
        <div id='circular-container' style="width:650px; height:350px;"></div>
    </div>
```

{% tab template="circulargauge/gauge-dimensions", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container">
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

## Size for Circular Gauge

<!-- markdownlint-disable MD036 -->

You can also set size for the gauge directly through [`width`](../api/circular-gauge/#width-string)
and [`height`](../api/circular-gauge/#height-string) properties.

**In Pixel**

You can set the size of the gauge in pixel as demonstrated below.

{% tab template="circulargauge/gauge-dimensions", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" width="650" height="350">
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
        // Initialize objects.
    }
}

```

{% endtab %}

**In Percentage**

By setting value in percentage, gauge gets its dimension with respect to its container. For example, when
the height is ‘50%’, gauge renders to half of the container height.

{% tab template="circulargauge/gauge-dimensions", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" width="80%" height="50%">
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
        // Initialize objects.
    }
}

```

{% endtab %}

>Note: When you do not specify the size, it takes `450px` as the height and window size as its width.