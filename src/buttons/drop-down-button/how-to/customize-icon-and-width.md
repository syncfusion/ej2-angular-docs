---
title: "Customize icon and width"
component: "DropDownButton"
description: "Angular DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Customize icon and width

Width of the DropDownButton can be customized by setting required width to the dropdown element.

The following UI can be achieved by setting
[`iconPosition`](../../api/drop-down-button#iconposition) as `Top`, width as `85px`
and size of the font icon as `40px` by adding `e-custom` class.

{% tab template="drop-down-button/custom-width", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton. -->
               <button ejs-dropdownbutton [items]='items' content='Find & Select' iconCss='e-icons e-search' iconPosition='Top' cssClass='e-custom'></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
    {
        text: 'Find'
    },
    {
        text: 'Replace'
    },
    {
        text: 'Go To'
    },
    {
        text: 'Go To Special'
    }];
}
```

{% endtab %}