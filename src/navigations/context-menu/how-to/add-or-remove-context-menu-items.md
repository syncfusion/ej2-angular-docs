# Add or remove context menu items

ContextMenu items can be added or removed using the [`insertAfter`](../../api/menu#insertafter), [`insertBefore`](../../api/menu#insertbefore) and [`removeItems`](../../api/menu#removeitems) methods.

In the following example, the **Display Settings** menu items are added before the **Personalize** item, the **Sort By** menu items are added after the **Refresh**, and the **Paste** item is removed from context menu.

{% tab template= "context-menu/template", sourceFiles="app/**/*.ts", isDefaultActive=true  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ContextMenuComponent, MenuEventArgs, MenuItemModel } from '@syncfusion/ej2-angular-navigations';

@Component({
  selector: 'app-root',
  template: `<!--target element-->
            <div id="target">Right click / Touch hold to open the ContextMenu</div>
            <!-- To Render ContextMenu. -->
            <ejs-contextmenu #contextmenu target='#target' [items]='menuItems' (created)='onCreated()'></ejs-contextmenu>`
})

export class AppComponent {
     @ViewChild('contextmenu')
    public contextmenu: ContextMenuComponent;

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
        text: 'Refresh'
    },
    {
        text: 'Paste'
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
        text: 'Personalize'
    }];

    onCreated(): void {
      this.contextmenu.insertAfter([{text: 'Sort By'}] , 'Refresh');
      this.contextmenu.insertBefore([{text: 'Display Settings'}] , 'Personalize');
      this.contextmenu.removeItems(['Paste']);
    }

}
```

{% endtab %}