---
title: "Undo and redo"
component: "DocumentEditor"
description: "Learn how undo and redo can be done in JavaScript document editor and how to customize its limit."
---

# History

Document editor tracks the history of all editing actions done in the document, which allows undo and redo functionality.

## Enable or disable history

Inject the `EditorHistory` module in your application to provide history preservation functionality for `DocumentEditor`. Refer to the following code example.

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { DocumentEditorComponent, SfdtExportService, SelectionService,  EditorService, EditorHistoryService} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSelection]=true [enableEditor]=true [enableEditorHistory]=true >
    </ejs-documenteditor>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService,  EditorService, EditorHistoryService]
})

export class AppComponent {

}
```

You can enable or disable history preservation for a document editor instance any time using the ‘enableEditorHistory’ property. Refer to the following sample code.

```typescript
this.documentEditor.enableEditorHistory = false;
```

## Undo and redo

You can perform undo and redo by `CTRL+Z` and `CTRL+Y` keyboard shortcuts. Document editor exposes API to do it programmatically.
To undo the last editing operation in document editor, refer to the following sample code.

```typescript
this.documentEditor.editorHistory.undo();
```

To redo the last undone action, refer to the following code example.

```typescript
this.documentEditor.editorHistory.redo();
```

## Stack size

History of editing actions will be maintained in stack, so that the last item will be reverted first. By default, document editor limits the size of undo and redo stacks to 500 each respectively. However, you can customize this limit. Refer to the following sample code.

```typescript
this.documentEditor.editorHistory.undoLimit = 400;
this.documentEditor.editorHistory.redoLimit = 400;
```

## See Also

* [Feature modules](../document-editor/feature-module/)
* [Keyboard shortcuts](../document-editor/keyboard-shortcut/)