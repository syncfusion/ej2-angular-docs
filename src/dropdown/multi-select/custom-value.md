---
title: "Multiselect Custom value"
component: "MultiSelect"
description: "This section for Syncfusion angular multiselect component demonstrates the addition of a new value that is not present in the predefined list."
---

# CustomValue

The MultiSelect allows user to add a new non-present option to the component value when
[`allowCustomValue`](../api/multi-select/#allowcustomvalue) is enabled. while selecting the new custom value
[`customValueSelection`](../api/multi-select/#customvalueselection) event will be triggered.

The following sample demonstrates configuration of custom value support with the MultiSelect component.

{% tab template="multiselect/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for the MultiSelect component
    template: `<ejs-multiselect id='multiselectelement' [dataSource]='sportsData' [fields]='fields' [allowCustomValue]='true' [placeholder]='placeholder'></ejs-multiselect>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public sportsData: { [key: string]: Object }[] = [
    { id: 'game1', sports: 'Badminton' },
    { id: 'game2', sports: 'Football' },
    { id: 'game3', sports: 'Tennis' }
    ];
    // map the appropriate column
    public fields: Object = { text: 'sports', value: 'id' };
    // set the placeholder to the MultiSelect input
    public placeholder: string = 'Select games';
}

```

{% endtab %}