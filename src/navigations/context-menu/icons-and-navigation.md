---
title: "ContextMenu Icons and Navigation"
component: "ContextMenu"
description: "Angular ContextMenu allows the end user to place the icons on menu items and navigate to other webpages while clicking the menu items."
---

# Icons and Navigation

## Icons

The ContextMenu item can have an icon/image
in it to provide visual representation of the action. To place the icon on a menu item,
set the [`iconCss`](../api/context-menu/menuItemModel#iconcss) property to e-icons with the required
icon CSS. By default, the icon is positioned to the left side of the menu item. In the following sample, the icons for Cut,
Copy and Paste menu items are added using the `iconCss` property.

{% tab template="context-menu/icons-and-navigation", sourceFiles="app/**/*.ts",isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { MenuItemModel } from '@syncfusion/ej2-navigations';

@Component({
  selector: 'app-root',
  template: `<div id="target">Right click / Touch hold to open the ContextMenu</div>
            <ejs-contextmenu id='contextmenu' target='#target' [items]='menuItems'></ejs-contextmenu>`
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
        }];
}
```

{% endtab %}

## Navigation

Navigation in ContextMenu is usage to navigate to the other web page when menu item is
clicked. This can be achieved by providing link to the menu item using the
[`url`](../api/context-menu/menuItemModel#url) property.
In the following sample, Navigation URL for Flipkart, Amazon, and Snapdeal menu items
are added using the `url` property.

{% tab template="context-menu/icons-and-navigation", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { MenuItemModel, MenuEventArgs } from '@syncfusion/ej2-navigations';

@Component({
  selector: 'app-root',
  template: `<div id="target">Right click / Touch hold to open the ContextMenu</div>
            <ejs-contextmenu id='contextmenu' target='#target' [items]='menuItems'
            (beforeItemRender)='itemBeforeEvent($event)'></ejs-contextmenu>`,
})

export class AppComponent {
    public menuItems: MenuItemModel[] = [
     {
        text: 'Flipkart',
        iconCss: 'e-cart-icon e-link',
        url: 'https://www.google.co.in/search?source=hp&q=flipkart'
    },
    {
        text: 'Amazon',
        iconCss: 'e-cart-icon e-link',
        url: 'https://www.google.co.in/search?q=amazon'
    },
    {
        text: 'Snapdeal',
        iconCss: 'e-cart-icon e-link',
        url: 'https://www.google.co.in/search?q=snapdeal'
    }];

    public itemBeforeEvent (args: MenuEventArgs) {
        args.element.getElementsByTagName('a')[0].setAttribute('target', '_blank');
    }
}
```

{% endtab %}

> To open the links in new tab, set `target` attribute with the value `_blank` in the
[`beforeItemRender`](../api/context-menu#beforeitemrender) event.

## See Also

* [How to change menu items dynamically](./how-to/change-menu-items-dynamically)
