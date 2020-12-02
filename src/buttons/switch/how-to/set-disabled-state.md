---
title: "Set disabled state"
component: "Switch"
description: "Angular Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Set disabled state

Switch can be disabled by setting the [`disabled`](../../api/switch#disabled) property to `true`.

The following example illustrates how to disable support in Switch component.

{% tab template= "switch/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-switch [disabled]="true"></ejs-switch>`

})

export class AppComponent {}

```

{% endtab %}