---
title: "How To"
component: "DateRangePicker"
description: "Miscellaneous aspects of customizing the date range picker"
---

# Disable, Placeholder, Read-only

Property | Purpose
-----|-----
 [`enabled`](../../api/daterangepicker#enabled) | The component can be restricted on a page, by setting `enabled` value as **false** which will disable the component completely from all user interactions including in form post action.
[`placeholder`](../../api/daterangepicker#placeholder) | Using `placeholder` you can display a short hint about the expected value in the input element.
[`readonly`](../../api/daterangepicker#readonly)       | Editing the value in the component can be prevented by setting `readonly` as **true**, but value can be included in the form post action.

{% tab template="daterangepicker/getting-started", isDefaultActive = "true",  sourceFiles="app/**/*.ts,styles.css,app/**/template.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    templateUrl: './app/template.html'
})
export class AppComponent {
    public value: Date[] = [new Date('1/1/2020'), new Date('2/1/2023')];
}

```

{% endtab %}