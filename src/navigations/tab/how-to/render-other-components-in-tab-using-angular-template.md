---
title: "Tab How To sections"
component: "Tab"
description: "This example demonstrates how to render other Essential JS 2 components in Essential JS 2 Tab component using ng-template."
---

# Render other components in Tab using ng-template

You can render other components inside Tab using Angular **ng-template**. Through this, we can add content as other components directly with
all their functionalities to our Tab. We need to use `ng-template` inside the each `e-tabitem` tag with `#content` attribute, which is
mandatory to render content. And now use `ng-template` tag with select attribute of id or class name for mapping required content.

{% tab template="tab/direct-components", sourceFiles="app/**/*.ts,index.css"%}

```typescript

import { Component, ViewChild } from '@angular/core';
import { enableRipple, createElement } from '@syncfusion/ej2-base';
import { TabComponent, selectEventArgs } from '@syncfusion/ej2-angular-navigations';
import { ComboBoxComponent } from '@syncfusion/ej2-angular-dropdowns';
import { CalenderComponent } from '@syncfusion/ej2-angular-calendars';

enableRipple(true);

@Component({
    selector: 'app-container',
    template: `<ejs-tab id="element">
    <e-tabitems>
        <e-tabitem>
            <ng-template #headerText>

                <div> Tab1 </div>

            </ng-template>
            <ng-template #content>

                <ejs-calendar></ejs-calendar>

            </ng-template>

        </e-tabitem>
        <e-tabitem>
            <ng-template #headerText>

                <div> Tab2 </div>

            </ng-template>
            <ng-template #content>

                <ejs-combobox id='comboelement' #samples [dataSource]='data' [placeholder]='text'></ejs-combobox>

            </ng-template>
        </e-tabitem>
        <e-tabitem>
            <ng-template #headerText>

                <div> Tab3 </div>

            </ng-template>
            <ng-template #content>

                <p>text inside tab3</p>

            </ng-template>

        </e-tabitem>
    </e-tabitems>
</ejs-tab>`
})

export class AppComponent {
    @ViewChild('element') tabInstance: TabComponent;

    // defined the array of data
    public data: string[] = ['Badminton', 'Basketball', 'Cricket', 'Golf', 'Hockey', 'Rugby'];
    // set placeholder text to ComboBox input element
    public text: string = 'Select a game';

}

```

{% endtab %}
