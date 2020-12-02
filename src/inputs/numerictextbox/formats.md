---
title: "Formats"
component: "NumericTextBox"
description: "The Numeric Text Box provides an option to customize the display format of the numeric value using the format property"
---

# Number Formats

You can format the value of NumericTextBox using [`format`](../api/numerictextbox#format) property.
The value will be displayed in the specified format when the component is in focused out state. The format string
supports both the [standard numeric format string](https://msdn.microsoft.com/en-us/library/dwhawy9k.aspx)
and [custom numeric format string](https://msdn.microsoft.com/en-us/library/0c899ak8.aspx) as
specified in MSDN.

## Standard formats

From the [standard Numeric Formats](https://msdn.microsoft.com/en-us/library/dwhawy9k.aspx) of MSDN, you can use the numeric related
format specifiers such as `n`,`p` and `c` in the NumericTextBox component. By using these format specifiers, you can achieve the percentage
and currency textbox behavior also.

The below example demonstrates percentage and currency formats.

{% tab template="numerictextbox/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the NumericTextBox component
    // sets percentage with 2 numbers of decimal places format
    // sets currency with 2 numbers of decimal places format
    template: `
             <div class='wrap'>
               <ejs-numerictextbox format='p2' value='0.5' min='0' max='1' step='0.01' placeholder='Percentage format' floatLabelType= 'Auto'></ejs-numerictextbox>
             </div>
             <div class='wrap'>
               <ejs-numerictextbox format='c2' value='10' placeholder='Currency format' floatLabelType= 'Auto'></ejs-numerictextbox>
             </div>
            `
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}

## Custom formats

From the [custom numeric format string](https://msdn.microsoft.com/en-us/library/0c899ak8.aspx) of MSDN, you can provide any custom format by
combining one or more custom specifiers.

The below examples demonstrate format the value by using currency format string `#` and `0`.

{% tab template="numerictextbox/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the NumericTextBox component
    // sets the format using custom format string `#`
    // sets the format using custom format string `0`
    template: `
            <div class='wrap'>
               <ejs-numerictextbox format='###.##' value='10' placeholder='Custom format string #' floatLabelType= 'Auto'></ejs-numerictextbox>
             </div>
            <div class='wrap'>
               <ejs-numerictextbox format='000.00' value='10' placeholder='Custom format string 0' floatLabelType= 'Auto'></ejs-numerictextbox>
             </div>
            `
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}