---
title: "DropDownButton Accessibility"
component: "DropDownButton"
description: "Angular DropDownButton component has accessibility support to help access the features via keyboard, on-screen readers, or other assistive technology devices."
---

# Accessibility

## ARIA attributes

The web accessibility makes web content and web applications more accessible for people with disabilities. Mostly it helps in dynamic
content change and development of advanced user interface controls with AJAX, HTML, JavaScript, and related technologies.
DropDownButton provides built-in compliance with `WAI-ARIA` specifications. `WAI-ARIA` support is achieved through the attributes like
`aria-expanded`, `aria-owns` and `aria-haspopup` applied for action item in DropDownButton. It helps by providing information about the
widget for assistive technology in the screen readers. DropDownButton component contains the `menu` role and `menuItem` role.

| Properties | Functionality |
| ------------ | ----------------------- |
| menu | Specified for an DropDownButton element. |
| menuItem | Specified for an action items. |
| aria-haspopup | Indicates the availability and type of interactive dropdown popup element. |
| aria-expanded | Indicates whether the current state of the dropdown popup can be expanded or collapsed. |
| aria-owns | Identifies elements to define a visual, functional, or contextual parent or child relationship between DOM(Document Object Model) elements where the hierarchy cannot be used to represent the relationship. |

## Keyboard interaction

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td>
<b>Keyboard shortcuts</b></td><td>
<b>Actions</b></td></tr>
<tr>
<td>
<kbd>Esc</kbd></td><td>
Closes the popup.</td></tr>
<tr>
<td>
<kbd>Enter</kbd></td><td>
Opens the popup, or activates the highlighted item and closes the popup.</td></tr>
<tr>
<td>
<kbd>Space</kbd></td><td>
Opens the popup.</td></tr>
<tr>
<td>
<kbd>Up</kbd></td><td>
Navigates up or to the previous action item.</td></tr>
<tr>
<td>
<kbd>Down</kbd></td><td>
Navigates down or to the next action item.</td></tr>
<tr>
<td>
<kbd>Alt + Up Arrow</kbd></td><td>
Closes the popup.</td></tr>
<tr>
<td>
<kbd>Alt + Down Arrow</kbd></td><td>
Opens the popup</td></tr>
</table>

{% tab template="drop-down-button/accessibility", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ItemModel, MenuEventArgs } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render Button. -->
               <button ejs-dropdownbutton [items]='items' content='Clipboard' iconCss='e-icons e-edit'></button>`
})

export class AppComponent {

   public items: ItemModel[] = [
    {
        text: 'Cut',
        iconCss: 'e-db-icons e-cut'
    },
    {
        text: 'Copy',
        iconCss: 'e-icons e-copy'
    },
    {
        text: 'Paste',
        iconCss: 'e-db-icons e-paste'
    },
    {
        separator: true
    },
    {
        text: 'Font',
        iconCss: 'e-db-icons e-font'
    },
    {
        text: 'Paragraph',
        iconCss: 'e-db-icons e-paragraph'
    }];

    public itemBeforeEvent (args: MenuEventArgs) {
       args.element.style.height = '105px';
    }

}
```

{% endtab %}