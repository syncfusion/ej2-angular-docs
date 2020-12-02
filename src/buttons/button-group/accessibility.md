---
title: "ButtonGroup Accessibility"
component: "ButtonGroup"
description: "ButtonGroup component has accessibility support to help access the features via keyboard, on-screen readers, or other assistive technology devices."
---

# Accessibility

The web accessibility makes web content and web applications more accessible for people with disabilities. It especially helps in dynamic content change and development of advanced user interface controls with AJAX, HTML, JavaScript, and related technologies.
ButtonGroup provides built-in compliance with `WAI-ARIA` specifications. It helps the people with disabilities by providing information about the widget for assistive
technology in the screen readers. ButtonGroup component contains the `group` role.

| Properties | Functionality |
| ------------ | ----------------------- |
| role | Indicates the `group` for the container that holds two or more buttons. |

## Keyboard interaction

### Normal behavior

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Keyboard shortcuts</b></td>
<td><b>Actions</b></td>
</tr>
<tr>
<td><kbd>Tab</kbd></td>
<td>Focuses the next button in the ButtonGroup.</td>
</tr>
<tr>
<td><kbd>Enter/Space</kbd></td>
<td>Activates the focussed button in the ButtonGroup.</td>
</tr>
</table>

### Checkbox behavior

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Keyboard shortcuts</b></td>
<td><b>Actions</b></td>
</tr>
<tr>
<td><kbd>Tab</kbd></td>
<td>Focuses the next button in the ButtonGroup.</td>
</tr>
<tr>
<td><kbd>Space</kbd></td>
<td>Activates the focussed button in the ButtonGroup.</td>
</tr>
</table>

### Radiobutton behavior

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td><b>Keyboard shortcuts</b></td>
<td><b>Actions</b></td>
</tr>
<tr>
<td><kbd>Tab</kbd></td>
<td>Focuses the active button in the ButtonGroup.</td>
</tr>
<tr>
<td><kbd>Arrow Keys</kbd></td>
<td>Activates next/previous button in the ButtonGroup.</td>
</tr>
</table>

{% tab template="button-group/util", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render ButtonGroup. -->
            <h5>Normal behavior</h5>
            <div class='e-btn-group' role='group'>
                <button class="e-btn">HTML</button>
                <button class="e-btn">CSS</button>
                <button class="e-btn">Javascript</button>
            </div>
            <h5>Checkbox type behavior</h5>
            <div class='e-btn-group' role='group'>
                <input type="checkbox" id="check_bold" name="font" value="bold"/>
                <label class="e-btn" for="check_bold">Bold</label>
                <input type="checkbox" id="check_italic" name="font" value="italic"/>
                <label class="e-btn" for="check_italic">Italic</label>
                <input type="checkbox" id="check_underline" name="font" value="underline"/>
                <label class="e-btn" for="check_underline">Underline</label>
            </div>
            <h5>Radiobutton type behavior</h5>
            <div class='e-btn-group' role='group'>
                <input type="radio" id="radioleft" name="align" value="left"/>
                <label class="e-btn" for="radioleft">Left</label>
                <input type="radio" id="radiomiddle" name="align" value="middle"/>
                <label class="e-btn" for="radiomiddle">Center</label>
                <input type="radio" id="radioright" name="align" value="right"/>
                <label class="e-btn" for="radioright">Right</label>
            </div>`
})

export class AppComponent { }
```

{% endtab %}