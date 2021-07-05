---
title: "Import"
component: "DocumentEditor"
description: "Learn how to import SFDT and word documents in JavaScript document editor using supported APIs."
---

# Import

In Document Editor, the documents are stored in its own format called **Syncfusion Document Text (SFDT)**.

The following example shows how to open SFDT data in Document Editor.

{% tab template="document-editor/import",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="width:100%;height:330px">
     <ejs-documenteditor #document_editor id="container" (created)="onCreated()" style="width:100%;height:100%;display:block"></ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

    onCreated() {
       if(this.documentEditor.isDocumentLoaded) {
            let sfdt: string =`{
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
        this.documentEditor.open(sfdt);
       }
    }
}

```

{% endtab %}

## Import document from local machine

The following example shows how to import document from local machine.

{% tab template="document-editor/import",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="width:100%;height:330px">
     <input id="open_sfdt" #open_sfdt style="position:fixed; left:-100em" type="file" (change)="onFileChange($event)" accept=".sfdt"/>
    <button ejs-button (click)="onFileOpenClick()" >Import</button>
    <ejs-documenteditor #document_editor  id="container" style="width:100%;height:100%;display:block"></ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

public onFileOpenClick() :void {
    document.getElementById('open_sfdt').click();
}

public onFileChange(e: any) :void {
    if (e.target.files[0]) {
            let file = e.target.files[0];
            if (file.name.substr(file.name.lastIndexOf('.')) === '.sfdt') {
                let fileReader: FileReader = new FileReader();
                fileReader.onload = (e: any) => {
                    let contents: string = e.target.result;
                    this.documentEditor.open(contents);
                };
                fileReader.readAsText(file);
                 this.documentEditor.documentName = file.name.substr(0, file.name.lastIndexOf('.'));
            }
    }
}
}

```

{% endtab %}

## Convert word documents into SFDT

You can convert word documents into SFDT format using the .NET Standard library [`Syncfusion.EJ2.WordEditor.AspNet.Core`](<https://www.nuget.org/packages/Syncfusion.EJ2.WordEditor.AspNet.Core/>) by the web API service implementation. This library helps you to convert word documents (.dotx,.docx,.docm,.dot,.doc), rich text format documents (.rtf), and text documents (.txt) into SFDT format.

>Note: The Syncfusion Document editor component's document pagination (page-by-page display) can't be guaranteed for all the Word documents to match the pagination of Microsoft Word application. For more information about [why the document pagination (page-by-page display) differs from Microsoft Word](../document-editor/import/#why-the-document-pagination-differs-from-microsoft-word)

Please refer the following example for converting word documents into SFDT.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="width:100%;height:330px">
     <input id="open_sfdt" #open_sfdt style="position:fixed; left:-100em" type="file" (change)="onFileChange($event)" accept=".dotx,.docx,.docm,.dot,.doc,.rtf,.txt,.xml,.sfdt"/>
     <button ejs-button (click)="onFileOpenClick()" >Import</button>
     <ejs-documenteditor #document_editor  id="container" style="width:100%;height:100%;display:block"></ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

public onFileOpenClick() :void {
    document.getElementById('open_sfdt').click();
}

public onFileChange(e: any) :void {
     if (e.target.files[0]) {
        let file = e.target.files[0];
        if (file.name.substr(file.name.lastIndexOf('.')) !== '.sfdt') {
            this.loadFile(file);
        }
    }
}

public loadFile(file: File): void {
    let ajax: XMLHttpRequest = new XMLHttpRequest();
    ajax.open('POST', 'https://localhost:4000/api/documenteditor/Import', true);
    ajax.onreadystatechange = () => {
        if (ajax.readyState === 4) {
            if (ajax.status === 200 || ajax.status === 304) {
                // open SFDT text in document editor
                this.documentEditor.open(ajax.responseText);
            }
        }
    }
    let formData: FormData = new FormData();
    formData.append('files', file);
    ajax.send(formData);
}

}

```

Here’s how to handle the server-side action for converting word document in to SFDT.

```csharp
[AcceptVerbs("Post")]
public string Import(IFormCollection data)
{
    if (data.Files.Count == 0)
        return null;
    Stream stream = new MemoryStream();
    IFormFile file = data.Files[0];
    int index = file.FileName.LastIndexOf('.');
    string type = index > -1 && index < file.FileName.Length - 1 ?
        file.FileName.Substring(index) : ".docx";
    file.CopyTo(stream);
    stream.Position = 0;

    WordDocument document = WordDocument.Load(stream, GetFormatType(type.ToLower()));
    string sfdt = Newtonsoft.Json.JsonConvert.SerializeObject(document);
    document.Dispose();
    return sdft;
}

internal static FormatType GetFormatType(string format)
{
    if (string.IsNullOrEmpty(format))
        throw new NotSupportedException("EJ2 DocumentEditor does not support this file format.");
    switch (format.ToLower()) {
        case ".dotx":
        case ".docx":
        case ".docm":
        case ".dotm":
            return FormatType.Docx;
        case ".dot":
        case ".doc":
            return FormatType.Doc;
        case ".rtf":
            return FormatType.Rtf;
        case ".txt":
            return FormatType.Txt;
        case ".xml":
            return FormatType.WordML;
        default:
            throw new NotSupportedException("EJ2 DocumentEditor does not support this file format.");
    }
}

```

## Compatibility with Microsoft Word

Syncfusion Document editor is a minimal viable Word document viewer/editor product for web applications. As most compatible Word editor, the product vision is adding valuable feature sets of Microsoft Word, and not to cover 100% feature sets of Microsoft Word desktop application. You can even see the feature sets difference between Microsoft Word desktop and their Word online application. So kindly don't misunderstand this component as a complete replacement for Microsoft Word desktop application and expect 100% feature sets of it.

### How Syncfusion accepts the feature request for Document editor

Syncfusion accepts new feature request as valid based on feature value and technological feasibility, then plan to implement unsupported features incrementally in future releases in a phase-by-phase manner.

### How to report the problems in Document editor

You can report the problems with displaying, or editing Word documents in Document editor component through [`support forum`](https://www.syncfusion.com/forums/), [`Direct-Trac`](https://www.syncfusion.com/support/directtrac/), or [`feedback portal`](https://www.syncfusion.com/feedback/). Kindly share the Word document for replicating the problem easily in minimal time. If you have confidential data, you can replace it and attach the document.

### Why the document pagination differs from Microsoft Word

For your understanding about the Word document structure and the workflow of Word viewer/editor components, the Word document is a flow document in which content will not be preserved page by page; instead, the content will be preserved sequentially like a HTML file. Only the Word viewer/editor paginates the content of the Word document page by page dynamically, when opened for viewing or editing and this page-wise position information will not be preserved in the document level (it is Word file format specification standard). Syncfusion Document editor component also does the same.
  
At present there is a known technical limitation related to slight difference in text size calculated using HTML element based text measuring approach. Even though the text size is calculated with correct font and font size values, the difference lies; it is as low as 0.00XX to 0. XXXX values compared to that of Microsoft Word application’s display. Hence the document pagination (page-by-page display) can't be guaranteed for all the Word documents to match the pagination of Microsoft Word application.

### How Syncfusion address the document pagination difference compared to Microsoft Word

The following table illustrates the reasons for pagination (page-by-page display) difference compared to Microsoft Word in your documents and how Syncfusion address it.

| Root causes | How is it solved? |
|-----------------|-------------|
|Any mistake (wrong behavior handled) in lay outing the supported elements and formatting   |Customer can report to Syncfusion support and track the status through bug report link.  Syncfusion fixes the bugs in next possible weekly patch release and service pack or main releases. |
|Font missing in deployment environment|Customer can either report to Syncfusion support and get suggestion or solve it on their own by installing the missing fonts in their deployment environment.|
|Any unsupported elements or formatting present in your document |Customer can report to Syncfusion support and track the status through feature request link.   Syncfusion implements unsupported features incrementally in future releases based on feature importance, customer interest, efforts involved, and technological feasibility. Also, suggests alternate approach for possible cases.|
|Technical limitation related to framework   For example, there is a known case with slight fractional difference in text size measured using HTML and Microsoft Word’s display.|Customer can report to Syncfusion support and track the status through feature request link.  Syncfusion does research about alternate approaches to overcome the technical limitation/behaviors and process it same as a feature. >Note: Here the challenge is, time schedule for implementation varies based on the alternate solution and its reliability.|

## See Also

* [Feature modules](../document-editor/feature-module/)