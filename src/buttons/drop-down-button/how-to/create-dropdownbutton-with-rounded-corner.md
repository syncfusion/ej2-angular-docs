---
title: "Create DropDownButton with rounded corner"
component: "DropDownButton"
description: "Angular DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Create DropDownButton with rounded corner

DropDownButton with rounded corner can be achieved by adding `border-radius` CSS property to button element.

In the following example, `e-round-corner` class is defined with `5px` `border-radius`
property and added that class to button element using
[`cssClass`](../../api/drop-down-button#cssclass) property.

{% tab template="drop-down-button/rounded", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton with 'e-round-corner' class. -->
               <button ejs-dropdownbutton [items]='items' content='Clipboard' cssClass='e-round-corner'></button>`
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