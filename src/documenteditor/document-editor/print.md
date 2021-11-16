---
title: "Print"
component: "DocumentEditor"
description: "Learn how to print the document in Angular document editor and customize page size, margins, and more during print."
---

# Print

To print the document, use the `print` method from document editor instance.

Refer to the following example for showing a document and print it.

{% tab template="document-editor/link",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, PrintService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
      selector: 'app-container',
      //specifies the template string for the Document Editor component
      template: `<div>
      <button ejs-button (click)="onPrint()" >Print</button>
      <ejs-documenteditor #document_editor height="330px" style="display:block" [enablePrint]=true (created)="onCreated()"></ejs-documenteditor>
      </div>`,
      encapsulation: ViewEncapsulation.None,
      providers: [PrintService]
})

export class AppComponent {
    @ViewChild('document_editor')
    public documentEditor: DocumentEditorComponent;

    onCreated(): void {
        if (this.documentEditor.isDocumentLoaded) {
            let sfdt: string = `{
                "sections": [
                    {
                        "blocks": [
                            {
                                "inlines": [
                                    {
                                        "characterFormat": {
                                            "bold": true,
                                            "italic": true
                                        },
                                        "text": "Hello World"
                                    }
                                ]
                            }
                        ],
                        "headersFooters": {
                        }
                    }
                ]
            }`;
            //Open the default document.
            this.documentEditor.open(sfdt);
        }
    }

    public onPrint(): void {
        //Print the document content.
        this.documentEditor.print();
    }
}
```

{% endtab %}

Refer to the following example for creating a document and print it.

{% tab template="document-editor/link",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, PrintService, SelectionService, EditorService, EditorHistoryService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
      selector: 'app-container',
      template: `<div>
      <button ejs-button (click)="onPrint()" >Print</button>
      <ejs-documenteditor #document_editor height="330px" style="display:block" [isReadOnly]=true [enableSelection]=true [enableEditor]=true [enablePrint]=true (created)="onCreated()"></ejs-documenteditor>
      </div>`,
      encapsulation: ViewEncapsulation.None,
      providers: [PrintService, SelectionService, EditorService, EditorHistoryService]
})

export class AppComponent {
    @ViewChild('document_editor')
    public documentEditor: DocumentEditorComponent;

    onCreated(): void {
        if (this.documentEditor.isDocumentLoaded) {
            let sfdt: string = `{
                "sections": [
                    {
                        "blocks": [
                            {
                                "inlines": [
                                    {
                                        "characterFormat": {
                                            "bold": true,
                                            "italic": true
                                        },
                                        "text": "Hello World"
                                    }
                                ]
                            }
                        ],
                        "headersFooters": {
                        }
                    }
                ]
            }`;
            //Open the document content.
            this.documentEditor.open(sfdt);
        }
    }

    public onPrint(): void {
        //Print the document content.
        this.documentEditor.print();
    }
}
```

{% endtab %}

## Print using window object

You can print the document in document editor by passing the window instance. This is useful to implement print in third party frameworks such as electron, where the window instance will not be available. Refer to the following example.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, PrintService, SelectionService, EditorService, EditorHistoryService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
      selector: 'app-container',
      template: `<div>
      <button ejs-button (click)="onPrint()" >Print</button>
      <ejs-documenteditor #document_editor height="330px" style="display:block" [enablePrint]=true></ejs-documenteditor>
      </div>`,
      encapsulation: ViewEncapsulation.None,
      providers: [PrintService]
})

export class AppComponent {
    @ViewChild('document_editor')
    public documentEditor: DocumentEditorComponent;

    public onPrint(): void {
        //Print the document content.
        this.documentEditor.print(window);
    }
}
```

## Page setup

Some of the print options cannot be configured using JavaScript. Refer to the following links to learn more about the browser page setup:

* [`Chrome`](https://support.google.com/chrome/answer/1069693?hl=en&visit_id=1-636335333734668335-3165046395&rd=1/)
* [`Firefox`](https://support.mozilla.org/en-US/kb/how-print-web-pages-firefox/)

However, you can customize margins, paper, and layout options by modifying the section format properties using page setup dialog

```typescript
this.documentEditor.showPageSetupDialog();
```

By customizing margins, papers, and layouts, the layout of the document will be changed in document editor. To modify these options during print operation, serialize the document as SFDT using the `serialize` method in document editor instance and open the SFDT data in another instance of document editor in separate window.

The following example shows how to customize layout options only for printing.

{% tab template="document-editor/link",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, PrintService, SelectionService, EditorService, EditorHistoryService, SfdtExportService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
      selector: 'app-container',
      //specifies the template string for the Document Editor component
      template: `<div>
          <button ejs-button (click)="onPrint()" >Print</button>
          <ejs-documenteditor #document_editor height="330px" style="display:block" [isReadOnly]=false [enableSelection]=true [enableEditor]=true [enablePrint]=true [enableSfdtExport]=true></ejs-documenteditor>
          <ejs-documenteditor #document_editor_preview height="330px" style="display:block" [isReadOnly]=false [enableSelection]=true [enableEditor]=true [enablePrint]=true [enableSfdtExport]=true></ejs-documenteditor>
      </div>`,
      encapsulation: ViewEncapsulation.None,
      providers: [PrintService, SelectionService, EditorService, EditorHistoryService, SfdtExportService]
})

export class AppComponent {
    @ViewChild('document_editor')
    public documentEditor: DocumentEditorComponent;

    @ViewChild('document_editor_preview')
    public documentEditorPreview: DocumentEditorComponent;

    public onPrint(): void {
        let sfdtData = this.documentEditor.serialize();
        //Open the document in preview document editor.
        this.documentEditorPreview.open(sfdtData);
        //Set A5 paper size
        this.documentEditorPreview.selection.sectionFormat.pageWidth = 419.55;
        this.documentEditorPreview.selection.sectionFormat.pageHeight = 595.30;
        //Print the document content.
        this.documentEditorPreview.print();
    }
}

```

{% endtab %}
