---
title: "CheckBox Accessibility"
component: "CheckBox"
description: "Angular CheckBox component has accessibility support to help access the features via keyboard, on-screen readers, or other assistive technology devices."
---

# Accessibility

The web accessibility makes web content and web applications more accessible for people with disabilities.
It especially helps in dynamic content change and development of advanced user interface controls with AJAX, HTML, JavaScript, and
related technologies. CheckBox provides built-in compliance with `WAI-ARIA` specifications. `WAI-ARIA` support is achieved through
the attributes like `aria-checked` and `aria-disabled`. It helps the people with disabilities by providing information about the
widget for assistive technology in the screen readers. CheckBox component contains the `checkbox` role.

| Properties | Functionality |
| ------------ | ----------------------- |
| role | Indicates the type of input element. |
| aria-checked | Indicates whether the input is checked, unchecked, or represents mixture of checked and unchecked values. |
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
When the checkbox has focus, pressing the Space key changes the state of the checkbox.</td></tr>
</table>

{% tab template= "check-box/label-and-size", sourceFiles="app/**/*.ts",index.html,styles.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ul>
               <!-- checked state. -->
               <li><ejs-checkbox label="Checked State" [checked]="true"></ejs-checkbox></li>

               <!-- unchecked state. -->
               <li><ejs-checkbox label="Unchecked State"></ejs-checkbox></li>

               <!-- indeterminate state. -->
               <li><ejs-checkbox label="Indeterminate State" [indeterminate]="true"></ejs-checkbox></li>
               </ul>`
})

export class AppComponent { }

```

{% endtab %}