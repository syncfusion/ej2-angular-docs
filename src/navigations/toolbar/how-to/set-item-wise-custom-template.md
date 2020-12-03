---
title: "Set item-wise custom template"
component: "Toolbar"
description: "This example demonstrates how to create custom template into the Essential JS 2 Toolbar component items."
---

# Set item wise custom template

The Toolbar supports adding template commands using the  `template` property. Template property can be given as the `HTML element`
that is either a `string`  or a `query selector`.

## As string

The HTML element tag can be given as a string for the template property. Here, the checkbox is rendered as a HTML template.

```typescript
template: "<div><input type='checkbox' id='check1' checked=''>Accept</input></div>"

```

## As selector

The template property also allows getting template content through query `selector`. Here, checkbox 'ID' attribute is specified in the template.

```typescript
template: "#Template"

```

{% tab template="toolbar/toolbar-items", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
         <button id='Template' class='e-btn'>Template</button>
        <ejs-toolbar>
          <e-items>
             <e-item text='Cut'></e-item>
             <e-item type='Separator'></e-item>
             <e-item text='Paste' prefixIcon = 'e-paste-icon'></e-item>
             <e-item type='Separator'></e-item>
             <e-item [template]='templateEle'></e-item>
             <e-item text='Undo'></e-item>
             <e-item text='Redo'></e-item>
             <e-item [template]='templateEleId'></e-item>
          </e-items>
        </ejs-toolbar>
        `
})

export class AppComponent {
    @ViewChild('element') element;
    public templateEle: any = '<input placeholder="Search" style="height:27px;"/>';
    public templateEleId: any = '#Template';
    ngAfterViewInit() {
    }
}

```

{% endtab %}