---
title: "Enable RTL"
component: "Switch"
description: "Angular Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Enable RTL

Switch component has RTL support. This can be achieved by setting [`enableRtl`](../../api/switch#enablertl) as `true`.

The following example illustrates how to enable right-to-left support in Switch component.

{% tab template= "switch/rtl", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-switch [enableRtl]="true"></ejs-switch>`
})

export class AppComponent { }

```

{% endtab %}