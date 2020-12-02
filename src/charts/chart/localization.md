---
title: " Chart Localization | Angular "

component: "Chart"

description: "Localization library allows to localize the default text content of Chart."
---

# Localization

Localization library allows to localize the default text content of Chart. In Chart component,
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

To load translation object in an application use load function of L10n class.

For more information about localization, refer this
[`localization`](http://ej2.syncfusion.com/angular/documentation/base/localization.html)

{% tab template="chart/user-interaction/zoom", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { L10n } from '@syncfusion/ej2-base';

L10n.load({
    'ar-AR': {
        'chart': {
            ZoomIn: 'تكبير',
            ZoomOut: 'تصغير',
            Zoom: 'زوم',
            Pan: 'مقلاة',
            Reset: 'إعادة تعيين',
        },
    }
});

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'[primaryYAxis]='primaryYAxis' [title]='title' locale='ar-AR' [zoomSettings]='zoom'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y' name='Product X' ></e-series>
            <e-series [dataSource]='chartData' type='Area' xName='x' yName='y1' name='Product Y'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    public title: string;
    public marker: Object;
    public primaryYAxis: Object;
    public zoom: Object;
    ngOnInit(): void {
        this.chartData = [
                { x: 1900, y: 4, y1: 2.6, y2: 2.8 }, { x: 1920, y: 3.0, y1: 2.8, y2: 2.5 },
                { x: 1940, y: 3.8, y1: 2.6, y2: 2.8 }, { x: 1960, y: 3.4, y1: 3, y2: 3.2 },
                { x: 1980, y: 3.2, y1: 3.6, y2: 2.9 }, { x: 2000, y: 3.9, y1: 3, y2: 2 }
        ];
        this.primaryXAxis = {
            title: 'Year',
            edgeLabelPlacement: 'Shift'
        };
        this.primaryYAxis = {
           title: 'Sales Amount in Millions',
        };
        this.zoom = {
            enableMouseWheelZooming: true,
            enableDeferredZooming: true,
            enablePinchZooming: true,
            enableSelectionZooming: true
        }
        this.title = 'Average Sales Comparison';
    }

}
```

{% endtab %}