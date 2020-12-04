---
title: "Dynamically move input to edit mode"
component: "In-place Editor"
description: "Learn how to dynamically move input to edit mode in the Essential JS 2 In-place Editor component."
---

# Dynamically move input to edit mode

At component initial load, if you want to open editor state without interacting **In-place Editor** input element, it can be achieved by configuring the [enableEditMode](../../../api/inplace-editor/#enableeditmode) property to `true`.

In the following sample, editor opened at initial load and when toggling a checkbox, it will remove or open the editor.

{% tab template="in-place-editor/dynamic-edit", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { InPlaceEditorComponent } from '@syncfusion/ej2-angular-inplace-editor';
import {  ChangeEventArgs } from '@syncfusion/ej2-buttons';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
    <table class="table-section">
        <tr>
            <td> EnableEditMode: </td>
            <td>
                <ejs-checkbox id="enable" label="Enable" [checked]="true" (change)="onChange($event)"></ejs-checkbox>
             </td>
        </tr>
        <tr>
            <td class="sample-td"> Enter your name: </td>
            <td class="sample-td">
                <ejs-inplaceeditor #element id="element" mode="Inline" value="Andrew" enableEditMode="true" actionOnBlur="Ignore" [model]="model"></ejs-inplaceeditor>
            </td>
        </tr>
    </table>
</div>
    `
})

export class AppComponent {
    @ViewChild('element') editObj: InPlaceEditorComponent;
    public model: object = { placeholder: 'Enter some text' };
    public onChange(e: ChangeEventArgs): void {
        this.editObj.enableEditMode = e.checked;
        this.editObj.dataBind();
    }
}
```

{% endtab %}