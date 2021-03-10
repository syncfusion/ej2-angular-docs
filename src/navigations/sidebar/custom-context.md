---
title: "Custom Context"
component: "Sidebar"
description: "Sidebar can set to be initialized , target to any HTML element alongside of the main content of a web page."
---

# Target

Sidebar has a flexible option to make it initialize, target to any HTML element alongside of the main content of a web page.

By default, it initialize target to the body element. [`target`](../api/sidebar/#target)  property allows users to set target element to initialize the Sidebar inside any HTML container element apart from the body element.

> If required , `zIndex` can be set when sidebar act as overlay type.

{% tab template="sidebar/custom", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';
import { ButtonComponent } from "@syncfusion/ej2-angular-buttons";
@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('sidebar') sidebar: SidebarComponent;
    public type: string = 'Push';
    public target: string = '.content';
    @ViewChild('togglebtn')
    public togglebtn: ButtonComponent;
    public onCreated(args: any) {
         this.sidebar.element.style.visibility = '';
    }
    btnClick(){
        if(this.togglebtn.element.classList.contains('e-active')){
            this.togglebtn.content = 'Open';
            this.sidebar.hide();
        }
        else{
            this.togglebtn.content = 'Close';
            this.sidebar.show();
        }
    }
    closeClick() {
         this.sidebar.hide();
         this.togglebtn.element.classList.remove('e-active');
         this.togglebtn.content = 'Open'
    }
}

```

{% endtab %}

## See Also

* [Angular routing](./how-to/hide-sidebar)