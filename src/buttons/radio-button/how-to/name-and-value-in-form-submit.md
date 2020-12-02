---
title: "Name and Value in form submit"
component: "RadioButton"
description: "Angular RadioButton how to section, name and value in form submit, customize RadioButton appearance."
---

# Name and Value in form submit

The [`name`](../../api/radio-button#name) attribute of the RadioButton is used to group RadioButton. When the RadioButton
are grouped in form, the checked item [`value`](../../api/radio-button#value) attribute will be post to server on form submit
that can be retrieved through the name. The disabled and unchecked RadioButton value will
not be sent to the server on form submit.

In the following code snippet, Credit and Debit card is in the checked state. Now, the value that is in checked state will be sent on form submit.

{% tab template= "radio-button/form", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // Name and Value attribute in form submit.
    template: `<form>
                <ul>
                    <li><ejs-radiobutton name="payment" value="credit/debit" label="Credit / Debit card" checked="true"></ejs-radiobutton></li>

                    <li><ejs-radiobutton name="payment" value="netbanking" label="Net Banking"></ejs-radiobutton></li>

                    <li><ejs-radiobutton name="payment" value="cashondelivery" label="Cask On Delivery"></ejs-radiobutton></li>

                    <li><ejs-radiobutton name="payment" value="others" label="Others"></ejs-radiobutton></li>

                    <li><button ejs-button [isPrimary]="true">Submit</button></li>
                </ul>
               </form>`
})

export class AppComponent { }

```

{% endtab %}