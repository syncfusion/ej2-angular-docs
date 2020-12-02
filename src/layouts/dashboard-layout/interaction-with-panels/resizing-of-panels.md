---
title: "Resizing panels"
component: "DashboardLayout"
description: "This section explains how to enable resizing and the dynamic resizing of panels within the layout in Essential JS 2 DashboardLayout component"
---

# Resizing panels

The DashboardLayout component is also provided with the resizing functionality that can be enabled using the `allowResize` property of the component. This functionality allows you to resize the panels dynamically using the resizing handlers which controls the resizing of panels in various directions.

Initially, the panels can be resized only in south-east direction. However, panels can also be resized in east, west, north, south and south-west directions also by defining the required directions with the `resizableHandles` property.

On resizing a panel in Dashboard layout the following events will be triggered,
* [resizeStart](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#resizestart) - Triggers when panel resize starts
* [resize](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#resize) - Triggers when panel is being resized
* [resizeStop](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#resizestop) - Triggers when panel resize stops

The following sample demonstrates how to enable and disable the resizing of panels in the DashboardLayout component in different directions.

{% tab template="dashboard-layout/resizing-of-panels", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

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
    public allowResizing: boolean = true;
    public resizableHandles: string[] = ['e-south-east','e-east','e-west','e-north','e-south'];
    public panels: any = [{ "sizeX": 1, "sizeY": 1, "row": 0, "col": 0, content: '<div class="content">0</div>' },
    { "sizeX": 3, "sizeY": 2, "row": 0, "col": 1, content: '<div class="content">1</div>' },
    { "sizeX": 1, "sizeY": 3, "row": 0, "col": 4, content: '<div class="content">2</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 1, "col": 0, content: '<div class="content">3</div>' },
    { "sizeX": 2, "sizeY": 1, "row": 2, "col": 0, content: '<div class="content">4</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 2, content: '<div class="content">5</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 3, content: '<div class="content">6</div>' }
    ];

    //Dashboard Layout's resizestart event function
    onResizeStart(args: any) {
        console.log("Resize start");
    }

    //Dashboard Layout's resize event function
    onResize(args: any) {
        console.log("Resizing");
    }

    //Dashboard Layout's resizestop event function
    onResizeStop(args: any) {
        console.log("Resize stop");
    }

}
```

{% endtab %}

# Resizing panels programmatically

The Dashboard Layout panels can also be resized programmatically by using [resizePanel](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#resizepanel) method. The method is invoked as follows,

```js
resizePanel(id, sizeX, sizeY)

```

Where,
* id - ID of the panel which needs to be resized.
* sizeX - New panel width in cells count for resizing the panel.
* sizeY - New panel height in cells count for resizing the panel.

The following sample demonstrates resizing panels programmatically in the Dashboard Layout's [created](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#created) event.

{% tab template="dashboard-layout/resize-panel", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { DashboardLayoutComponent } from '@syncfusion/ej2-angular-layouts';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild('defaultLayout') dashboardLayout: DashboardLayoutComponent;
    public cellSpacing: number[] = [10, 10];
    public columns: number = 5;
    public panels: any = [
    {'sizeX': 1, 'sizeY': 1, 'row': 0, 'col': 0, content:'<div class="content">0</div>'},
    {'sizeX': 3, 'sizeY': 2, 'row': 0, 'col': 1, content:'<div class="content">1</div>'},
    {'sizeX': 1, 'sizeY': 3, 'row': 0, 'col': 4, content:'<div class="content">2</div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 1, 'col': 0, content:'<div class="content">3</div>'},
    {'sizeX': 2, 'sizeY': 1, 'row': 2, 'col': 0, content:'<div class="content">4</div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 2, 'col': 2, content:'<div class="content">5</div>'},
    {'sizeX': 1, 'sizeY': 1, 'row': 2, 'col': 3, content:'<div class="content">6</div>'},
    ];

    //Dashboard Layout's created event function
    onCreated(args: any) {
        // resizePanel("id", sizeX, sizeY)
        this.dashboardLayout.resizePanel("layout_4", 1, 1);
        this.dashboardLayout.resizePanel("layout_5", 2, 1);
    }

}
```

{% endtab %}