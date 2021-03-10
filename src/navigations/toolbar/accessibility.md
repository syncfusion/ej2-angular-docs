---
title: "Toolbar Accessibility"
component: "Toolbar"
description: "The Toolbar control has accessibility support to access the features via keyboard, screen readers, or other assistive technology devices."
---

# Accessibility

The Toolbar component has been designed,  keeping in mind the [WAI-ARIA](http://www.w3.org/WAI/PF/aria-practices/) specifications,
and applying the WAI-ARIA roles, states, and properties along with keyboard support for people who use assistive devices. WAI-ARIA
accessibility support is achieved through attributes like `aria-orientation`, `aria-disabled`, and `aria-haspopup`. It provides
information about elements in a document for assistive technology.  The component implements keyboard navigation support by
following the [WAI-ARIA practices](https://www.w3.org/TR/wai-aria-practices/), and has been tested in major screen readers.

## ARIA attributes

The Toolbar element is assigned the role of `toolbar`.

| **Property** | **Functionalities** |
| --- | --- |
| role="toolbar" | This attribute added to the ToolBar element describes the actual role of the element. |
| aria-orientation     | Indicates the ToolBar orientation. Default value is `horizontal`. |
| aria-haspopup       | Indicates the popup mode of the Toolbar. Default value is false. When popup mode is enabled,  attribute value has to be changed to `true`. |
| aria-disabled       | Indicates the disabled state of the ToolBar. |

## Keyboard interaction

Keyboard navigation is enabled by default. Possible keys are

| Key           | Description                                                                         |
|---------------|-------------------------------------------------------------------------------------|
| <kbd>Left</kbd>    | Focuses the previous element.                                                    |
| <kbd>Right</kbd>   | Focuses the next element.                                                            |
| <kbd>Enter</kbd>         | When focused on a ToolBar command, clicking the key triggers the click of Toolbar element. When popup drop-down icon is focused, the popup opens. |
| <kbd>Esc(Escape)</kbd>           | Closes popup.                                                                     |
| <kbd>Down</kbd>   | Focuses the next popup element.                                                  |
| <kbd>Up</kbd>      | Focuses the previous popup element.                                                |

{% tab template="toolbar/toolbar-items", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ToolbarComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-container',
    template: `
        <ejs-toolbar>
          <e-items>
             <e-item text='Cut' prefixIcon = 'e-cut-icon tb-icons' showTextOn ='Overflow'></e-item>
             <e-item text='Copy' prefixIcon = 'e-copy-icon tb-icons' showTextOn ='Overflow'></e-item>
             <e-item text='Paste' prefixIcon = 'e-paste-icon tb-icons' showTextOn ='Overflow'></e-item>
             <e-item type='Separator'></e-item>
             <e-item text='bold' prefixIcon = 'e-bold-icon tb-icons' showTextOn ='Overflow'></e-item>
             <e-item text='underline' prefixIcon = 'e-underline-icon tb-icons' showTextOn ='Overflow'></e-item>
             <e-item text='italic' prefixIcon = 'e-italic-icon tb-icons' showTextOn ='Overflow'></e-item>
             <e-item type='Separator'></e-item>
             <e-item text='A-Z Sort' prefixIcon = 'e-ascending-icon tb-icons' showTextOn ='Overflow'></e-item>
             <e-item text='Z-A Sort' prefixIcon = 'e-descending-icon tb-icons' showTextOn ='Overflow'></e-item>
          </e-items>
        </ejs-toolbar>
        `
})

export class AppComponent {
    @ViewChild('element') element;

    ngAfterViewInit() {
    document.onkeyup = function (e) {
    if (e.altKey && e.keyCode === 84) {
        document.getElementById('Toolbar').focus();
    }
    };
    }
}
```

{% endtab %}
