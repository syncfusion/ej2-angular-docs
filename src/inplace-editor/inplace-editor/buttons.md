---
title: "Buttons"
component: "In-place Editor"
description: "Learn how to show or hide buttons, customize its behavior, and the appearance in the Essential JS 2 In-place Editor component."
---

# Buttons

The **In-place Editor** has an option to save and cancel using buttons. The [saveButton](../api/inplace-editor/#savebutton) and [cancelButton](../api/inplace-editor/#cancelbutton) properties accept the [ButtonModel](../api/button/buttonModel/) objects for customizing the save and cancel button properties.

Buttons can be show or hide by sets a Boolean value to the [showButtons](../api/inplace-editor/#showbuttons) property.

> Without buttons value will be processed via the following ways.

* **[actionOnBlur](../api/inplace-editor/#actiononblur)**: By clicking out side the editor component get focus out and do action based on this property value.
* **[submitOnEnter](../api/inplace-editor/#submitonenter)**: Pressing `Enter` key it performs the submit action, if this property set to `true`.

In the following sample, the [content](../api/button#content) and [cssClass](../api/button#cssclass) properties of `Button` value assigned to the [saveButton](../api/inplace-editor/#savebutton) and [cancelButton](../api/inplace-editor/#cancelbutton) properties to customize its appearance. Also check or uncheck a checkbox buttons render or removed from the editor.

To restrict either save or cancel button rendering into a DOM, simply pass empty object `{}` in the  `saveButton` or `cancelButton` properties.

> For more details about buttons, refer this documentation [section](../button/).

{% tab template="in-place-editor/show-buttons", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { InPlaceEditorComponent } from '@syncfusion/ej2-angular-inplace-editor';
import { ChangeEventArgs } from '@syncfusion/ej2-buttons';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
    <table class="table-section">
        <tr>
            <td> ShowButtons: </td>
            <td>
                <ejs-checkbox label="Show" [checked]="true" (change)="onChange($event)"></ejs-checkbox>
            </td>
        </tr>
        <tr>
            <td  class="sample-td"> Enter your name: </td>
            <td  class="sample-td">
                <ejs-inplaceeditor #element id="element" mode="Inline" value="Andrew" [model]="model" [saveButton]="saveButton" [cancelButton]="cancelButton"></ejs-inplaceeditor>
            </td>
        </tr>
    </table>
</div>
    `
})

export class AppComponent {
  @ViewChild('element') editorObj: InPlaceEditorComponent;
  public model: Object = {  placeholder: 'Enter some text' };
  public saveButton: object = { content: 'Ok', cssClass: 'e-outline'};
  public cancelButton: object = { content: 'Cancel', cssClass: 'e-outline'};

  public onChange(e: ChangeEventArgs): void {
    this.editorObj.showButtons = e.checked;
    this.editorObj.dataBind();
  }
}

```

{% endtab %}

## See Also

* [In-place editor buttons](./how-to/dynamic-edit-mode/)