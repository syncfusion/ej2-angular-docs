---
title: "Add Font Awesome icons || Add third-party icons"
component: "Toolbar"
description: "This example demonstrates how to add the font awesome icons into Essential JS Toolbar items."
---

# Add Font Awesome

You can customize the Toolbar component items by using third-party icons other than the icons available in the Syncfusion library. In the following example, font awesome icons are used as toolbar items.

* Refer to the third-party reference link. Here, the CDN link of font awesome is referred.

```html
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css" />
```

* Add the icons to the toolbar component using ['prefixIcon'](../../api/toolbar/itemDirective/#prefixicon) property

The following sample explains how to use font awesome in the toolbar component.

{% tab template="toolbar/add-font-awesome", sourceFiles="app/app.component.ts,index.html" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ToolbarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-container',
    template: `
        <ejs-toolbar>
          <e-items>
          <e-item prefixIcon="fa fa-twitter"></e-item>
          <e-item prefixIcon="fa fa-facebook"></e-item>
          <e-item prefixIcon="fa fa-whatsapp"></e-item>
          <e-item
          template='<button class="e-btn e-tbar-btn"><span><i style="font-size: 3em; color: Tomato" class="e-icons fa fa-twitter"></i></span></button>'></e-item>
          </e-items>
       </ejs-toolbar>`
})

export class AppComponent {

}

```

{% endtab %}

> We can also use templates for rendering icons based on the requirements.

## Customization

The class “e-icons” is used for standardizing the appearance of the icons to fit into toolbar items. If you wish to override the appearance of the icons used, you could do this by using the following set of classes

Use the following CSS to set the color of icons.

```CSS

    .e-toolbar .e-icons {
        color: #e3165b !important;
    }

```

Use the following CSS to set the font size of icons.

```CSS

    .e-toolbar .e-btn .e-icons.e-btn-icon {
        font-size: 14px !important;
    }

```