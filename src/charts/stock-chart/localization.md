---
title: " StockChart Localization | Angular "

component: "StockChart"

description: "Localization library allows to localize the default text content of StockChart."
---

# Localization

Localization library allows to localize the default text content of StockChart. In stock chart component,
it has the static text on some features(like zooming toolbars)
and this can be changed to any other culture(Arabic, Deutsch, French, etc) by defining the locale value and translation object.

<!-- markdownlint-disable MD033 -->

<table>
<tr>
<td><b>Locale key words</b></td>
<td><b>Text to display</b></td>
</tr>
<tr>
<td>Zoom</td>
<td>Zoom</td>
</tr>
<tr>
<td>ZoomIn</td>
<td>ZoomIn</td>
</tr>
<tr>
<td>ZoomOut</td>
<td>ZoomOut</td>
</tr>
<tr>
<td>Reset</td>
<td>Reset</td>
</tr>
<tr>
<td>Pan</td>
<td>Pan</td>
</tr>
<tr>
<td>ResetZoom</td>
<td>Reset Zoom</td>
</tr>
</table>

To load translation object in an application use load function of `L10n` class.

For more information about localization, refer this
[`localization`](https://ej2.syncfusion.com/angular/documentation/common/localization/)

{% tab template="stock-chart/localization", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, OnInit } from '@angular/core';
import { chartData } from 'datasource.ts';
import { L10n, setCulture  } from '@syncfusion/ej2-base';
setCulture('ar-AR');
L10n.load({
    'ar-AR': {
        'chart': {
            ZoomIn: 'تكبير',
            ZoomOut: 'تصغير',
            Zoom: 'زوم',
            Pan: 'مقلاة',
            Reset: 'إعادة تعيين',
            ResetZoom: ' زومإعادة تعيين'
        },
    }
});

@Component({
    selector: 'app-container',
    template:
        `<ejs-stockchart id='chart-container' [primaryXAxis]='primaryXAxis' style="display:block;"
        [primaryYAxis]='primaryYAxis' [crosshair]='crosshair' (tooltipRender)='tooltipRender($event)' [tooltip]='tooltip'
        [zoomSettings]="zoomSettings" [locale]='ar-AR'>
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
        crosshairTooltip: { enable: true }
    };
    public zoomSettings: Object = {
        enableMouseWheelZooming: true,
        mode: 'XY'
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
