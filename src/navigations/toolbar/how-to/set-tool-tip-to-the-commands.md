---
title: "Set Essential JS 2 Tooltip to the commands"
component: "Toolbar"
description: "This example demonstrates how to set the Essential JS 2 Tooltip control to the Essential JS 2 Toolbar control commands."
---

# Set Essential JS 2 tooltip to the commands

The [`tooltipText`](../../../api/toolbar/item#tooltiptext) property of the Toolbar item is used to set the HTML Tooltip to the commands that can be viewed as hint texts on mouse hover.

To change the [`tooltipText`](../../../api/toolbar/item#tooltiptext) to ej2-tooltip component:

* Import the `Tooltip` module from `ej2-popups`,and initialize the Tooltip with the Toolbar target. Refer to the following code example:

{% tab template="toolbar/toolbar-items", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ToolbarComponent } from '@syncfusion/ej2-angular-navigations';
import { Tooltip } from '@syncfusion/ej2-popups';

@Component({
    selector: 'app-container',
    template: `
        <div id = 'Tooltip'>
        <ejs-toolbar id = 'Toolbar'>
          <e-items>
             <e-item text='Cut' tooltipText = 'Cut'></e-item>
             <e-item text='Copy' tooltipText = 'Copy'></e-item>
             <e-item text='Paste' tooltipText = 'Paste'></e-item>
             <e-item text='Undo' tooltipText = 'Undo'></e-item>
             <e-item text='Redo' tooltipText = 'Redo'></e-item>
          </e-items>
        </ejs-toolbar>
        </div>
        `
})

export class AppComponent {
    @ViewChild('element') element;

    ngAfterViewInit() {
       let tooltip: Tooltip = new Tooltip({
       target: '#Toolbar [title]',
        });
       tooltip.appendTo('#Tooltip');
    }
}
```

{% endtab %}