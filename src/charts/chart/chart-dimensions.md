---
title: " Chart Appearance | Angular "

component: "Chart"

description: "We can set chart size manually by using width and height properties. We can set percentage or pixel size values to the chart."
---

# Chart Dimensions

## Size for Container

Chart can render to its container size. You can set the size via inline or CSS as demonstrated below.

```html
    <div style="width:650px; height:350px;">
        <ejs-chart id="chart-container"></ejs-chart>
    </div>
```

```javascript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<div style="width:650px; height:350px;">
        <ejs-chart id="chart-container"></ejs-chart>
    </div>`
})
export class AppComponent {
    constructor(){
        /*
        */
    }
}
```

{% tab template="chart/getting-started/datasource", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<div style="width:650px; height:350px;">
        <ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis'>
            <e-series-collection>
                <e-series [dataSource]='chartData' type='Line' xName='month' yName='sales' name='Sales'></e-series>
            </e-series-collection>
        </ejs-chart>
    </div>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    ngOnInit(): void {
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
    }

}
```

{% endtab %}

## Size for Chart

You can also set size for chart directly through [`width`](../api/chart/#width) and
[`height`](../api/chart/#height) properties.

<!-- markdownlint-disable MD036 -->
**In Pixel**
<!-- markdownlint-disable MD036 -->

You can set the size of chart in pixel as demonstrated below.

{% tab template= "chart/getting-started/datasource", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' width='650' height='350'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='month' yName='sales' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    ngOnInit(): void {
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
    }

}
```

{% endtab %}

**In Percentage**

By setting value in percentage, chart gets its dimension with respect to its container. For example,
when the height is ‘50%’, chart renders to half of the container height.

{% tab template="chart/getting-started/datasource", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-chart id="chart-container" [primaryXAxis]='primaryXAxis' width='80%' height='90%'>
        <e-series-collection>
            <e-series [dataSource]='chartData' type='Line' xName='month' yName='sales' name='Sales'></e-series>
        </e-series-collection>
    </ejs-chart>`
})
export class AppComponent implements OnInit {
    public primaryXAxis: Object;
    public chartData: Object[];
    ngOnInit(): void {
        this.chartData = [
            { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
            { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
            { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
            { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
            { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
            { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
        ];
        this.primaryXAxis = {
            valueType: 'Category'
        };
    }

}
```

{% endtab %}

> Note:  When you do not specify the size, it takes `450px` as the height and window size as its width.