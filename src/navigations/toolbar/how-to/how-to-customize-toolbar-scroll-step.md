---
title: "How to customize toolbar scrollStep"
component: "Toolbar"
description: "This example demonstrates how to customize the scrolling distance of Essential JS 2 Toolbar control items when clicking left or right navigation icons."
---

# How to customize toolbar scrollStep

Toolbar supports to customize the scrolling distance when you click the left and right side navigation icons. we can customize `ScrollStep` property for scrolling distance. Refer to the following code example.

By using Toolbar scrollStep property, pass a required value to customize toolbar scrollStep.

{% tab template="toolbar/scrollstep", sourceFiles="app/app.component.html,app/app.component.ts,index.css,index.html" %}

```typescript

import { Component, ViewEncapsulation, Inject } from '@angular/core';
import { ToolbarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-container',
    templateUrl: 'app/app.component.html',
    encapsulation: ViewEncapsulation.None
})
export class DefaultToolbarComponent {
}

```

{% endtab %}