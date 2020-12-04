---
title: "Server actions"
component: "In-place Editor"
description: "Learn how to modify and submit a value to the server, and handle success and failure events in the Essential JS2 In-place Editor component."
---

# Server actions

By passing **In-place Editor** component value to the server, the [primaryKey](../api/inplace-editor/#primarykey) property value must require, otherwise action not performed for remote data.

If the [URL](../api/inplace-editor/#url) property value is empty, data passing will handled at local and also the [actionSuccess](../api/inplace-editor/#actionsuccess) event will trigger with `null` as argument value.

> The following arguments are passed to the server when submit actions perform.

| Arguments  | Explanations                                              |
|------------|-----------------------------------------------------------|
| value      | For processing edited value, like DB value updating.      |
| primaryKey | For value mapping to the server, like selecting DB.            |
| name       | For field mapping to the server, like DB column field mapping. |

Find the following sample server codes for defining models and controller functions to configure processing data.

```C#
    public class SubmitModel
        {
            public string Name { get; set; }
            public string PrimaryKey { get; set; }
            public string Value { get; set; }
        }
```

```C#

public IEnumerable<SubmitModel> UpdateData([FromBody]SubmitModel value)
        {
         // User can process data
          return value;
        }

```

* Server actions successfully done, the [actionSuccess](../api/inplace-editor/#actionsuccess) event will be fired with returned server data.

* If the server is not responding, the [actionFailure](../api/inplace-editor/#actionfailure) event will be fired with data, but value not updated in the Editor.

In the following sample, the `actionSuccess` event will trigger once the value submitted successfully into the server. In this sample, both `actionSuccess` and `actionFailure` were configured and resulted value will be converted to chips.

{% tab template="in-place-editor/server-actions", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { InPlaceEditorComponent, ActionEventArgs } from '@syncfusion/ej2-angular-inplace-editor';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
        <span class="content-title"> Select frameworks: </span>
        <ejs-inplaceeditor #element id="element" data-underline="false" type="MultiSelect" mode="Inline" [value]="value" [model]="model" name="skill" [url]="url" primaryKey="FrameWork" adaptor="UrlAdaptor" (created)="created()" (actionSuccess)="actionSuccess($event)" (actionFailure)="actionFailure($event)"></ejs-inplaceeditor>
    </div>
    `
})

export class AppComponent {
    @ViewChild('element') editObj: InPlaceEditorComponent;
    public value: string[] =  ['JavaScript', 'jQuery'];
    public url = 'https://ej2services.syncfusion.com/development/web-services/api/Editor/UpdateData';
    public frameWorkList: string[] = ['Android', 'JavaScript', 'jQuery', 'TypeScript', 'Angular', 'React', 'Vue', 'Ionic'];
    public model: object = { mode: 'Box', dataSource: this.frameWorkList, placeholder: 'Select skill' };
    chipOnCreate() {
        this.editObj.element.querySelector('.e-editable-value').innerHTML = this.chipCreation(this.editObj.value, true);
    }
    public actionSuccess(e: ActionEventArgs): void {
        e.value = this.chipCreation(e.value.split(','), true);
    }
    public actionFailure(e: ActionEventArgs): void {
        e.value = this.chipCreation(e.value.split(','), false);
    }
    public created(): void {
        this.chipOnCreate();
    }
    chipCreation(data, isSuccess): string {
        let value = '<div class="e-chip-list">';
        [].slice.call(data).forEach((val: string) => {
            value += '<div class="e-chip"> <span class="e-chip-text' + (!isSuccess ? 'e-highlight' : '') + '"> ' + val + '</span></div>';
        });
        value += '</div>';
        return value;
    }
}
```

{% endtab %}