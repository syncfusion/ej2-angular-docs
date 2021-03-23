# Enable or disable context menu items

You can enable and disable the menu items using the [`enableItems`](../../api/menu#enableitems) method in ContextMenu. To enable menuItems, set the `enable` property in argument to `true` and vice-versa.

In the following example, the **Display Settings** in parent items and **Medium icons** in sub menu items are disabled.

{% tab template= "context-menu/template", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ContextMenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-angular-navigations';

@Component({
  selector: 'app-root',
  template: `<!--target element-->
            <div id="target">Right click / Touch hold to open the ContextMenu</div>
            <!-- To Render ContextMenu. -->
            <ejs-contextmenu #contextmenu target='#target' [items]='menuItems' (created)='onCreated()' (beforeOpen)='beforeOpen()'></ejs-contextmenu>`
})

export class AppComponent {

    @ViewChild('contextmenu')
    public contextmenu: ContextMenuComponent;

    // ContextMenu items definition
    public menuItems: MenuItemModel[] = [
    {
        text: 'View',
        items: [
          {
            text: 'Large icons'
          },
          {
            text: 'Medium icons'
          },
          {
            text: 'Small icons'
          }
        ]
    },
    {
        text: 'Sort By'
    },
    {
        text: 'Refresh'
    },
    {
        separator: true
    },
    {
        text: 'New'
    },
    {
        separator: true
    },
    {
        text: 'Display Settings'
    },
    {
        text: 'Personalize'
    }];

    onCreated(): void {
      this.contextmenu.enableItems(['Display Settings'], false);
    }

    beforeOpen(): void {
      this.contextmenu.enableItems(['Medium icons'], false);
    }
}
```

{% endtab %}

> To disable sub menu items, use the [`beforeOpen`](../../api/menu#beforeopen) event.