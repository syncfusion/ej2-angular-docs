---
title: "Find and replace"
component: "DocumentEditor"
description: "Learn how to find a portion of text in JavaScript document editor and replace it with another portion of text."
---

# Find and replace

The document editor component searches a portion of text in the document through a built-in interface called `OptionsPane` or rich APIs. When used in combination with selection performs various operations on the search results like replacing it with some other text, highlighting it, making it bolder, and more.

## Options pane

This provides the options to search for a portion of text in the document. After search operation is completed, the search results will be displayed in a list and options to navigate between them. The current occurrence of matched text or all occurrences with another text can be replaced by switching to `Replace` tab. This pane is opened using the keyboard shortcut `CTRL+F`. You can also open it programmatically using the following sample code.

{% tab template="document-editor/find-replace",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent,  SelectionService, EditorService, SearchService, OptionsPaneService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="width:100%;height:330px">
    <button ejs-button (click)="showOptionsPane()" >Show</button>
    <ejs-documenteditor #document_editor  id="container" style="width:100%;height:100%;display:block" [enableSelection]=true [enableSearch]=true [enableEditor]=true [isReadOnly]=false [enableOptionsPane]=true (created)="onCreated()"></ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SelectionService, EditorService, SearchService, OptionsPaneService]
})

export class AppComponent {
    @ViewChild('document_editor')
    public documentEditor: DocumentEditorComponent;

    onCreated(): void {
        if(this.documentEditor.isDocumentLoaded) {
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
                                    "text": "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Bothell, Washington with 290 employees, several regional sales teams are located throughout their market base."
                                }
                            ]
                        }
                    ]
                }
            ]
        }`;
            this.documentEditor.open(sfdt);
        }
    }

 public showOptionsPane() :void {
    this.documentEditor.showOptionsPane();
 }

}
```

{% endtab %}

You can close the options pane by pressing `Esc` key.

## Search

The `Search` module of document editor exposes the following APIs:

|API Name|Type |Description|
|---|---|---|
|`findAll()` | Method |Searches for specified text in the whole document and highlights it with yellow.|
|`searchResults` |Property |This is an instance of `SearchResults`.|

Refer to the following code example.

```typescript
this.documentEditor.search.findAll('Some text', 'None');
```

## Search results

The `SearchResults` class provides information about the search results after a search operation is completed that can be identified using the `searchResultsChange` event. This will expose the following APIs:

|API Name|Type |Description|
|---|---|---|
|`length`|Property|Returns the total number of results found on the search.|
|`index`|Property|Returns the index of selected search result. You can change the value for this property to move the selection.|
|`replaceAll()`|Method|Replaces all the occurrences with specified text.|
|`clear()`|Method|Clears the search result.|

## SearchResultsChange event

`DocumentEditor` exposes the `searchResultsChange’`event that will be triggered whenever search results are changed. Consider the following scenarios:

* A search operation is completed with some results.
* The results are replaced with some other text, since it will be cleared automatically.
* The results are cleared explicitly.

Refer to the following code example.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, EditorService, SelectionService, SfdtExportService, EditorHistoryService, BookmarkDialogService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<ejs-documenteditor #document_editor  id="container" style="width:100%;height:100%;display:block" [isReadOnly]=false [enableSelection]=true [enableSearch]=true (searchResultsChange)="onSearchResultChange()" > </ejs-documenteditor>`,
    encapsulation: ViewEncapsulation.None,
    providers: [EditorService, SelectionService, SfdtExportService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

// search result change event handler
public onSearchResultChange() :void {

}

}
```

## Customize find and replace

Using the exposed APIs, you can customize the find and replace functionality in your application. Refer to the following sample code.

{% tab template="document-editor/find-replace",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent,  SelectionService, EditorService, SearchService, OptionsPaneService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="width:100%;height:330px">
    <table>
        <tr>
            <td>
                <label>Text to find:</label>
            </td>
            <td>
                <input type="text" id="find_text" />
            </td>
        </tr>
        <tr>
            <td>
                <label>Text to replace:</label>
            </td>
            <td>
                <input type="text" id="replace_text" />
            </td>
        </tr>
        <tr>
            <td colspan="2">
                 <button ejs-button (click)="onReplaceButtonClick()" >Replace all</button>
            </td>
        </tr>
    </table>
    <ejs-documenteditor #document_editor  id="container" style="width:100%;height:100%;display:block" [enableSelection]=true [enableSearch]=true [enableEditor]=true [isReadOnly]=false (created)="onCreated()"></ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [ SelectionService, EditorService, SearchService]
})

export class AppComponent {
    @ViewChild('document_editor')
    public documentEditor: DocumentEditorComponent;

    onCreated(): void {
        if(this.documentEditor.isDocumentLoaded) {
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
                                    "text": "Adventure Works Cycles, the fictitious company on which the AdventureWorks sample databases are based, is a large, multinational manufacturing company. The company manufactures and sells metal and composite bicycles to North American, European and Asian commercial markets. While its base operation is located in Bothell, Washington with 290 employees, several regional sales teams are located throughout their market base."
                                }
                            ]
                        }
                    ]
                }
            ]
        }`;
            this.documentEditor.open(sfdt);
        }
    }

 public onReplaceButtonClick() :void {
    let textToFind: string = (document.getElementById('find_text') as HTMLInputElement).value;
    let textToReplace: string = (document.getElementById('replace_text') as HTMLInputElement).value;
    if (textToFind !== '') {
        // Find all the occurences of given text
        this.documentEditor.searchModule.findAll(textToFind);
        if (this.documentEditor.searchModule.searchResults.length > 0) {
            // Replace all the occurences of given text
            this.documentEditor.searchModule.searchResults.replaceAll(textToReplace);
        }
    }
 }

}
```

{% endtab %}