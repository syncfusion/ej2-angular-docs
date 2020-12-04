---
title: "Custom animation for popup mode"
component: "In-place Editor"
description: "Learn how to configure custom animation for popup and customize it dynamically in the Essential JS 2 In-place Editor component."
---

# Set custom animation for popup mode

In popup mode, the **In-place Editor** rendered with the Essential JS 2 `Tooltip` component. You can use tooltip properties and events to customize the popup by configure properties into the [model](../../../api/inplace-editor/popupSettings/#model) property inside the [popupSettings](../../../api/inplace-editor/popupSettings/) API.

In the following sample, popup animation can be customized by passing animation effect using the `model` property and the dynamic animation effect changes configured from the Essential JS 2 `DropDownList` component `change` event.

{% tab template="in-place-editor/custom-animation", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { InPlaceEditorComponent } from '@syncfusion/ej2-angular-inplace-editor';
import { ChangeEventArgs } from '@syncfusion/ej2-dropdowns';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
    <table class="table-section">
        <tr>
            <td> Open Animation: </td>
            <td>
                <div id="openDropDown"></div>
                <ejs-dropdownlist #openDropDown (change)="onChange($event)" id='openDropDown' [dataSource]='openAnimateData' value='ZoomIn' placeholder="Select a animate type" popupHeight="150px">
                </ejs-dropdownlist>
            </td>
        </tr>
        <tr>
            <td  class="sample-td"> Enter your name: </td>
            <td  class="sample-td">
                <ejs-inplaceeditor #element id="element" mode="Popup" value="Andrew" [model]="model" [popupSettings]="popupSettings"></ejs-inplaceeditor>
            </td>
        </tr>
    </table>
</div>
    `
})

export class AppComponent {
    @ViewChild('element') editObj: InPlaceEditorComponent;
    public model: object = { placeholder: 'Enter some text' };
    public popupSettings: object = { model: { animation: { open: {effect: 'ZoomIn', duration: 1000, delay: 0}}}};
    public openAnimateData: string[] = ['None', 'FadeIn', 'FadeZoomIn', 'ZoomIn'];

    public onChange(e: ChangeEventArgs): void {
        this.editObj.popupSettings.model.animation.open.effect = e.value;
        this.editObj.dataBind();
    }
}

```

{% endtab %}