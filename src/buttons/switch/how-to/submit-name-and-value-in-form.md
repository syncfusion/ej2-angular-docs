---
title: "Submit name and value in form"
component: "Switch"
description: "Angular Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Submit name and value in form

The [`name`](../../api/switch#name) attribute of the Switch is used to group Switches. When the Switches are grouped in form, the checked items
[`value`](../../api/switch#value) attribute will post to the server on form submit. The disabled and unchecked Switch values will not be sent to
the server on form submit.

In the following code snippet, USB and Wi-Fi in the [`checked`](../../switch#checked) state, and Bluetooth is in disabled state.
Values that are in checked state only be sent on form submit.

{% tab template= "switch/form", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<form><table class='size'>
                <tr>
                    <td class='lSize'>USB</td>
                    <td>
                        <ejs-switch name= "Tethering" value= "USB" [checked]="true" ></ejs-switch>
                    </td>
                </tr>
                <tr>
                    <td class='lSize'>Wi-Fi</td>
                    <td>
                        <ejs-switch name= "Hotspot" value= "Wi-Fi" [checked]="true" ></ejs-switch>
                    </td>
                </tr>
                <tr>
                    <td class='lSize'>Bluetooth</td>
                    <td>
                        <ejs-switch name= "Tethering" value= "Bluetooth" [disabled]="true" ></ejs-switch>
                    </td>
                </tr>
               <tr>
                    <td>
                        <button ejs-button [isPrimary]="true">Submit</button>
                    </td>
                </tr>
                </table></form>`
})

export class AppComponent { }

```

{% endtab %}
