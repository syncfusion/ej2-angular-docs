---
title: "Configuration"
component: "In-place Editor"
description: "Learn how to configure various renders, display modes, and configure the focus out actions in the Essential JS 2 In-place Editor component."
---

# Configuration

## Rendering modes

This section explains the supported rendering modes of the **In-place Editor**. Possible Rendering modes are as follows.

    * Popup
    * Inline

> By default, `Popup` mode will be rendered, when opening an editor.

* For `Popup` mode, editable container displays as like tooltip or popover above the element.

* For `Inline` mode, editable container displays as instead of the element. To render `Inline` mode while opening the editor, specify `mode` as `Inline`.

In the following sample, the **In-place Editor** renders with `Inline` mode. You can dynamically switch into another mode by changing the drop-down item value.

{% tab template="in-place-editor/modes", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { InPlaceEditorComponent, RenderMode } from '@syncfusion/ej2-angular-inplace-editor';
import { ChangeEventArgs } from '@syncfusion/ej2-dropdowns';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
        <table class="table-section">
            <tr>
                <td> Mode: </td>
                <td>
                    <ejs-dropdownlist #dropDown (change)="onChange($event)" id='dropDown' width="auto" [dataSource]='modeData' value='Inline' placeholder="Select Mode">
                    </ejs-dropdownlist>
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
  public model: Object = {  placeholder: 'Enter some text' };
  public modeData: string[] = ['Inline', 'Popup'];

  public onChange(e: ChangeEventArgs): void {
    const mode: RenderMode = e.itemData.value as RenderMode;
    this.editObj.mode = mode;
    this.editObj.dataBind();
  }
}

```

{% endtab %}

### Pop-up customization

**In-place Editor** popup mode can be customized by using the [title](../api/inplace-editor/popupSettings/#title) and [model](../api/inplace-editor/popupSettings/#model) properties in [popupSettings](../api/inplace-editor/popupSettings/) API.

Popup mode rendered by using the Essential JS 2 Tooltip component, so you can use tooltip properties and events to customize the behavior of popup via the [model](../api/inplace-editor/popupSettings/#model) property of [popupSettings](../api/inplace-editor/popupSettings/) API.

> For more details, refer the tooltip documentation [section](../tooltip/).

In the following sample, popup [title](../api/inplace-editor/popupSettings/#title) and [position](../api/tooltip/#position) customized using the [popupSettings](../api/inplace-editor/popupSettings/) property. All possible tooltip position data configured in the drop-down, if we change drop down item, selected value bound to [model](../api/inplace-editor/popupSettings/#model) property and applied it to [Tooltip](../tooltip/) component. `Tooltip` has following position options.

* TopLeft
* TopCenter
* TopRight
* BottomLeft
* BottomCenter
* BottomRight
* LeftTop
* LeftCenter
* LeftBottom
* RightTop
* RightCenter
* RightBottom

{% tab template="in-place-editor/popup", sourceFiles="app/**/*.ts,index.html,index.css" %}

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
                <td> Position: </td>
                <td>
                    <ejs-dropdownlist #dropDown (change)="onChange($event)" id='dropDown' width="auto" [dataSource]='positionData' value='BottomCenter' placeholder="Select a position" popupHeight="150px">
                    </ejs-dropdownlist>
                </td>
            </tr>
            <tr>
                <td  class="edit-heading sample-td"> Enter your name: </td>
                <td  class="sample-td">
                    <ejs-inplaceeditor #element id="element" mode="Popup" value="Andrew" [model]="model" [popupSettings]="popupSettingsModel"></ejs-inplaceeditor>
                </td>
            </tr>
        </table>
    </div>
    `
})

export class AppComponent {
  @ViewChild('element') editObj: InPlaceEditorComponent;
  public model: Object = {  placeholder: 'Enter some text' };
  public popupSettingsModel: object = { title: 'Enter name', model : { position: 'BottomCenter' }};
  public positionData: string[] = ['TopLeft', 'TopCenter',
  'TopRight', 'BottomLeft', 'BottomCenter', 'BottomRight', 'LeftTop', 'LeftCenter', 'LeftBottom', 'RightTop', 'RightCenter', 'RightBottom'];

  public onChange(e: ChangeEventArgs): void {
    this.editObj.popupSettings.model.position = e.value as string;
    this.editObj.dataBind();
  }
}

```

{% endtab %}

## Event actions for editing

The event action of the editor that enable in the edit mode based on the [editableOn](../api/inplace-editor/#editableon) property, by default `Click` is assigned, the following options are also supported.

* **[Click](../api/inplace-editor/editableType/)**:  The editor will be opened as single click actions.
* **[DblClick](../api/inplace-editor/editableType/)**: The editor will be opened as double-click actions and it is not applicable for edit icon.
* **[EditIconClick](../api/inplace-editor/editableType/)**: Disables the editing of event action of input and allows user to edit only through edit icon.

> **In-place Editor** get focus by pressing the `tab` key from previous focusable DOM element and then by pressing `enter` key, the editor will be opened.

In the following sample, when switching drop-down item, the selected value assigned to the `editableOn` property. If you changed to `DblClick`, the editor will open when making a double click on the input.

{% tab template="in-place-editor/editable-on", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { InPlaceEditorComponent, EditableType } from '@syncfusion/ej2-angular-inplace-editor';
import { ChangeEventArgs } from '@syncfusion/ej2-dropdowns';

@Component({
    selector: 'app-root',
    template: `
       <div id='container'>
        <table class="table-section">
            <tr>
                <td> EditableOn: </td>
                <td>
                    <ejs-dropdownlist #dropDown (change)="onChange($event)" id='dropDown' width="auto" [dataSource]='editableOnData' value='Click' placeholder="Select edit type">
                    </ejs-dropdownlist>
                </td>
            </tr>
            <tr>
                <td  class="sample-td"> Enter your name: </td>
                <td  class="sample-td">
                    <ejs-inplaceeditor #element id="element" mode="Inline" value="Andrew" [model]="model"></ejs-inplaceeditor>
                </td>
            </tr>
        </table>
    </div>
    `
})

export class AppComponent {
  @ViewChild('element') editObj: InPlaceEditorComponent;
  public model: Object = {  placeholder: 'Enter some text' };
  public editableOnData: string[] = ['Click', 'DblClick', 'EditIconClick'];

  public onChange(e: ChangeEventArgs): void {
    let editType: EditableType = e.itemData.value as EditableType;
    this.editObj.editableOn = editType;
    this.editObj.dataBind();
  }
}
```

{% endtab %}

## Action on focus out

Action to be performed when the user clicks outside the container, that means focusing out of editable content and it can be handled by the [actionOnBlur](../api/inplace-editor/#actiononblur) property, by default `Submit` assigned. It also has the following options.

* **[Cancel](../api/inplace-editor/actionBlur/)**: Cancels the editing and resets the old content.
* **[Submit](../api/inplace-editor/actionBlur/)**: Submits the edited content to the server.
* **[Ignore](../api/inplace-editor/actionBlur/)**: No action is performed with this type and allows to edit multiple editors.

In the following sample, when switching drop-down item, the selected value assigned to the `actionOnBlur` property.

{% tab template="in-place-editor/action-on-blur", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { InPlaceEditorComponent, ActionBlur } from '@syncfusion/ej2-angular-inplace-editor';
import { ChangeEventArgs } from '@syncfusion/ej2-dropdowns';

@Component({
    selector: 'app-root',
    template: `
       <div id='container'>
    <table class="table-section">
        <tr>
            <td> ActionOnBlur: </td>
            <td>
                <div id="dropDown"></div>
                <ejs-dropdownlist #dropDown (change)="onChange($event)" id='dropDown' width="auto" [dataSource]='blurActionData' value='Submit' placeholder="Select blur action">
                </ejs-dropdownlist>
            </td>
        </tr>
        <tr>
            <td  class="sample-td"> Enter your name: </td>
            <td  class="sample-td">
                <ejs-inplaceeditor #element id="element" mode="Inline" value="Andrew" [model]="model"></ejs-inplaceeditor>
            </td>
        </tr>
    </table>
</div>
    `
})

export class AppComponent {
  @ViewChild('element') editObj: InPlaceEditorComponent;
  public model: Object = {  placeholder: 'Enter some text' };
  public blurActionData: string[] = ['Submit', 'Cancel', 'Ignore'];

  public onChange(e: ChangeEventArgs): void {
    let editType: ActionBlur = e.itemData.value as ActionBlur;
    this.editObj.actionOnBlur = editType;
    this.editObj.dataBind();
  }
}

```

{% endtab %}

## Display modes

By default, **In-place Editor** input element highlighted with a dotted underline. To remove dotted underline from input element, add `data-underline="false"` attribute at **In-place Editor** root element.

The following sample, denotes intractable and normal display modes with different samples.

{% tab template="in-place-editor/under-line", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';
import { InPlaceEditorComponent } from '@syncfusion/ej2-angular-inplace-editor';

@Component({
    selector: 'app-root',
    template: `
       <div id='container'>
    <h4>Example of data-underline attribute</h4>
    <table class="table-section">
        <tr>
            <td class="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> Intractable UI </td>
            <td class="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                <ejs-inplaceeditor id="default" mode="Inline" value="Andrew" [model]="model"></ejs-inplaceeditor>
            </td>
        </tr>
        <tr>
            <td class="col-lg-6 col-md-6 col-sm-6 col-xs-6 control-title"> Normal UI </td>
            <td class="col-lg-6 col-md-6 col-sm-6 col-xs-6">
                <ejs-inplaceeditor id="inline" data-underline="false" mode="Inline" value="Andrew" [model]="model"></ejs-inplaceeditor>
            </td>
        </tr>
    </table>
</div>
    `
})

export class AppComponent {
  public model: Object = {  placeholder: 'Enter some text' };
}
```

{% endtab %}

## See Also

* [Types of rendering the editor](./how-to/disable-edit-mode/)
* [Animate the editor during popup mode](./how-to/custom-animation/)