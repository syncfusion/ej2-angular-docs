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
import { Component, OnInit } from '@angular/core';
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
    `<ejs-stockchart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis'
        [crosshair]='crosshair' [zoomSettings]="zoomSettings" locale='ar-AR'>
        <e-stockchart-series-collection>
            <e-stockchart-series [dataSource]='chartData' type='Spline' xName='x' yName='open' [marker]='marker'></e-stockchart-series>
        </e-stockchart-series-collection>
    </ejs-stockchart>`
})

export class AppComponent implements OnInit {
  public chartData: Object[];
  public primaryXAxis: Object;
  public primaryYAxis: Object;
  public crosshair: Object;
  public zoomSettings: Object;
  public marker: Object;
  ngOnInit(): void {
    this.chartData = chartData;
    this.primaryXAxis = {
      valueType: 'DateTime',
      majorGridLines: { color: 'transparent' }, crosshairTooltip: { enable: true }
    };
    this.primaryYAxis = {
      lineStyle: { color: 'transparent' },
      majorTickLines: { color: 'transparent', width: 0 },
      crosshairTooltip: { enable: true }
    };
    this.zoomSettings = {
      enableMouseWheelZooming: true,
      mode: 'XY'
    };
    this.crosshair = { enable: true };
    this.marker = { visible: true, width: 10, height: 10 };
  }
}
```

{% endtab %}
