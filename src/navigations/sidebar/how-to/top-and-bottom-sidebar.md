# Top and bottom Sidebar

You can initialize Sidebar at the left and right positions by using the [`position`](../../api/sidebar#position) property. It will automatically adjust the width of the main content.

You can also initialize Sidebar at the top and bottom positions in application level. For initializing Sidebar, you need to manually adjust the height of the main content.

In the following sample, the [`toggle`](../../api/sidebar/#toggle) method has been used to show or hide the top and bottom sidebar on button click.

{% tab template="sidebar/top-bottom", sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('topSidebar', { static: true }) topSidebar: SidebarComponent;
    @ViewChild('bottomSidebar', { static: true }) bottomSidebar: SidebarComponent;

    public type: string = 'Push';
    // only for sample browser use
    constructor( ) {

    }
    topBtnClick() {
        this.topSidebar.toggle();
    }
    bottomBtnClick() {
        this.bottomSidebar.toggle();
    }
    top_sidebar_open() {
        let element: Element = document.getElementsByClassName("e-content-animation")[0];
        (<HTMLElement>element).style.height = ((<HTMLElement>element).offsetHeight - 75) + "px";
        element.classList.add("top_content_animation");
        // Remove the e-left class in sidebar
        this.topSidebar.element.classList.remove("e-left");
        // Add the custom class to sidebar
        this.topSidebar.element.classList.add("top_sidebar");
    }
    top_sidebar_close() {
        let element: Element = document.getElementsByClassName("e-content-animation")[0];
        (<HTMLElement>element).style.height = ((<HTMLElement>element).offsetHeight + 75) + "px";
        element.classList.remove("top_content_animation");
    }

    bottom_sidebar_open() {
        let element: Element = document.getElementsByClassName("e-content-animation")[0];
        (<HTMLElement>element).style.height = ((<HTMLElement>element).offsetHeight - 75) + "px";
        element.classList.add("bottom_animation_content");
        // Remove the e-left class in sidebar
        this.bottomSidebar.element.classList.remove("e-left");
        // Add the custom class to sidebar
        this.bottomSidebar.element.classList.add("bottom_sidebar");
    }

    bottom_sidebar_close() {
        let element: Element = document.getElementsByClassName("e-content-animation")[0];
        (<HTMLElement>element).style.height = ((<HTMLElement>element).offsetHeight + 75) + "px";
        element.classList.remove("bottom_animation_content");
    }
}

```

{% endtab %}
