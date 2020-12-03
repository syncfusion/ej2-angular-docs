---
title: "How To"
component: "Sidebar"
description: "Miscellaneous aspects of customizing the sidebar"
---

# Sidebar with fixed position

The following example demonstrates how to render sidebar with fixed position. When scroll the main content area, the position of the sidebar will not change.

{% tab template="sidebar/fixed-position", sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('sidebar')
    public sidebar: SidebarComponent;
    public width: string = '290px';
    public onCreated(args: any) {
         this.sidebar.element.style.visibility = '';
    }
    openClick(): void {
        this.sidebar.toggle();
    }

}


```

{% endtab %}
