# Open and close ContextMenu

Open and close the ContextMenu manually whenever required by using open and close methods.

In the following sample, the ContextMenu is opened using the [`open`](../../api/context-menu#open)
method at the specified position with `X` and `Y` coordinates and to close the ContextMenu,
[`close`](../../api/context-menu#close) method is called internally on ContextMenu
item click or document click.

{% tab template= "context-menu/how-to", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { getInstance } from '@syncfusion/ej2-base';
import { MenuItemModel, ContextMenu } from '@syncfusion/ej2-navigations';

@Component({
  selector: 'app-root',
  template: `<!-- To Render ContextMenu. -->
            <ejs-contextmenu id='contextmenu' [items]= 'menuItems'></ejs-contextmenu>
            <!-- To Render Button. -->
            <button ejs-button (click)="btnClick()">Open ContextMenu</button>`,
})

export class AppComponent  {
    // Initialize action items.
    public menuItems: MenuItemModel[] = [
        {
            text: 'Cut'
        },
        {
            text: 'Copy'
        },
        {
            text: 'Paste'
        }];

    btnClick() {
        let contextmenuObj: ContextMenu = getInstance(document.getElementById("contextmenu_0"), ContextMenu) as ContextMenu;
        contextmenuObj.open(40, 20);
    }
}
```

{% endtab %}
