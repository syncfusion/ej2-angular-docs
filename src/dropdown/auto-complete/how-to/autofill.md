---
title: "Autocomplete autofill"
component: "AutoComplete"
description: "This section explains how to acheive autofill functionality in autocomplete control."
---

# Autofill supported with AutoComplete

The AutoComplete supports the autofill behavior with the help of
[`autofill`](../../api/auto-complete/#autofill) property. Whenever you change the
input value, the AutoComplete will autocomplete your data by matching the typed
character. Suppose, if no matches found then, AutoComplete doesn't suggest any item.

In the below sample, showcase that how to work `autofill` with AutoComplete.

{% tab template="autocomplete/getting-started", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the AutoComplete component
    template: `<ejs-autocomplete id='atcelement' [dataSource]='searchData' [fields]='fields' [placeholder]='text' [autofill]='autofill'></ejs-autocomplete>`
})

export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public searchData: { [key: string]: Object }[] = [
    { Name: 'Australia', Code: 'AU' },
    { Name: 'Bermuda', Code: 'BM' },
    { Name: 'Canada', Code: 'CA' },
    { Name: 'Cameroon', Code: 'CM' },
    { Name: 'Denmark', Code: 'DK' },
    { Name: 'France', Code: 'FR' },
    { Name: 'Finland', Code: 'FI' },
    { Name: 'Germany', Code: 'DE' },
    { Name: 'Greenland', Code: 'GL' },
    { Name: 'Hong Kong', Code: 'HK' },
    { Name: 'India', Code: 'IN' },
    { Name: 'Italy', Code: 'IT' },
    { Name: 'Japan', Code: 'JP' },
    { Name: 'Mexico', Code: 'MX' },
    { Name: 'Norway', Code: 'NO' },
    { Name: 'Poland', Code: 'PL' },
    { Name: 'Switzerland', Code: 'CH' },
    { Name: 'United Kingdom', Code: 'GB' },
    { Name: 'United States', Code: 'US' }];
    // maps the appropriate column to fields property
    public fields: Object = { value: "Name" };
    // set the placeholder to the AutoComplete input
    public text: string = "Find a country";
    //enable the highlight property to highlight the matched character in suggestion list
    public autofill: Boolean = true;
}

```

{% endtab %}