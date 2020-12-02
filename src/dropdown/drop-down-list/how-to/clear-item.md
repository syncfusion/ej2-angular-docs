---
title: "Drop-down list How to clear the list item"
component: "DropDownList"
description: "This section explains on how to clear the selected items of the Syncfusion Angular drop-down list component."
---

# Clear the selected item in DropDownList

You can clear the selected item in the below two different ways.

By clicking on the `clear icon` which is shown in DropDownList element, you can clear the selected item in
DropDownList through **interaction**. By using [`showClearButton`](../../api/drop-down-list/#showclearbutton)
property, you can enable the clear icon in DropDownList element.

Through **programmatic** you can set `null` value to anyone of the index, text or value property to clear the selected item in DropDownList.

The following example demonstrate about how to clear the selected item in DropDownList.

{% tab template="dropdownlist/clear-item", sourceFiles="app/**/*.ts,clear.html"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { DropDownListComponent } from '@syncfusion/ej2-angular-dropdowns';
import { Button } from '@syncfusion/ej2-buttons';

@Component({
    selector: 'control-content',
    // specifies the template string for the DropDownList component with change event
    templateUrl: `./clear.html`
})
export class AppComponent {
    constructor() {
    }
    ngAfterViewInit() {
      // Set null value to value property for clear the selected item
        document.getElementById('btn').onclick = () => {
          this.dropDownListObject.value = null;
        }
    }
    // defined the array of data
    public data: string[] = ['Badminton', 'Basketball', 'Cricket', 'Golf', 'Hockey', 'Rugby'];
    // set placeholder text to DropDownList input element
    public placeholder: string = 'Select a game';
     @ViewChild('ddlelement')
    public dropDownListObject: DropDownListComponent;
}
```

{% endtab %}