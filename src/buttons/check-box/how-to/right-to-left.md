---
title: "Right-To-Left"
component: "CheckBox"
description: "Angular CheckBox how to section, name and value in form submit, and customization of CheckBox appearance, frame & check icon."
---

# Right-To-Left

CheckBox component has RTL support. This can be achieved by setting [`enableRtl`](../../api/check-box#enablertl) as `true`.

The following example illustrates how to enable right-to-left support in CheckBox component.

{% tab template= "check-box/rtl", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ejs-checkbox label="Default" [enableRtl]="true"></ejs-checkbox>`
})

export class AppComponent { }

```

{% endtab %}