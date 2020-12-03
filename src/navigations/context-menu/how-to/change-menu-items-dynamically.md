# Change menu items dynamically

The items visible in the ContextMenu can be changed dynamically based on the target in which
you open the ContextMenu. To achieve this behavior, initialize ContextMenu with all
items using [`items`](../../api/context-menu#items)
property and then based on the context you open hide/show required items using
[`hideItems`](../../api/context-menu#hideitems)/
[`showItems`](../../api/context-menu#showitems) method in
[`beforeOpen`](../../api/context-menu#beforeopen) event.

In the following example, the datasource for Clipboard div is `Cut`, `Copy`, `Paste` and
for the Editor div is `Add`, `Edit`, `Delete` is changed on
[`beforeOpen`](../../api/context-menu#beforeopen) event using
[`hideItems`](../../api/context-menu#hideitems) and
[`showItems`](../../api/context-menu#showitems) method.

{% tab template="context-menu/dynamic", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { MenuItemModel, BeforeOpenCloseMenuEventArgs } from '@syncfusion/ej2-navigations';
import { ContextMenuComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
  selector: 'app-root',
  template: `<!--target element-->
            <div id="target">
              <div id='left' class='e-div'>Clipboard</div>
              <div id='right' class='e-div'>Editor</div>
            </div>
            <!-- To Render ContextMenu. -->
            <ejs-contextmenu #contextmenu target='#target .e-div' [items]= 'menuItems' (beforeOpen)='beforeOpen($event)'></ejs-contextmenu>`
})

export class AppComponent {
    @ViewChild('contextmenu')
    public cmenu: ContextMenuComponent;
    // Initialize menu items.
    public menuItems: MenuItemModel[] = [
    {
        text: 'Cut'
    },
    {
        text: 'Copy'
    },
    {
        text: 'Paste'
    },
    {
        text: 'Add'
    },
    {
        text: 'Edit'
    },
    {
        text: 'Delete'
    }];

    public beforeOpen (args: BeforeOpenCloseMenuEventArgs) {
       // To hide/show items on right click.
       if ((args.event.target as HTMLElement).id === 'right') {
          this.cmenu.hideItems(['Cut', 'Copy', 'Paste']);
          this.cmenu.showItems(['Add', 'Edit', 'Delete']);
       } else if ((args.event.target as HTMLElement).id === 'left') {
          this.cmenu.showItems(['Cut', 'Copy', 'Paste']);
          this.cmenu.hideItems(['Add','Edit','Delete']);
       }
    }
}
```

{% endtab %}
