---
title: "Integrate HTML5 components"
component: "In-place Editor"
description: "Learn how to configure template and integrate HTML5 components, get and pass a modified value to the server in the Essential JS 2 In-place Editor component."
---

# Integrate HTML5 components (Template)

The **In-place Editor** supports adding HTML5 input components using the [template](../api/inplace-editor/#template) property. The Template property can be given as either a `string` or a `query selector`.

## As a string

The HTML element tag can be given as a string for the template property. Here, the input is rendered as an HTML template.

```typescript
template: "<div><input type='text' id='name'></input></div>"

```

## As a ng-template

You can render other components inside **In-place editor** using Angular `ng-template`. We need to use `ng-template` inside the `<ejs-inplaceeditor>` tag with `#template` attribute, which is mandatory to render that template.

```typescript
<ng-template #template>
    <input id="date" value="2018-05-23" type="date">
</ng-template>

```

Template mode, the `value` property not handled by the **In-place Editor** component. So, before sending a value to the server, you need to modify at [actionBegin](../api/inplace-editor/#actionbegin) event, otherwise, an empty string will pass. In the following template sample, before submitting a data to the server, event argument and [value](../api/inplace-editor/#value) property content updated in the `actionBegin` event handler.

{% tab template="in-place-editor/html-template", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { InPlaceEditorComponent, ActionBeginEventArgs } from '@syncfusion/ej2-angular-inplace-editor';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
        <span class="content-title"> Select date: </span>
        <ejs-inplaceeditor #element id="element" mode="Inline" value="2018-05-23" (actionBegin)="actionBegin($event)">
            <ng-template #template>
                <input id="date" value="2018-05-23" type="date">
            </ng-template>
        </ejs-inplaceeditor>
    </div>
    `
})

export class AppComponent {
    @ViewChild('element') editObj: InPlaceEditorComponent;
    public actionBegin(e: ActionBeginEventArgs): void {
        const value = (<any>this.editObj.element.querySelector('#date')).value;
        this.editObj.value = value;
        (<any>e).value = value;
    }
}

```

{% endtab %}