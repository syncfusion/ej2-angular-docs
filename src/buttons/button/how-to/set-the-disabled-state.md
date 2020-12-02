---
title: "Set the disabled state"
component: "Button"
description: "Angular Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Set the disabled state

Button component can be enabled/disabled by giving
[`disabled`](../../api/button#disabled) property. To disable Button component,
the `disabled` property can be set as `true`.

The following example demonstrates button in `disabled` state.

{% tab template="button/block", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template:  `<button ejs-button [disabled]="true">Disabled</button>`
})

export class AppComponent { }
```

{% endtab %}