---
title: "Set the disabled state"
component: "SplitButton"
description: "Angular SplitButton how to section, group popup items using list view component, dialog open on popup item click."
---

# Set the disabled state

SplitButton component can be enabled or disabled by [`disabled`](../../api/split-button#disabled) property.
To disable SplitButton component, set the disabled property as true.

The following example illustrates how to set the disable state in SplitButton component.

{% tab template="split-button/disabled", sourceFiles="app/**/*.ts", isDefaultActive=true %}

 ```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To Render splitbutton. -->
               <ejs-splitbutton content="Autosum" [items]='items' iconCss="e-sb e-sigma" disabled= true></ejs-splitbutton>`
})

export class AppComponent {
  public items: ItemModel[] = [
      {
        text: 'Autosum'
    },
    {
        text: 'Average'
    },
    {
        text: 'Count numbers',
    },
    {
        text: 'Min'
    },
    {
        text: 'Max'
    }];
}
```

{% endtab %}