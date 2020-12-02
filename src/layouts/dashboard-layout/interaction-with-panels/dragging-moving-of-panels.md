---
title: "Customizing the dragging handler"
component: "DashboardLayout"
description: "This section explains how to adjust the panels within the layout in Essential JS 2 DashboardLayout component"
---

# Dragging of panels

The Dashboard Layout component is provided with dragging functionality to drag and reorder the panels within the layout. While dragging a panel, a holder will be highlighted below the panel indicating the panel placement on panel drop. This helps the user to decide whether to place the panel in the current position or revert to previous position without disturbing the layout.

If one or more panels collide while dragging, then the colliding panels will be pushed towards the left or right or top or bottom direction where an adaptive space for the collided panel is available. The position changes of these collided panels will be updated dynamically during dragging of a panel, so the user can conclude whether to place the panel in the current position or not.

While dragging a panel in Dashboard layout the following dragging events will be triggered,
* [dragStart](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#dragstart) - Triggers when panel drag starts
* [drag](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#drag) - Triggers when panel is being dragged
* [dragStop](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#dragstop) - Triggers when panel drag stops

The following sample demonstrates dragging and pushing of panels. For example, while dragging the panel 0 over panel 1, these panels get collided and push the panel 1 towards the feasible direction, so that, the panel 0 gets placed in the panel 1 position.

{% tab template="dashboard-layout/dragging-of-panels", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

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
    public columns: number = 5;
    public panels: any = [{'sizeX': 1, 'sizeY': 1, 'row': 0, 'col': 0, content:'<div class="content">0</div>'},
    {'sizeX': 3, 'sizeY': 2, 'row': 0, 'col': 1, content:'<div class="content">1</div>'},
    {'sizeX': 1, 'sizeY': 3, 'row': 0, 'col': 4, content:'<div class="content">2</div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 1, 'col': 0, content:'<div class="content">3</div>'},
    {'sizeX': 2, 'sizeY': 1, 'row': 2, 'col': 0, content:'<div class="content">4</div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 2, 'col': 2, content:'<div class="content">5</div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 2, 'col': 3, content:'<div class="content">6</div>'},
    ];

    //Dashboard Layout's drag start event function
    onDragStart(args: any) {
        console.log("Drag start");
    }
    //Dashboard Layout's drag event function
    onDrag(args: any) {
        console.log("Dragging");
    }
    //Dashboard Layout's dragstop event function
    onDragStop(args: any) {
        console.log("Drag stop");
    }

}
```

{% endtab %}

## Customizing the dragging handler

Initially, the complete panel will act as the handler for dragging the panel such that the dragging action occurs on clicking anywhere over a panel. However, this dragging handler for the panels can be customized using the `draggableHandle` property to restrict the dragging action within a particular element in the panel.

The following sample demonstrates customizing the dragging handler of the panels where the dragging action of panel occurs only with the header of the panel.

{% tab template="dashboard-layout/customizing-the-dragging-handler", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component,ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public cellSpacing: number[] = [10, 10];
    public draggableHandle: string = '.e-panel-header';
    public primaryXAxis: Object = { valueType: 'Category' };
    public chartData: any[] = [
        { month: 'Jan', sales: 35 }, { month: 'Feb', sales: 28 },
        { month: 'Mar', sales: 34 }, { month: 'Apr', sales: 32 },
        { month: 'May', sales: 40 }, { month: 'Jun', sales: 32 },
        { month: 'Jul', sales: 35 }, { month: 'Aug', sales: 55 },
        { month: 'Sep', sales: 38 }, { month: 'Oct', sales: 30 },
        { month: 'Nov', sales: 25 }, { month: 'Dec', sales: 32 }
    ];
    public lineData: any[] = [
        { x: 2013, y: 28 }, { x: 2014, y: 25 }, { x: 2015, y: 26 }, { x: 2016, y: 27 },
        { x: 2017, y: 32 }, { x: 2018, y: 35 },
    ];
    public piechart: any[] = [
        { x: 'TypeScript', y: 13, text: 'TS 13%' },
        { x: 'React', y: 12.5, text: 'Reat 12.5%' },
        { x: 'MVC', y: 12, text: 'MVC 12%' },
        { x: 'Core', y: 12.5, text: 'Core 12.5%' },
        { x: 'Vue', y: 10, text: 'Vue 10%' },
        { x: 'Angular', y: 40, text: 'Angular 40%' }
    ];
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

## Disable dragging of panels

By default, the dragging of panels is enabled in Dashboard Layout. It can also be disabled with the help of [allowDragging](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#allowdragging) API. Setting [allowDragging](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#allowdragging) to false disables the dragging functionality in Dashboard Layout.

The following sample demonstrates Dashboard Layout with dragging support disabled.

{% tab template="dashboard-layout/disable-dragging", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

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
    public columns: number = 5;
    public allowDragging: boolean = false;
    public panels: any = [
    {'sizeX': 1, 'sizeY': 1, 'row': 0, 'col': 0, content:'<div class="content">0</div>'},
    {'sizeX': 3, 'sizeY': 2, 'row': 0, 'col': 1, content:'<div class="content">1</div>'},
    {'sizeX': 1, 'sizeY': 3, 'row': 0, 'col': 4, content:'<div class="content">2</div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 1, 'col': 0, content:'<div class="content">3</div>'},
    {'sizeX': 2, 'sizeY': 1, 'row': 2, 'col': 0, content:'<div class="content">4</div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 2, 'col': 2, content:'<div class="content">5</div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 2, 'col': 3, content:'<div class="content">6</div>'},
    ];

}
```

{% endtab %}