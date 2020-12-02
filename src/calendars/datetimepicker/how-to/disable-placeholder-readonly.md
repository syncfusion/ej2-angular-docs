---
title: "How To"
component: "DateTimePicker"
description: "Miscellaneous aspects of customizing the date time picker"
---

# Disable, Placeholder, Read-only

Property | Purpose
-----|-----
 [`enabled`](../../api/datetimepicker#enabled) | The component can be restricted on a page, by setting `enabled` value as **false** which will disable the component completely from all user interactions including in form post action.
[`placeholder`](../../api/datetimepicker#placeholder) | Using `placeholder` you can display a short hint about the expected value in the input element.
[`readonly`](../../api/datetimepicker#readonly)       | Editing the value in the component can be prevented by setting `readonly` as **true**, but value can be included in the form post action.

{% tab template="datetimepicker/accessibility", sourceFiles="app/**/*.ts,app/**/template.html,styles.css", isDefaultActive=true %}

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
