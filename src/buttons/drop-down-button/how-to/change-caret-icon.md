---
title: "Change caret icon"
component: "DropDownButton"
description: "Angular DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Change caret icon

Dropdown arrow can be customized on popup open and close. It can be handled in
[`beforeOpen`](../../api/drop-down-button#beforeopen) and
[`beforeClose`](../../api/drop-down-button#beforeclose) event.

In the following example, the up arrow is updated on popup close and down arrow is updated
on popup open using `beforeOpen` and `beforeClose` event by adding and removing
`e-caret-up` class.

{% tab template="drop-down-button/updown", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ItemModel, BeforeOpenCloseMenuEventArgs, DropDownButtonComponent  } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render DropDownButton. -->
               <button ejs-dropdownbutton #dropdownbutton [items]='items' content='Clipboard' (beforeOpen)='beforeOpen($event)' (beforeClose)='beforeClose($event)'></button>`
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
    // To update up arrow with `e-caret-up` class.
    public beforeOpen (args: BeforeOpenCloseMenuEventArgs) {
        this.dropdownbutton.cssClass = 'e-caret-up';
    }
    // To remove `e-caret-up` class.
    public beforeClose (args: BeforeOpenCloseMenuEventArgs) {
        this.dropdownbutton.cssClass = '';
    }

}
```

{% endtab %}