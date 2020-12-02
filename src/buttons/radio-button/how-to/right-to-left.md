---
title: "Right-To-Left"
component: "RadioButton"
description: "Angular RadioButton how to section, name and value in form submit, customize RadioButton appearance."
---

# Right-To-Left

RadioButton component has RTL support. This can be achieved by setting [`enableRtl`](../../api/radio-button#enablertl) as `true`.

The following example illustrates how to enable right-to-left support in RadioButton component.

{% tab template= "radio-button/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // To customize RadioButton appearance
    template: `<ul>
               <li><ejs-radiobutton label="Option 1" name="default" enableRtl="true" checked="true"></ejs-radiobutton></li>
               <li><ejs-radiobutton label="Option 2" name="default" enableRtl="true"></ejs-radiobutton></li>
               </ul>`
})

export class AppComponent { }

```

{% endtab %}