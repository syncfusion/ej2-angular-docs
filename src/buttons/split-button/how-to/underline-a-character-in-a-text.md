---
title: "Underline a character in a text"
component: "SplitButton"
description: "Angular SplitButton how to section, group popup items using list view component, dialog open on popup item click."
---

# Underline a character in a text

To underline a particular character in a text, it can be handled in [`beforeItemRender`](../../api/split-button#beforeitemrender) event by
adding `<u>` tag in between the text and given as innerHTML in `li` rendering.

In the following example, `C` is underlined in the text `Copy`:

{% tab template="split-button/underline", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel, MenuEventArgs } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To Render splitbutton. -->
               <ejs-splitbutton content="Paste" [items]='items' (beforeItemRender)="itemRender($event)"></ejs-splitbutton>`
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
            // To underline a particular text.
            args.element.innerHTML = '<u>C</u>opy';
        }
    }

}
```

{% endtab %}