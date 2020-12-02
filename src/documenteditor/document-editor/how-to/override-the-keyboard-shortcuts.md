---
title: "How to"
component: "DocumentEditor"
description: "Learn how to work with document editor in real time scenarios like create simple word processor, override keyboard shortcut behaviors, and more."
---

# How to override the keyboard shortcuts in document editor

Document editor triggers the [`keyDown`](../../api/document-editor/#keydown) event every time when any key is entered and provides an instance of [`DocumentEditorKeyDownEventArgs`](../../api/document-editor/documentEditorKeyDownEventArgs). You can use the [`isHandled`](../../api/document-editor/documentEditorKeyDownEventArgs/#ishandled) property to override the keyboard shortcut behaviour.

## Preventing default keyboard shortcut

The following code shows how to prevent the `CTRL + C` keyboard shortcut for copying selected content in document editor.

{% tab template="document-editor/prevent-keyboard",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, EditorService, DocumentEditorKeyDownEventArgs
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <ejs-documenteditor #document_editor style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSelection]=true [enableSfdtExport]=true [enableEditor]=true (keyDown)="onKeyDown($event)">
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SelectionService, EditorService, SfdtExportService]
})

export class AppComponent {

 public onKeyDown(args : DocumentEditorKeyDownEventArgs) :void {
    let keyCode: number = args.event.which || args.event.keyCode;
    let isCtrlKey: boolean = (args.event.ctrlKey || args.event.metaKey) ? true : ((keyCode === 17) ? true : false);
    //67 is the character code for 'C'
    if (isCtrlKey && keyCode === 67) {
        //To prevent copy operation set isHandled to true
        args.isHandled = true;
    }
 }
}
```

{% endtab %}

## Override or define the keyboard shortcut

Override or define a new keyboard shortcut behaviour instead of preventing the keyboard shortcut.

For example, `Ctrl + S` keyboard shortcut saves the document in SFDT format by default, and there is no behaviour for `Ctrl + Alt + S`. The following code demonstrates how to override the `Ctrl + S` shortcut to save a document in DOCX format and define `Ctrl + Alt + S` to save the document in SFDT format.

{% tab template="document-editor/override-keyboard",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SelectionService, EditorService, DocumentEditorKeyDownEventArgs, SfdtExportService, WordExportService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <ejs-documenteditor #document_editor style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSelection]=true [enableSfdtExport]=true [enableEditor]=true (keyDown)="onKeyDown($event)">
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SelectionService, EditorService, SfdtExportService, WordExportService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public onKeyDown(args : DocumentEditorKeyDownEventArgs) :void {
    let keyCode: number = args.event.which || args.event.keyCode;

    let isCtrlKey: boolean = (args.event.ctrlKey || args.event.metaKey) ? true : ((keyCode === 17) ? true : false);

    let isAltKey: boolean = args.event.altKey ? args.event.altKey : ((keyCode === 18) ? true : false);

   // 83 is the character code for 'S'
    if (isCtrlKey && !isAltKey && keyCode === 83) {
        //To prevent default save operation, set the isHandled property to true
        args.isHandled = true;
       this.documentEditor.save('sample', 'Docx');
       args.event.preventDefault();
    } else if (isCtrlKey && isAltKey && keyCode === 83) {
       this.documentEditor.save('sample', 'Sfdt');
    }
 }
}
```

{% endtab %}