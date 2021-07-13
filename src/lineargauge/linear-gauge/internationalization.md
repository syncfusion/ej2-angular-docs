---
title: " Internationalization in Angular Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about the Internationalization feature of Syncfusion Angular Linear Gauge component and more."
---

# Internationalization in Angular Linear Gauge

Globalization is the process of designing and developing a component that works in different cultures. Internationalization is used to globalize the number content in Linear Gauge component using [`format`](../api/linear-gauge/label/#format) property in [`ejs-lineargauge`](../api/linear-gauge/linearGaugeModel/).  It has static text on some features such as

* Axis label
* Tooltip

The static text on above features can be changed to any culture such as Arabic, Deutsch and French. To know more about the globalization in Angular components, refer [here](https://ej2.syncfusion.com/angular/documentation/common/internationalization/).

## Numeric Format

The text in axis labels and tooltip can be displayed in the numeric format such as currency, percentage and so on. To know more about the numeric formats in axis labels, refer [here](axis/#displaying-numeric-format-in-labels). In the below example, the axis label is displayed in the currency format.

{% tab template= "linear-gauge/internationalization", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" format="c">
    </ejs-lineargauge>`
})
export class AppComponent {
    ngOnInit(): void {
    }
}
```

{% endtab %}