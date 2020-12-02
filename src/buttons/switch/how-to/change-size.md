---
title: "Change Size"
component: "Switch"
description: "Angular Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Change Size

The different Switch sizes available are default and small. To reduce the size of default Switch to small,
set the [`cssClass`](../../api/switch#cssclass) property to `e-small`.

{% tab template= "switch/state", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<table class='size'>
                <tr>
                    <td class='lSize'>Small</td>
                    <td>
                        <ejs-switch cssClass="e-small"></ejs-switch>
                    </td>
                </tr>
                <tr>
                    <td class='lSize'>Default</td>
                    <td>
                        <ejs-switch></ejs-switch>
                    </td>
                </tr>
               </table>`
})

export class AppComponent { }

```

{% endtab %}