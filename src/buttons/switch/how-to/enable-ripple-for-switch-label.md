---
title: "Enable ripple for Switch label"
component: "Switch"
description: "Angular Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Enable ripple for Switch label

By default, label with ripple effect is not available in Switch. You can achieve this by using `rippleMouseHandler`
method.

The following example illustrates how to enable ripple effect for labels in Switch component.

{% tab template= "switch/getting-started", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component, OnInit } from '@angular/core';
import { rippleMouseHandler } from '@syncfusion/ej2-buttons';

@Component({
    selector: 'app-root',
    template: `<div id='container'>
        <table class="ripple">
            <tr>
                <td class="lRipple"><label for='switch1'>USB Tethering</label></td>
                <td>
                    <ejs-switch id="switch1" [checked]="true"></ejs-switch>
                </td>
            </tr>
        </table>
    </div>`

})

export class AppComponent implements OnInit {
    ngOnInit(): void {
                document.querySelector('.lRipple label').addEventListener('mouseup', rippleHandler);
                document.querySelector('.lRipple label').addEventListener('mousedown', rippleHandler);
                function rippleHandler(e: MouseEvent): void  {
                    let rippleSpan: Element = this.parentElement.nextElementSibling.querySelector('.e-ripple-container');
                    if (rippleSpan) {
                        rippleMouseHandler(e, rippleSpan);
                    }
                }
            }
    }
```

{% endtab %}