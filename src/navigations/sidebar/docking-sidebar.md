---
title: "Docking Sidebar"
component: "Sidebar"
description: "Docking lets the sidebar occupy a small vertical area in a page always and typically contains shortened view of navigation options."
---

# Dock

Dock state of the Sidebar reserves some space on the page that always remains in a visible, when the Sidebar is in collapsed state. It is used to show the short form of a content like icons alone instead of lengthy text. To achieve this , set [`enableDock`](../api/sidebar/#enabledock) as true along with required [`dockSize`](../api/sidebar/#docksize).

{% tab template="sidebar/dock", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('dockBar') dockBar: SidebarComponent;
    public enableDock: boolean = true;
    public width: string = '220px';
    public dockSize: string = '72px';
    toggleClick() {
        this.dockBar.toggle();
    }
}

```

{% endtab %}

## See Also

* [How to add sidebar navigation](./how-to/sidebar-with-treeview)