# Underline a character in the item text

To underline a particular character in a text, it can be handled in `beforeItemRender` event by
adding `<u>` tag in between the text and given as innerHTML in `li` rendering.

{% tab template="context-menu/separators", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { MenuItemModel, MenuEventArgs } from '@syncfusion/ej2-navigations';

@Component({
  selector: 'app-root',
  template: `<div id="target">Right click / Touch hold to open the ContextMenu</div>
            <ejs-contextmenu id='contextmenu' target='#target' [items]= 'menuItems' (beforeItemRender)='itemRender($event)'></ejs-contextmenu>`
})

export class AppComponent {
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
    public itemRender(args: MenuEventArgs ) {
       if (args.item.text === "Copy") {
            args.element.innerHTML = '<u>C</u>opy';
       }
    }
}
```

{% endtab %}
