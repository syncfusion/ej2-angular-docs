---
title: "How To"
component: "Sidebar"
description: "Miscellaneous aspects of customizing the sidebar"
---

# Multiple Sidebar

Two Sidebars can be initialized in a web page with same main content. Sidebars can be initialized on right
side or left side of the main content using [`position`](../../api/sidebar#position) property.

>The HTML element with class name `e-main-content` will be considered as the main content and both the
Sidebars will behave as side content to this main content area of a web page.

{% tab template="sidebar/multiple", sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('leftSidebar') leftSidebar: SidebarComponent;
    @ViewChild('rightSidebar') rightSidebar: SidebarComponent;

    public width:string='250px';
    public position:string='Right';
    public type:string='Push';

    leftToggle() {
        this.leftSidebar.toggle();
    }
    rightToggle() {
        this.rightSidebar.toggle();
    }
}


```

{% endtab %}
