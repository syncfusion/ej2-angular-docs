---
title: "Underline a character in the item text"
component: "DropDownButton"
description: "Angular DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Underline a character in the item text

Underline a particular character in a text can be handled in
[`beforeItemRender`](../../api/drop-down-button#beforeitemrender)event by
adding `<u>` tag in between the text and given as innerHTML in `li` rendering.

In the following example, `C` is underlined in the text `Copy`.

{% tab template="drop-down-button/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel, MenuEventArgs } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton. -->
               <button ejs-dropdownbutton [items]='items' content='Clipboard' (beforeItemRender)="itemRender($event)"></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
        {
            text: 'Cut'
        },
        {
            text: 'Copy'
        },
        {
            text: 'Paste'
        }];
    public itemRender(args: MenuEventArgs) {
        if (args.item.text === 'Copy') {
            //To underline a particular text.
            args.element.innerHTML = '<u>C</u>opy';
        }
    }
}
```

{% endtab %}