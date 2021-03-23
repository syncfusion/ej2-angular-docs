---
title: "Set command customization"
component: "Toolbar"
description: "This example demonstrates how to set the HTML attribute commands to Essential JS 2 Toolbar control items."
---

# Set command customization

The [`htmlAttributes`](../../../api/toolbar/item#htmlattributes) property of the Toolbar item is used to set the HTML attributes ('ID', 'class', 'style' ,'role') for the commands.

When style attributes are added, if the same attributes were already present, they will be replaced. This is not so in the case of
`class` attribute. Classes will be added to the element instead of replacing the existing ones.

Single or multiple CSS classes can be added to the Toolbar commands using the Toolbar item [`cssClass`](../../../api/toolbar/item#cssclass) property.

{% tab template="toolbar/toolbar-items", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ToolbarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-container',
    template: `
        <ejs-toolbar>
          <e-items>
             <e-item text='Bold'  [htmlAttributes] = 'boldAttribute'></e-item>
             <e-item text='Italic' [htmlAttributes] = 'italicAttribute'></e-item>
             <e-item text='Underline' [htmlAttributes] = 'underAttribute'></e-item>
             <e-item type='Separator'></e-item>
             <e-item text='Uppercase' cssClass = 'e-txt-casing'></e-item>
          </e-items>
        </ejs-toolbar>
        `
})

export class AppComponent {
    @ViewChild('element') element;
     public boldAttribute: any = { 'class': 'custom_bold', 'id': 'itemId' };
     public italicAttribute: any = { 'class': 'custom_italic' };
     public underAttribute: any = { 'class': 'custom_underline' };
    ngAfterViewInit() {
    }
}
```

{% endtab %}