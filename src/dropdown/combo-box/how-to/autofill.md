---
title: "Combo box autofill"
component: "ComboBox"
description: "This section explains how to acheive autofill functionality in combo box control."
---

# Autofill supports with ComboBox

The ComboBox supports the `autofill` behaviour with the help
of [autofill](../../api/combo-box#autofill) property. Whenever you change the input value,
the ComboBox will autocomplete your data by matching the typed character. Suppose, if no matches
found then, comboBox doesn't suggest any item.

The following examples, showcase that how to work autofill with ComboBox.

{% tab template="combobox/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // specifies the template string for enable the autofill in ComboBox component
    template: `<ejs-combobox id='comboelement' #samples [dataSource]='data' [autofill]='true' [placeholder]='text'></ejs-combobox>`
})
export class AppComponent {
    constructor() {
    }
    // defined the array of data
    public data: string[] = ['Badminton', 'Basketball', 'Cricket', 'Golf', 'Hockey', 'Rugby'];
    // set placeholder text to ComboBox input element
    public text: string = 'Select a game';
}
```

{% endtab %}
