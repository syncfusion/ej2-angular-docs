---
title: "ContextMenu Template and  Multilevel Nesting"
component: "ContextMenu"
description: "Angular ContextMenu allows the end user to customize the menu items, and supports multiple level of nesting."
---

# Template and Multilevel nesting

## Template

The ContextMenu items can be customized using the
[`beforeItemRender`](../api/context-menu#beforeitemrender) property. The item render event
triggers while rendering each menu item. The event argument will be used to identify the menu
item and customized it based on the requirement. In the following sample, the menu item is rendered with keycode for
specified action in ContextMenu using the template. Here, the keycode is specified for Save as, View page
source, and Inspect in the right side corner of the menu items by adding span element in the
[`beforeItemRender`](../api/context-menu#beforeitemrender) event.

{% tab template= "context-menu/template", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { createElement } from '@syncfusion/ej2-base';
import { MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-navigations';

@Component({
  selector: 'app-root',
  template: `<!--target element-->
            <div id="target">Right click / Touch hold to open the ContextMenu</div>
            <!-- To Render ContextMenu. -->
            <ejs-contextmenu id='contextmenu' #contextmenu target='#target' [items]='menuItems' (beforeItemRender)='itemBeforeEvent($event)'></ejs-contextmenu>`
})

export class AppComponent {
    public menuItems: MenuItemModel[] = [
        {
            text: 'Save as...'
        },
        {
            text: 'View page source'
        },
        {
            text: 'Inspect'
        }];

    public itemBeforeEvent (args: MenuEventArgs) {
        let shortCutSpan: HTMLElement = createElement('span');
        let text: string = args.item.text;
        let shortCutText: string = text === 'Save as...' ? 'Ctrl + S' : (text === 'View page source' ? 'Ctrl + U'      : 'Ctrl + Shift + I');
        shortCutSpan.textContent = shortCutText;
        args.element.appendChild(shortCutSpan);
        shortCutSpan.setAttribute('class','shortcut');
    }
}
```

{% endtab %}

> To create span element, `createElement` utility function used from `ej2-base`.

## Multilevel nesting

The Multiple level nesting supports in ContextMenu. It can be achieved by mapping the [`items`](../api/context-menu/menuItemModel#items)
property inside the parent [`menuItems`](../api/context-menu#items). In the following sample, three
level nesting of ContextMenu is provided.

{% tab template= "context-menu/template", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { MenuItemModel } from '@syncfusion/ej2-navigations';

@Component({
  selector: 'app-root',
  template: `<!--target element-->
            <div id="target">Right click / Touch hold to open the ContextMenu</div>
            <!-- To Render ContextMenu. -->
            <ejs-contextmenu id='contextmenu' #contextmenu target='#target' [items]='menuItems'></ejs-contextmenu>`
})

export class AppComponent {
    public menuItems: MenuItemModel[] = [
        {
            text: 'Show All Bookmarks'
        },
        {
            text: 'Bookmarks Toolbar',
            items: [
                {
                    text: 'Most Visited',
                    items:[
                        {
                            text: 'Gmail'
                        },
                        {
                            text: 'Google'
                        }
                    ]
                },
                {
                    text: 'Recently Added'
                }
            ]
        }];

}
```

{% endtab %}

> To open sub menu items only on click, [`showItemOnClick`](../api/context-menu#showitemonclick) property should be set as `true`.

## See Also

* [Populate menu items with data source](./how-to/populate-menu-items-with-data-source)
