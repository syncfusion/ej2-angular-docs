---
title: "Moving of panels programmatically"
component: "Dashboard Layout"
description: "This section explains how to move the panels programmatically within the layout in Essential JS 2 Dashboard Layout component"
---

# Moving of panels programmatically

Other than drag and drop, it is possible to move the panels in Dashboard Layout programmatically. This can be achieved using [movePanel](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#movepanel) method. The method is invoked as follows,

```js
movePanel(id, row, col)

```

Where,
* id - ID of the panel which needs to be moved.
* row - New row position for moving the panel.
* col - New column position for moving the panel.

Each time a panel's position is changed(Programmatically or through UI interaction), the Dashboard Layout's [change](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#change) event will be triggered.

The following sample demonstrates moving a panel programmatically to a new position in the Dashboard Layout's [created](https://ej2.syncfusion.com/angular/documentation/api/dashboard-layout/#created) event.

{% tab template="dashboard-layout/moving", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

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
       // movePanel("id", row, col)
        this.dashboardLayout.movePanel("layout_0", 1, 0);

    }
    //Dashboard Layout's change event function
    onChange(args: any) {
        console.log("Change event triggered");
    }

}
```

{% endtab %}