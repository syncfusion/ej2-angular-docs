---
title: "Hyperlink"
component: "DocumentEditor"
description: "Learn how to insert, delete, or navigate links in JavaScript document editor."
---

# Hyperlink

Document editor supports hyperlink field. You can link a part of the document content to Internet or file location, mail address, or any text within the document.

## Navigate a hyperlink

Document editor triggers `requestNavigate` event whenever user clicks Ctrl key or tap a hyperlink within the document. This event provides necessary details about link type, navigation URL, and local URL (if any) as arguments, and allows you to easily customize the hyperlink navigation functionality. Refer to the following example.

{% tab template="document-editor/link",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent,  SfdtExportService, SelectionService, RequestNavigateEventArgs
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <ejs-documenteditor #document_editor style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSelection]=true [enableSfdtExport]=true [enableEditor]=true (requestNavigate)="onRequestNavigate($event)">
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [ SfdtExportService, SelectionService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public onRequestNavigate(args : DocumentEditorKeyDownEventArgs) :void {
    if (args.linkType !== 'Bookmark') {
         let link: string = args.navigationLink;
        if (args.localReference.length > 0) {
            link += '#' + args.localReference;
        }
        window.open(link);
        args.isHandled = true;
    }
}
}
```

{% endtab %}

If the selection is in hyperlink, trigger this event by calling `navigateHyperlink` method of `Selection` instance. Refer to the following example.

```typescript
this.documentEditor.selection.navigateHyperlink();
```

## Copy link

Document editor copies link text of a hyperlink field to the clipboard if the selection is in hyperlink. Refer to the following example.

```typescript
this.documentEditor.selection.copyHyperlink();
```

## Add hyperlink

To create a basic hyperlink in the document, press `ENTER` / `SPACEBAR` / `SHIFT + ENTER` / `TAB` key after typing the address, for instance `http://www.google.com`. Document editor automatically converts this address to a hyperlink field. The text can be considered as a valid URL if it starts with any of the following.

> `<http://>`<br>
> `<https://>`<br>
> `file:///`<br>
> `www.`<br>
> `mailto:`<br>

Refer to the following example.

{% tab template="document-editor/link",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent,   SfdtExportService, SelectionService, EditorService, RequestNavigateEventArgs
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <ejs-documenteditor #document_editor style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSelection]=true  [enableEditor]=true (requestNavigate)="onRequestNavigate($event)">
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [ SfdtExportService, SelectionService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public onRequestNavigate(args : DocumentEditorKeyDownEventArgs) :void {
    if (args.linkType !== 'Bookmark') {
         let link: string = args.navigationLink;
        if (args.localReference.length > 0) {
            link += '#' + args.localReference;
        }
        window.open(link);
        args.isHandled = true;
    }
}
}
```

{% endtab %}

## Remove hyperlink

To remove link from hyperlink in the document, press Backspace key at the end of a hyperlink. By removing the link, it will be converted as plain text. You can use ‘removeHyperlink’ method of ‘Editor’ instance if the selection is in hyperlink. Refer to the following example.

```typescript
this.documentEditor.editor.removeHyperlink();
```

## Hyperlink dialog

Document editor provides dialog support to insert or edit a hyperlink. Refer to the following example.

{% tab template="document-editor/link",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, EditorService, SelectionService, EditorHistoryService, HyperlinkDialogService, SfdtExportService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="width:100%;height:330px"><button ejs-button (click)="showHyperlinkDialog()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width:100%;height:100%;display:block" [isReadOnly]=false [enableEditor]=true [enableSelection]=true [enableSfdtExport]=true [enableEditorHistory]=true [enableHyperlinkDialog]=true> </ejs-documenteditor></div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [ EditorService, SelectionService, EditorHistoryService, HyperlinkDialogService, SfdtExportService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public showHyperlinkDialog() :void {
    this.documentEditor.showDialog('Hyperlink');;
 }

}
```

{% endtab %}

You can use the following keyboard shortcut to open the hyperlink dialog if the selection is in hyperlink.

| Key Combination | Description |
|-----------------|-------------|
|Ctrl + K | Open hyperlink dialog that allows you to create or edit hyperlink|

## See Also

* [Feature modules](../document-editor/feature-module/)
* [Hyperlink dialog](../document-editor/dialog#hyperlink-dialog/)
