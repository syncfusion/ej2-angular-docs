---
title: "Custom indication for unsaved value"
component: "In-place Editor"
description: "Learn how to add a custom indication to the unsaved value of the Essential JS 2 In-place Editor component."
---

# Add custom indication to unsaved value

You can add custom indication to unsaved input value by using the [actionSuccess](../../../api/inplace-editor/#actionsuccess) event, when data not submitted to the server.

In this sample, the `actionSuccess` event configured and the [URL](../../../api/inplace-editor/#url) property not included. Then submit button clicked, the current editor value saved into input and data sending to server action prevented due to the `URL` property not configured.

But `actionSuccess` event will trigger the handler function with `null` argument values. In handler function data property [primaryKey](../../../api/inplace-editor/#primarykey) value checked, whether it empty or not. If it is empty custom class, added in the `e-value-wrapper` element to customize its styles.

> To send input value to local, set the `URL` property as empty.

{% tab template="in-place-editor/custom-indication", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';
import { InPlaceEditorComponent, ActionEventArgs } from '@syncfusion/ej2-angular-inplace-editor';
import { isNullOrUndefined as isNOU } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
        <span class="content-title"> Enter your name: </span>
        <ejs-inplaceeditor #element id="element" mode="Inline" value="Andrew" [model]="model" (actionSuccess)="actionSuccess($event)"></ejs-inplaceeditor>
    </div>
    `
})

export class AppComponent {
    public model: object = { placeholder: 'Enter some text' };
    public actionSuccess(e: ActionEventArgs): void {
        let pk: string = e.data['PrimaryKey'];
        if (isNOU(pk) || pk === '') {
            document.querySelector('.e-editable-value').classList.add('e-send-error');
        }
    }
}

```

{% endtab %}