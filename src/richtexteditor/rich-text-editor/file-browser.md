---
title: "Rich Text Editor File Browser"
component: "Rich Text Editor"
description: "This section explains about how to enable the file browser feature in the Syncfusion Angular Rich Text Editor component."
---

# File Browser

Rich Text Editor allows to browse and insert images in the edit panel using the file browser. File browser allows the users to browse and select a file or folder from the file system and it supports various cloud services.

The following example explains about how to configure the file browser within the Rich Text Editor.

* Configure the `FileManager` toolbar item in the `toolbarSettings` API `items` property.
* Set the [`enable`](../api/rich-text-editor/fileManagerSettings/#enable) property as `true` on [`fileManagerSettings`](../api/rich-text-editor/#fileManagerSettings) property to make the file browser in the  Rich Text Editor to appear on the `FileManager` toolbar click action.

> Rich Text Editor features are segregated into individual feature-wise modules. To use the file browser tool, configure `FileManagerService` in providers.

{% tab template="rich-text-editor/file-browser", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

/**
* RTE File Browser Sample
*/
import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, QuickToolbarService, FileManagerService } from '@syncfusion/ej2-angular-richtexteditor';

@Component({
selector: 'app-root',
template: `<ejs-richtexteditor [toolbarSettings]='toolbarSettings' [fileManagerSettings]='fileManagerSettings'>
            <ng-template #valueTemplate>
                <p>The Rich Text Editor is WYSIWYG ("what you see is what you get") editor useful to create and edit content, and return the valid <a href="https://ej2.syncfusion.com/home/" target="_blank">HTML markup</a> or <a href="https://ej2.syncfusion.com/home/" target="_blank">markdown</a> of the content</p>
                <p><b>Key features:</b></p>
                <ul>
                    <li><p>Provides &lt;IFRAME&gt; and &lt;DIV&gt; modes</p></li>
                    <li><p>Capable of handling markdown editing.</p></li>
                    <li><p>Contains a modular library to load the necessary functionality on demand.</p></li>
                    <li><p>Provides a fully customizable toolbar.</p></li>
                    <li><p>Provides HTML view to edit the source directly for developers.</p></li>
                    <li><p>Supports third-party library integration.</p></li>
                    <li><p>Allows preview of modified content before saving it.</p></li>
                    <li><p>Handles images, hyperlinks, video, hyperlinks, uploads, etc.</p></li>
                </ul>
            </ng-template>
          </ejs-richtexteditor>`,
providers: [ToolbarService, LinkService, ImageService, HtmlEditorService, QuickToolbarService, FileManagerService]
})

export class AppComponent {
    private hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    private toolbarSettings: Object = {
        items: ['FileManager']
    };
    private fileManagerSettings: object = {
        enable: true,
        path: '/Pictures/Food',
        ajaxSettings: {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        }
    };
}

```

{% endtab %}