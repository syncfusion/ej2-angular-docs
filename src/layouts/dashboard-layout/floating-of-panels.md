---
title: "Floating"
component: "DashboardLayout"
description: "This section explains the floating functionality of Essential JS 2 DashboardLayout component"
---

# Floating

The floating functionality of the component allows you to effectively use the entire layout for the panel's placement. If the floating functionality is enabled, the panels within the layout get floated upwards automatically to occupy the empty cells available in previous rows. This functionality can be enabled or disabled using the `allowFloating` property of the component.

The following sample demonstrates how to enable or disable the floating of panels in the DashboardLayout component.

{% tab template="dashboard-layout/floating-of-panels", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts,app/default-style.css" %}

```typescript
import { Component, ViewChild, ViewEncapsulation } from '@angular/core';
import { DashboardLayoutComponent } from '@syncfusion/ej2-angular-layouts';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-root',
    styleUrls: ['app/default-style.css'],
    templateUrl: 'app/app.template.html',
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild('defaultLayout') dashboard: DashboardLayoutComponent;
    @ViewChild('toggleBtn') toggleBtn: ButtonComponent;
    public cellSpacing: any = [10, 10];
    public allowFloating: boolean = false;
    public cellAspectRatio: number = 100/75;
    public panels: any = [
    {'sizeX': 2, 'sizeY': 2, 'row': 1, 'col': 0, content:'<div class="content">0</div>'},
    {'sizeX': 2, 'sizeY': 2, 'row': 2, 'col': 2, content:'<div class="content">1</div>'},
    {'sizeX': 2, 'sizeY': 2, 'row': 3, 'col': 4, content:'<div class="content">2</div>'}
    ];

    btnClick() {
        if (this.toggleBtn.content == "Disable Floating and Reset") {
            this.toggleBtn.content = 'Enable Floating';
            this.dashboard.allowFloating = false;
            this.dashboard.panels = this.panels;
        } else {
            this.toggleBtn.content = 'Disable Floating and Reset';
            this.dashboard.allowFloating = true;
        }
    }
}
```

{% endtab %}
