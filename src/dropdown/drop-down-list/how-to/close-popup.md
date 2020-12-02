---
title: "Drop-down list How to close popup on scroll"
component: "DropDownList"
description: "This section explains on how to close popup on scroll in the Syncfusion Angular drop-down list component."
---

# Close the popup on scroll

By using the `hidePopup` method in DropDownList, you can close the popup on scroll when triggered the windows scroll event.

The following example demonstrate about how to close the popup on scroll.

{% tab template="dropdownlist/getting-started", sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { DropDownListComponent } from '@syncfusion/ej2-angular-dropdowns';

@Component({
    selector: 'app-root',
    // specifies the template string for the DropDownList component with change event
    template: `<ejs-dropdownlist #ddlelement id='ddlelement' #samples [dataSource]='data' [placeholder]='placeholder'></ejs-dropdownlist>`
})
export class AppComponent {
    constructor() {
        // bind the onscroll event to window
        window.onscroll = () => {
            this.dropDownListObject.hidePopup();
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