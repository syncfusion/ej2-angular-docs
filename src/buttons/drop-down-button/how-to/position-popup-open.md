---
title: "Position popup open"
component: "DropDownButton"
description: "Angular DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Position popup open

Popup open position can be changed according to the requirement. Popup open position can be changed in
[`open`](../../api/drop-down-button#open) event by setting `top` and `left` for the popup element.

In the following example, the `top` position of the popup element is changed in `open` event.

{% tab template="drop-down-button/position", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ItemModel, OpenCloseMenuEventArgs, DropDownButtonComponent  } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton. -->
               <button ejs-dropdownbutton #dropdownbutton [items]='items' content='Clipboard' (open)='onOpen($event)'></button>`
})

export class AppComponent {
   @ViewChild('dropdownbutton')
   public dropdownbutton: DropDownButtonComponent;
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
    // To open popup in particular position.
    public onOpen (args: OpenCloseMenuEventArgs) {
       args.element.parentElement.style.top = this.dropdownbutton.element.getBoundingClientRect().top - args.element.parentElement.offsetHeight +'px';
    }

}
```

{% endtab %}