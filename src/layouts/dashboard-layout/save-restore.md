---
title: "Panel State Maintenance"
component: "DashboardLayout"
description: "This section explains how to save and restore the panels settings of Essential JS 2 DashboardLayout component"
---

# Panel state maintenance

The current layout structure of the Dashboard Layout component can be obtained and saved to construct another dashboard with same panel structure using the serialize public method of the component. This method returns the component's current panel setting which can be used to construct a dashboard with the same layout settings.

The following sample demonstrates how to save and restore the state of the panels using the serialize method. Click Save to store the panel's settings and click Restore to restore the previously saved panel settings.

{% tab template="dashboard-layout/save-restore", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { DashboardLayoutComponent, PanelModel } from '@syncfusion/ej2-angular-layouts';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild('defaultLayout') dashboard: DashboardLayoutComponent;
    @ViewChild('saveBtn') saveBtn: ButtonComponent;
    @ViewChild('restoreBtn') restoreBtn: ButtonComponent;
    public restoreModel: any = [];
    public cellSpacing: number[] = [10, 10];
    public panels: any = [{ "sizeX": 1, "sizeY": 1, "row": 0, "col": 0, content: '<div class="content">0</div>' },
    { "sizeX": 3, "sizeY": 2, "row": 0, "col": 1, content: '<div class="content">1</div>' },
    { "sizeX": 1, "sizeY": 3, "row": 0, "col": 4, content: '<div class="content">2</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 1, "col": 0, content: '<div class="content">3</div>' },
    { "sizeX": 2, "sizeY": 1, "row": 2, "col": 0, content: '<div class="content">4</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 2, content: '<div class="content">5</div>' },
    { "sizeX": 1, "sizeY": 1, "row": 2, "col": 3, content: '<div class="content">6</div>' }
    ];

    onSaveClick() {
      this.restoreModel= this.dashboard.serialize();
      this.restoreModel[0].content = '<div class="content">0</div>';
      this.restoreModel[1].content = '<div class="content">1</div>';
      this.restoreModel[2].content = '<div class="content">2</div>';
      this.restoreModel[3].content = '<div class="content">3</div>';
      this.restoreModel[4].content = '<div class="content">4</div>';
      this.restoreModel[5].content = '<div class="content">5</div>';
      this.restoreModel[6].content = '<div class="content">6</div>';
    }

    onrestoreClick() {
      this.dashboard.panels = this.restoreModel;
    }
}
```

{% endtab %}