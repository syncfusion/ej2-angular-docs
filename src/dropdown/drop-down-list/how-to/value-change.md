---
title: "Drop-down list How to detect value change"
component: "DropDownList"
description: "This section explains on how to detect whether the value change happened by manual or programmatic in drop-down list control."
---

# Detect whether the value change happened by manual or programmatic

You can check about whether value change happened by manual or programmatic by
using [`change`](../../api/drop-down-list/#change) event argument that argument name is `isInteracted`.

The following example demonstrate, how to check whether value change happened by manual or programmatic.

{% tab template="dropdownlist/manual-programmatic", sourceFiles="app/**/*.ts,template.html"  %}

```typescript
import { Component , ViewChild} from '@angular/core';
import { DropDownListComponent } from '@syncfusion/ej2-angular-dropdowns';

@Component({
    selector: 'app-root',
    // specifies the template path for DropDownList component
    templateUrl: `./template.html`
})
export class AppComponent {
    constructor() {
    }
    ngAfterViewInit(){
        document.getElementById('btn').onclick = () => {
            this.dropDownListObject.value = 'game3';
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
    public dropDownListObject: DropDownListComponent;
    onChange(args): void {
        let element: HTMLElement = document.createElement('p');
        if (args.isInteracted) {
            element.innerText = 'Changes happened by Interaction';
        } else {
            element.innerText = 'Changes happened by programmatic';
        }
        document.getElementById('event').append(element);
    }
}
```

{% endtab %}