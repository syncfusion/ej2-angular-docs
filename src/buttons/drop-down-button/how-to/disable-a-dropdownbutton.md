---
title: "Disable a DropDownButton"
component: "DropDownButton"
description: "Angular DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Disable a DropDownButton

DropdownButton component can be enabled/disabled by giving [`disabled`](../../api/drop-down-button#disabled) property.
To disable DropdownButton component, the disabled property can be set as `true`.

{% tab template="drop-down-button/disabled", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton. -->
               <button ejs-dropdownbutton [items]='items' content='Message' iconCss='ddb-icons e-message' disabled='true'></button>`
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