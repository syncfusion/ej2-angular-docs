---
title: "How To"
component: "DatePicker"
description: "Miscellaneous aspects of customizing the date picker"
---

# Disable, Placeholder, Read-only

Property | Purpose
-----|-----
 [`enabled`](../../api/datepicker#enabled) | The component can be restricted on a page, by setting enabled value as false which will disable the component completely from all user interactions including in form post action.
[`placeholder`](../../api/datepicker#placeholder) | Using `placeholder` you can display a short hint in the input element.
[`readonly`](../../api/datepicker#readonly)       | set `readonly` to stop editing the value in the input, but value can be included when form submit.

The following example demonstrates how to achieve the above described properties in the DatePicker.

{% tab template="datepicker/disable", isDefaultActive = "true",  sourceFiles="app/**/*.ts,app/**/template.html,styles.css" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    templateUrl: './app/template.html'
})
export class AppComponent {
}

```

{% endtab %}
