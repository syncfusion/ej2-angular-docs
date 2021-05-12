---
title: " StockChart Internationalization | Angular "

component: "StockChart"

description: "StockChart provides the support for internationalization for axis label, tooltip and crosshair elements."
---

# Internationalization

Chart provide supports for internationalization for below chart elements.

* Axis label.
* Tooltip.
* Crosshair

For more information about number and date formatter you can refer
[`internationalization`](https://ej2.syncfusion.com/angular/documentation/stock-chart/internationalization/?no-cache=1).

<!-- markdownlint-disable MD036 -->
**Globalization**

Globalization is the process of designing and developing an component that works in different
cultures/locales.  Internationalization  library is used to globalize number, date, time values in
Chart component using  `labelFormat` property in axis.

**Numeric Format**

In the below example axis labels, tooltip and crosshair labels are globalized to EUR.

{% tab template="stock-chart/internationalization", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';
import { setCurrencyCode, L10n, setCulture  } from '@syncfusion/ej2-base';
setCurrencyCode("EUR");

@Component({
    selector: 'app-container',
    template:
        `<ejs-stockchart id='chart-container' [primaryXAxis]='primaryXAxis' style="display:block;"
        [primaryYAxis]='primaryYAxis' [crosshair]='crosshair' (tooltipRender)='tooltipRender($event)' [tooltip]='tooltip'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='data1' type='Candle' xName='x' yName='high' high='high' low='low'>
            </e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})

export class AppComponent implements OnInit {

    public data1: Object[] = chartData;

    public primaryXAxis: Object = { majorGridLines: { color: 'transparent' }, crosshairTooltip: { enable: true } };

    public primaryYAxis: Object = {
        lineStyle: { color: 'transparent' },
        majorTickLines: { color: 'transparent', width: 0 },
        labelFormat: 'c',
        crosshairTooltip: { enable: true }
    };
    public crosshair: Object = {
        enable: true
    };
    public tooltipRender(args: ITooltipRenderEventArgs): void {
        if (args.text.split('<br/>')[4]) {
        let target: number = parseInt(args.text.split('<br/>')[4].split('<b>')[1].split('</b>')[0], 10);
        let value: string = (target / 100000000).toFixed(1) + 'B';
        args.text = args.text.replace(args.text.split('<br/>')[4].split('<b>')[1].split('</b>')[0], value);
        }
    };

    public tooltip: object = { enable: true };
    constructor() {
        //code
    }
}
```

{% endtab %}