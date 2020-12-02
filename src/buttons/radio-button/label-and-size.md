---
title: "RadioButton Label and Size"
component: "RadioButton"
description: "Angular RadioButton component supports different sizes and label."
---

# Label and Size

This section explains the different sizes and labels.

## Label

RadioButton caption can be defined by using the [`label`](../api/radio-button#label) property. This reduces the manual addition
of label for RadioButton. You can customize the label position before or after the RadioButton
through the [`labelPosition`](../api/radio-button#labelposition) property.

{% tab template= "radio-button/label-and-size", sourceFiles="app/**/*.ts",index.html,styles.css", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ul>
               <!-- Label position - Left. -->
               <li><ejs-radiobutton label="Left Side Label" name="position" labelPosition="Before"></ejs-radiobutton></li>

               <!-- Label position - Right. -->
               <li><ejs-radiobutton label="Right Side Label" name="position" checked="true"></ejs-radiobutton></li>
               </ul>`
})

export class AppComponent { }

```

{% endtab %}

## Size

The different RadioButton size are default and small. To reduce the size of the default RadioButton to small,
set the [`cssClass`](../api/radio-button#cssclass) property to `e-small`.

{% tab template= "radio-button/label-and-size", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<ul>
               <!-- Small RadioButton. -->
               <li><ejs-radiobutton label="Small" name="small" checked="true" cssClass="e-small"></ejs-radiobutton></li>

               <!-- Default RadioButton. -->
               <li><ejs-radiobutton label="Default" name="small"></ejs-radiobutton></li>
               </ul>`
})

export class AppComponent { }

```

{% endtab %}

## See Also

* [How to customize the RadioButton appearance](./how-to/customize-radiobutton-appearance)
