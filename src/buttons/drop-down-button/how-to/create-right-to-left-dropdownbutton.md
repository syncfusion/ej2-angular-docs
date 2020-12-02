---
title: "Create right-to-left DropDownButton"
component: "DropDownButton"
description: "Angular DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Create right-to-left DropDownButton

DropDownButton component has RTL support. This can be achieved by setting [`enableRtl`](../../api/drop-down-button#enablertl) as true.

The following example illustrates how to enable right-to-left support in DropDownButton component.

{% tab template="drop-down-button/disabled", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton. -->
               <button ejs-dropdownbutton [items]='items' content='Message' iconCss='ddb-icons e-message' enableRtl='true'></button>`
})

export class AppComponent {
   // Initialize action items.
   public items: ItemModel[] = [
    {
        text: 'Edit'
    },
    {
        text: 'Delete'
    },
    {
        text: 'Mark as Read'
    },
    {
        text: 'Like Message'
    }];

}
```

{% endtab %}