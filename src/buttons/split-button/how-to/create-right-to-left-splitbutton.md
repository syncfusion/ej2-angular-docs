---
title: "Create right-to-left SplitButton"
component: "SplitButton"
description: "Angular SplitButton how to section, group popup items using list view component, dialog open on popup item click."
---

# Create right-to-left SplitButton

SplitButton component has RTL support. This can be achieved by setting [`enableRtl`](../../api/split-button#enablertl) as `true`.

The following example illustrates how to enable right-to-left support in SplitButton component.

{% tab template="split-button/disabled", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

 ```typescript
import { Component } from '@angular/core';
import { ItemModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To Render splitbutton. -->
               <ejs-splitbutton content="Autosum" [items]='items' iconCss="e-sb e-sigma" enableRtl=true></ejs-splitbutton>`
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