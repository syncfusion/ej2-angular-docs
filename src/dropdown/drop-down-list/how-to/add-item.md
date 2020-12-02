---
title: "Drop-down list How to add list item"
component: "DropDownList"
description: "This section explains on how to add list item to the Syncfusion Angular drop-down list component."
---

# Add item in between in DropDownList

You can add item in between based on item [`index`](../../api/drop-down-list#index).
If you add new item without item index, item will be added as last item in list.

The following example demonstrate how to add item in between in DropDownList.

{% tab template="dropdownlist/add-item", sourceFiles="app/**/*.ts,add.html"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { DropDownListComponent } from '@syncfusion/ej2-angular-dropdowns';

@Component({
    selector: 'control-content',
    // specifies the template path for DropDownList component
    templateUrl: `./add.html`
})
export class AppComponent {
    constructor() {
    }
    ngAfterViewInit() {
         // add item at first
        document.getElementById('first').onclick = () => {
            this.dropDownListObject.addItem({Id: 'game0', Game: 'Hockey'}, 0);
        }

        // add item in between
        document.getElementById('between').onclick = () => {
            this.dropDownListObject.addItem({Id: 'game4', Game: 'Golf'}, 2);
        }

        // add item at last
        document.getElementById('last').onclick = () => {
            this.dropDownListObject.addItem({Id: 'game5', Game: 'Cricket'});
        }
    }
    // defined the array of data
    public data: { [key: string]: Object }[] = [ { Id: 'game1', Game: 'Badminton' },
                 { Id: 'game2', Game: 'Football' }, { Id: 'game3', Game: 'Tennis' }];
    // maps the appropriate column to fields property
    public fields: Object = { text: 'Game', value: 'Id' };
    //set the placeholder to DropDownList input
    public text: string = "Select a game";
    @ViewChild('ddlelement')
    public dropDownListObject = DropDownListComponent;
}
```

{% endtab %}