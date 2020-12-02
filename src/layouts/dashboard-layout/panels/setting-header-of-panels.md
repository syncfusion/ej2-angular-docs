---
title: "Header and Content of Panels"
component: "DashboardLayout"
description: "This section explains how to add header for the panels in Essential JS 2 DashboardLayout component"
---

# Header and content of panels

The dashboard layout component is mostly used to represent the data used for monitoring or managing a process. These data or any HTML template can be placed as the content of a panel using the `content` property. Also, word or phrase that summarize the panel’s content can be added as the header on the top of each panel using the `header` property of the panel.

The following sample demonstrates how to add content for each panel using the header and content properties of the panels.

{% tab template="dashboard-layout/header-and-content-of-panels", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public cellSpacing: number[] = [10, 10];
    public columns: number = 6;
    public panels: any = [{'id':'Panel0', 'sizeX': 1, 'sizeY': 1,'row': 0, 'col': 0, header:'<div>Panel 0</div>', content:'<div class="content">Panel Content<div>'},
    {'id':'Panel1', 'sizeX': 3, 'sizeY': 2,'row': 0, 'col': 1, header:'<div>Panel 1</div>', content:'<div class="content">Panel Content<div>'},
    {'id':'Panel2', 'sizeX': 1, 'sizeY': 3,'row': 0, 'col': 4, header:'<div>Panel 2</div>', content:'<div class="content">Panel Content<div>'},
    {'id':'Panel3', 'sizeX': 1, 'sizeY': 1,'row': 1, 'col': 0, header:'<div>Panel 3</div>', content:'<div class="content">Panel Content<div>'},
    {'id':'Panel4', 'sizeX': 2, 'sizeY': 1,'row': 2, 'col': 0, header:'<div>Panel 4</div>', content:'<div class="content">Panel Content<div>'},
    {'id':'Panel5', 'sizeX': 1, 'sizeY': 1,'row': 2, 'col': 2, header:'<div>Panel 5</div>', content:'<div class="content">Panel Content<div>'},
    {'id':'Panel6','sizeX': 1, 'sizeY': 1,'row': 2, 'col': 3, header:'<div>Panel 6</div>', content:'<div class="content">Panel Content<div>'}
    ]
}
```

{% endtab %}

# Placing components as content of panels

In a dashboard, components like the chart, grids, maps, gauge and more . can be used to present a complex data. Such components can be placed as the panel content by assigning the corresponding component element as the `content` of the panel.

The following sample demonstrates how to add ej2-chart components as the `content` for each panel in the dashboard layout component.

{% tab template="dashboard-layout/components-as-content-of-panels", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public cellSpacing: number[] = [10, 10];
    public chartData: Object[] = [
      { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
      { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
      { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
      { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
      { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
      { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
    ];
    public primaryXAxis: Object = {
        valueType: 'Category'
    }
    public lineData: any[] = [
     { x: 2013, y: 28 }, { x: 2014, y: 25 },{ x: 2015, y: 26 }, { x: 2016, y: 27 },
    { x: 2017, y: 32 }, { x: 2018, y: 35 }
    ];
    public piechart: any[] = [{ x: 'TypeScript', y: 13, text: 'TS 13%' }, { x: 'React', y: 12.5, text: 'Reat 12.5%' },{ x: 'MVC', y: 12, text: 'MVC 12%' },{ x: 'Core', y: 12.5, text: 'Core 12.5%' },{ x: 'Vue', y: 10, text: 'Vue 10%' },{ x: 'Angular', y: 40, text: 'Angular 40%' }];
    public piechart1: any[] = [
     { 'x': 'Chrome', y: 37, text: '37%' },
     { 'x': 'UC Browser', y: 17, text: '17%' },
     { 'x': 'iPhone', y: 19, text: '19%' },
     { 'x': 'Others', y: 4, text: '4%' },
     { 'x': 'Opera', y: 11, text: '11%' },
     { 'x': 'Android', y: 12, text: '12%' }
     ];
     public legendSettings: Object = {
        visible: false
    };
}
```

{% endtab %}