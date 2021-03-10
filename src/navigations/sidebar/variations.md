---
title: "Variatons"
component: "Sidebar"
description: "The different types in type property of the sidebar gives flexibility to view or hide the content (primary/secondary) over/above the main content by pushing, sliding, or overlaying it."
---

# Types

The Sidebar component's expand behaviour can be modified based on the purpose of use.

## Expanding types of Sidebar

The Sidebar can be set to initialize based on four different types that are consistent with the main component as explained below.

 | Item | Description |
|-----|-----|
| `Over` | Sidebar floats over the main content area.|
| `Push` | Sidebar pushes the main content area to appear side-by-side, and shrinks the main content within the screen width.|
| `Slide` |Sidebar translates the x and y positions of main content area based on the Sidebar width. The main content area will not be adjusted within the screen width. |
| `Auto` | Sidebar with `Over` type in mobile resolution, and `Push` type in other higher resolutions. |

> `Auto` is the default expand mode.

In the following sample, the types of Sidebar are demonstrated.

{% tab template="sidebar/Types", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component, ViewChild  } from '@angular/core';
import { SidebarComponent } from '@syncfusion/ej2-angular-navigations';
import { ButtonComponent, RadioButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('sidebar') sidebar: SidebarComponent;
    @ViewChild('togglebtn') togglebtn: ButtonComponent;

    public type: string = 'Push';
    public target: string = '.content';
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
    changeHandler(args: any) : void {
        if(args.event.target.ej2_instances[0].label == 'Over') {
            this.sidebar.type = 'Over';
        } else if (args.event.target.ej2_instances[0].label == 'Push') {
             this.sidebar.type = 'Push';
        } else if (args.event.target.ej2_instances[0].label == 'Slide') {
             this.sidebar.type = 'Slide';
        } else {
             this.sidebar.type = 'Auto';
        }
    }
}
```

{% endtab %}