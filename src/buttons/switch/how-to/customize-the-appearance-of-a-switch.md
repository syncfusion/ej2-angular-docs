---
title: "Customize the appearance of a Switch"
component: "Switch"
description: "Angular Switch how to section, customization of Switch bar and handle, change size, name and value in form submit."
---

# Customize the appearance of a Switch

You can customize the appearance of the Switch component using the CSS rules. Define your own CSS rules according to
your requirement and assign the class name to the [`cssClass`](../../api/switch#cssClass) property.

## Customize Switch bar and handle

Switch bar and handle can be customized as per requirement using CSS rules. Switch bar and handle customized using
`cssClass` property. In the following sample, the `border-radius` CSS property for the Switch bar (`e-switch-inner`)
and handle (`e-switch-handle`) elements was changed border radius circle to square shape.

{% tab template= "switch/how-to", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div id='container'>
                <div class="container switch-control">
                    <div>
                        <h3>Customizing Shape</h3>
                    </div>
                <div>
                    <label for="switch1" style="padding: 10px 82px 10px 7px"> Square Switch </label>
                    <ejs-switch id="switch1" cssClass="square" ></ejs-switch>
                </div>
                <div>
                    <label for='switch2' style="padding: 10px 76px 10px 7px"> Bar and handle </label>
                    <ejs-switch id="switch2" cssClass="custom-switch" [checked]= "true" ></ejs-switch>
                </div>
                <div>
                    <label for='switch3' style="padding: 10px 96px 10px 7px"> Handle text </label>
                    <ejs-switch id="switch3" cssClass="handle-text" ></ejs-switch>
                </div>
                </div>
               </div>`
})

export class AppComponent { }

```

{% endtab %}

## Color the Switch

Switch colors can be customized as per the requirement using CSS rules. Switch bar and handle colors customized using
`cssClass` property. In the following sample, the Switch bar (`e-switch-inner`) element background and border colors
were changed from default colors.

{% tab template= "switch/on-off", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<div id='container'>
                <div class="container switch-control">
                    <div>
                        <h3>Customizing Color</h3>
                    </div>
                <div>
                    <label for="switch1" style="padding: 10px 85px 10px 7px"> Custom color </label>
                    <ejs-switch id="switch1" cssClass="bar-color" ></ejs-switch>
                </div>
                <div>
                    <label for='switch2' style="padding: 10px 88px 10px 7px"> Handle color </label>
                    <ejs-switch id="switch2" cssClass="handle-color" [checked]= "true" ></ejs-switch>
                </div>
                <div>
                    <label for='switch3' style="padding: 10px 102px 10px 7px"> iOS Switch </label>
                    <ejs-switch id="switch3" cssClass="custom-iOS" [checked]="true" ></ejs-switch>
                </div>
                </div>
               </div>`
})

export class AppComponent { }

```

{% endtab %}