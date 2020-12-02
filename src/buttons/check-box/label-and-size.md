---
title: "CheckBox Label and Size"
component: "CheckBox"
description: "Angular CheckBox component supports different sizes and label."
---

# Label and Size

This section explains the different sizes and labels.

## Label

The CheckBox caption can be defined using the [`label`](../api/check-box#label) property. This reduces the manual addition
of label for CheckBox. You can customize the label position before or after the CheckBox
through the [`labelPosition`](../api/check-box#labelposition) property.

{% tab template= "check-box/label-and-size", sourceFiles="app/**/*.ts",index.html,styles.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ul>
               <!-- Label position - Left. -->
               <li><ejs-checkbox label="Left Side Label" labelPosition="Before"></ejs-checkbox></li>

               <!-- Label position - Right. -->
               <li><ejs-checkbox label="Right Side Label" [checked]="true"></ejs-checkbox></li>
               </ul>`
})

export class AppComponent { }

```

{% endtab %}

## Size

The different CheckBox size are default and small. To reduce the size of default CheckBox to small,
set the [`cssClass`](../api/check-box#cssclass) property to `e-small`.

{% tab template= "check-box/label-and-size", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ul>
               <!-- Small CheckBox. -->
               <li><ejs-checkbox label="Small" cssClass="e-small"></ejs-checkbox></li>

               <!-- Default CheckBox. -->
               <li><ejs-checkbox label="Default"></ejs-checkbox></li>
               </ul>`
})

export class AppComponent { }

```

{% endtab %}

## See Also

* [CheckBox customization](./how-to/customized-checkbox)