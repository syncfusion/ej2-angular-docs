---
title: "Hide dropdown arrow"
component: "DropDownButton"
description: "Angular DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Hide dropdown arrow

You can hide the dropdown arrow from the DropDownButton by adding class `e-caret-hide`
to DropDownButton element using [`cssClass`](../../api/drop-down-button#cssclass)
property.

{% tab template="drop-down-button/hide", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton with cssClass. -->
               <button ejs-dropdownbutton [items]='items' content='Clipboard' cssClass='e-caret-hide'></button>`
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

}
```

{% endtab %}