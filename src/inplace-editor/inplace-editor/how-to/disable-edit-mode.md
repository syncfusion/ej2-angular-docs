---
title: "Disable the edit mode specifically"
component: "In-place Editor"
description: "Learn how to disable the edit mode in the Essential JS 2 In-place Editor component."
---

# Disable the edit mode specifically

The edit mode of **In-place Editor** can be disabled by setting the [disabled](../../../api/inplace-editor/#disabled) property value to `true`. In the following sample, when check or uncheck the checkbox, **In-place Editor** component will disable or enable the edit mode.

{% tab template="in-place-editor/disable-edit", sourceFiles="app/**/*.ts,index.html,index.css" %}

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
            <td> Disabled: </td>
            <td>
                <ejs-checkbox id="enable" label="Disable" [checked]="false" (change)="onChange($event)"></ejs-checkbox>
            </td>
        </tr>
        <tr>
            <td class="sample-td"> Enter your name: </td>
            <td class="sample-td">
                <ejs-inplaceeditor #element id="element" mode="Inline" value="Andrew" [model]="model"></ejs-inplaceeditor>
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
        this.editObj.disabled = e.checked;
        this.editObj.dataBind();
    }
}

```

{% endtab %}