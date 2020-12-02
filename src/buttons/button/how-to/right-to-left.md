---
title: "Right-To-Left"
component: "Button"
description: "Angular Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Right-To-Left

Button component has RTL support. This can be achieved by setting [`enableRtl`](../../api/button#enablertl) as `true`.

The following example illustrates how to enable right-to-left support in Button component.

{% tab template="button/block", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true%}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls:['styles.css'],
    template:  `<button ejs-button iconCss="e-btn-icons e-setting-icon" [enableRtl]="true">Settings</button>`
})

export class AppComponent { }
```

{% endtab %}