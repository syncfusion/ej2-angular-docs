---
title: "Name and Value in form submit"
component: "CheckBox"
description: "Angular CheckBox how to section, name and value in form submit, and customization of CheckBox appearance, frame & check icon."
---

# Name and Value in form submit

The [`name`](../../api/check-box/#name) attribute of the CheckBox is used to group Checkboxes. When the Checkboxes are
grouped in form, the checked items [`value`](../../api/check-box/#value) attribute will post to the server on form submit
which can be retrieved through the name. The [`disabled`](../../api/check-box/#disabled) and unchecked CheckBox value will
not be sent to the server on form submit.

In the following code snippet, Cricket and Hockey are in the checked state,
Tennis is in disabled state and Basketball is in unchecked state. Now, the value
that is in checked state only be sent on form submit.

{% tab template= "check-box/form", sourceFiles="app/**/*.ts",index.html,styles.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    //Name and Value attribute in form submit.
    template: `<form>
                <ul>
                    <li><ejs-checkbox name="Sport" value="Cricket" label="Cricket" [checked]="true"></ejs-checkbox></li>

                    <li><ejs-checkbox name="Sport" value="Hockey" label="Hockey" [checked]="true"></ejs-checkbox></li>

                    <li><ejs-checkbox name="Sport" value="Tennis" label="Tennis" [disabled]="true"></ejs-checkbox></li>

                    <li><ejs-checkbox name="Sport" value="Basketball" label="Basketball"></ejs-checkbox></li>

                    <li><button ejs-button [isPrimary]="true">Submit</button></li>
                </ul>
               </form>`
})

export class AppComponent { }

```

{% endtab %}