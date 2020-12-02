---
title: "Bind data using two way binding"
component: "Switch"
description: "Angular Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Bind data using two way binding

Switch component supports two way binding.

In this following example, two way binding for Switch is illustrated with CheckBox component. The steps to achieve two way binding in Switch
are as follows,

* Initialize Switch component and bind the checked value using `ngModel` as in the below code using "banana in a box" syntax,

```typescript

<ejs-switch #switch [(ngModel)]="checked"></ejs-switch>

```

* Initialize Checkbox component and assign the [`checked`](./../../check-box/api/check-box/#checked) property value like the below code,

```typescript

<ejs-checkbox #checkbox [(checked)]="checked"></ejs-checkbox>

```

* Now, the changes made in Switch will reflect in CheckBox (i.e When the state of Switch is changed to checked state then the CheckBox
state will also change to checked state) and vice versa.

{% tab template= "switch/binding", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div id='container'>
                    <table class='tablealign'>
                        <thead>
                            <th></th>
                            <th>
                                <h4>Switch</h4>
                            </th>
                            <th>
                                <h4>Checkbox</h4>
                            </th>
                        </thead>
                        <tr>
                            <td class='dataalign'>
                                <label>Wi-Fi</label>
                            </td>
                            <td class='dataalign'>
                                <ejs-switch #wswitch [(ngModel)]="checkedwifi">
                                </ejs-switch>
                            </td>
                            <td class='dataalign'>
                                <ejs-checkbox #wcheckbox [(checked)]="checkedwifi">
                                </ejs-checkbox>
                            </td>
                        </tr>
                        <tr>
                            <td class='dataalign'>
                                <label>Bluetooth</label>
                            </td>
                            <td class='dataalign'>
                                <ejs-switch #bswitch [(ngModel)]="checkedbluetooth">
                                </ejs-switch>
                            </td>
                            <td class='dataalign'>
                                <ejs-checkbox #bcheckbox  [(checked)]="checkedbluetooth">
                                </ejs-checkbox>
                            </td>
                        </tr>
                    </table>
               </div>`
})

export class AppComponent {
    public checkedwifi: boolean = true;
    public checkedbluetooth: boolean = false;
}

```

{% endtab %}