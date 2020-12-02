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

You can convert word documents into SFDT format using the .NET Standard library [`Syncfusion.EJ2.WordEditor.AspNet.Core`](<https://www.nuget.org/packages/Syncfusion.EJ2.WordEditor.AspNet.Core/>) by the web API service implementation. This library helps you to convert word documents (.dotx,.docx,.docm,.dot,.doc), rich text format documents (.rtf), and text documents (.txt) into SFDT format. Refer to the following example.

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

## See Also

* [Feature modules](../document-editor/feature-module/)