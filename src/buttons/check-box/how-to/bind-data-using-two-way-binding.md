---
title: "Bind data using two way binding"
component: "CheckBox"
description: "Angular CheckBox how to section, name and value in form submit, and customization of CheckBox appearance, frame & check icon."
---

# Bind data using two way binding

Checkbox component supports two way binding.

In this following example, two way binding for Checkbox is illustrated with Switch component. The steps to achieve two way binding in CheckBox
are as follows,

* Initialize CheckBox component and bind the checked value using `ngModel` as in the below code using "banana in a box" syntax,

```typescript

<ejs-checkbox #checkbox [(ngModel)]="checked"></ejs-checkbox>

```

* Initialize Switch component and assign the [`checked`](../../api/switch#checked) property value like the below code,

```typescript

<ejs-switch #switch [(checked)]="checked"></ejs-switch>

```

* Now, the changes made in CheckBox will reflect in Switch (i.e When the state of CheckBox is changed to checked state then the Switch
state will also change to checked state) and vice versa.

{% tab template= "check-box/binding", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div id='container'>
                    <table class='tablealign'>
                        <thead>
                            <th></th>
                            <th>
                                <h4>Checkbox</h4>
                            </th>
                            <th>
                                <h4>Switch</h4>
                            </th>
                        </thead>
                        <tr>
                            <td class='dataalign'>
                                <label>Wi-Fi</label>
                            </td>
                            <td class='dataalign'>
                                <ejs-checkbox #wcheckbox [(ngModel)]="checkedwifi">
                                </ejs-checkbox>
                            </td>
                            <td class='dataalign'>
                                <ejs-switch #wswitch [(checked)]="checkedwifi">
                                </ejs-switch>
                            </td>
                        </tr>
                        <tr>
                            <td class='dataalign'>
                                <label>Bluetooth</label>
                            </td>
                            <td class='dataalign'>
                                <ejs-checkbox #bcheckbox  [(ngModel)]="checkedbluetooth">
                                </ejs-checkbox>
                            </td>
                            <td class='dataalign'>
                                <ejs-switch #bswitch [(checked)]="checkedbluetooth">
                                </ejs-switch>
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