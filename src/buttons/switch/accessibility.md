---
title: "Switch Accessibility"
component: "Switch"
description: "Angular Switch component has accessibility support to help access the features via keyboard, on-screen readers, or other assistive technology devices."
---

# Accessibility

The web accessibility makes web content and web applications more accessible for people with disabilities. It
especially helps in dynamic content change and development of advanced user interface controls with AJAX, HTML,
JavaScript, and related technologies.

Switch provides built-in compliance with `WAI-ARIA` specifications. `WAI-ARIA` support is achieved through the
attributes like `aria-checked` and `aria-disabled`. It helps the people with disabilities by providing information
about the widget for assistive technology in the screen readers, such as screen readers.

| Properties | Functionality |
| ------------ | ----------------------- |
| role | Indicates the switch component. |
| aria-checked | Indicates whether the input is checked, unchecked. |
| aria-disabled | Indicates that the element is perceivable but disabled, so it is not editable or otherwise operable. |

## Keyboard interaction

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td>
<b>Keyboard shortcuts</b></td><td>
<b>Actions</b></td></tr>
<tr>
<td>
<kbd>Space</kbd></td><td>
When the switch has focus, pressing the Space key changes the state of the switch.</td></tr>
</table>

{% tab template= "switch/state", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<table class='size'>
                <tr>
                    <td class='lSize'>Checked</td>
                    <td>
                        <ejs-switch [checked]="true"></ejs-switch>
                    </td>
                </tr>
                <tr>
                    <td class='lSize'>Unchecked</td>
                    <td>
                        <ejs-switch></ejs-switch>
                    </td>
                </tr>
                </table>`
})

export class AppComponent { }

```

{% endtab %}