---
title: "ContextMenu Accessibility"
component: "ContextMenu"
description: "Angular ContextMenu component has accessibility support to help access the features via keyboard, on-screen readers, or other assistive technology devices."
---

# Accessibility

The web accessibility makes web content and web applications more accessible for people with
disabilities. It especially helps in dynamic content change and development of advanced user interface
controls with AJAX, HTML, JavaScript, and related technologies. ContextMenu provides built-in
compliance with `WAI-ARIA` specifications. `WAI-ARIA` support is achieved through attributes the
like `aria-expanded` and `aria-haspopup` applied for menu item in ContextMenu. It helps the people
with disabilities by providing information about the widget for assistive technology in the screen
readers. ContextMenu component contains the `menu` role and `menuItem` role.

| Properties | Functionality |
| ------------ | ----------------------- |
| menu | This role will be specified for an item that do not have sub menus. |
| menuItem | This role will be specified for an item which don’t have sub menus. |
| aria-haspopup | Indicates the availability and type of interactive popup element. |
| aria-expanded | Indicates whether the subtree can be expanded or collapsed, as well as indicates whether its current state expanded or collapsed. |

## Keyboard interaction

| Keyboard shortcuts | Actions |
| ------------ | ----------------------- |
| Esc | Closes the opened ContextMenu. |
| Enter | Selects the focused menu item. |
| Up | Navigates up or to the previous menu item. |
| Down | Navigates down or to the next menu item. |
| Left | Close the current sub menu and navigates to the parent menu. |
| Right | Navigates and opens the next sub menu. |

{% tab template="context-menu/aria-and-keyboard", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { getInstance } from '@syncfusion/ej2-base';
import { MenuItemModel, ContextMenu } from '@syncfusion/ej2-navigations';

@Component({
  selector: 'app-root',
  template: `
            <div id='target'>Right click / Touch hold to open the ContextMenu</div>
            <ejs-contextmenu id='contextmenu' target='#target' [items]= 'menuItems' (load)="menuOpen()"></ejs-contextmenu>`
})

export class AppComponent {
    public menuItems: MenuItemModel[] = [
        {
            text: 'Cut',
            iconCss: 'e-cm-icons e-cut'
        },
        {
            text: 'Copy',
            iconCss: 'e-cm-icons e-copy'
        },
        {
            text: 'Paste',
            iconCss: 'e-cm-icons e-paste',
            items: [
                {
                    text: 'Paste Text',
                    iconCss: 'e-cm-icons e-pastetext'
                },
                {
                    text: 'Paste Special',
                    iconCss: 'e-cm-icons e-pastespecial'
                }
            ]
        }];

     ngAfterViewInit(): void{
         setTimeout(() => {
            let contextmenuObj: ContextMenu = getInstance(document.getElementById("contextmenu_0"), ContextMenu) as ContextMenu;
            contextmenuObj.open(40, 20);
        }, 300);
     }
}
```

{% endtab %}