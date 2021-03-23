---
title: "How To"
component: "Sidebar"
description: "Miscellaneous aspects of customizing the sidebar"
---

# Open and close the Sidebar

Opening and closing the Sidebar can be achieved with built-in public methods.

* [`show()`](../../api/sidebar/#show): Method to open the Sidebar.
* [`hide()`](../../api/sidebar/#hide): Method to close the Sidebar.
* [`toggle()`](../../api/sidebar/#toggle): Method to toggle between open and close states of the Sidebar.

In the following sample, toggle method has been used to show or hide the Sidebar on button click.

{% tab template="sidebar/openclose", sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('sidebar') sidebar: SidebarComponent;
    public open() {
       console.log("Sidebar Opened");
    }
    public close() {
        console.log("Sidebar Closed");
    }
    toggleClick() {
        this.sidebar.toggle();
    }
    closeClick() {
        this.sidebar.hide();
    }
}

```

{% endtab %}
