---
title: " Rich text editor restricts the image uploading while uploading with large size"
component: "Rich Text Editor"
description: "This section for Syncfusion Angular Rich Text Editor control explains about, how to restrict the image to upload, when the given image size is greater than the allowed size"
---

# Restrict the image uploading while uploading with large size

By using the Rich text editor's `imageUploading` event, you can get the image size before uploading and restrict the image to upload, when the given image size is greater than the allowed size.

In the following, we have validated the image size before uploading and determined whether the image has been uploaded or not.

{% tab template="rich-text-editor/how-to/check-image-size", sourceFiles="app/**/*.ts,index.html" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, RichTextEditorComponent  } from '@syncfusion/ej2-angular-richtexteditor';
import { UploadingEventArgs } from '@syncfusion/ej2-angular-inputs';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='defaultRTE' #sample [insertImageSettings]='insertImageSettings' [toolbarSettings]='toolbarSettings' (imageUploading)='onImageUploading($event)'>
</ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService ]
})
export class AppComponent  {
@ViewChild('sample') public rteObj: RichTextEditorComponent;

public toolbarSettings: Object = {
  items: ['Bold', 'Italic', 'Underline', 'StrikeThrough','|',
      'FontName', 'FontSize', 'FontColor', 'BackgroundColor',
      'LowerCase', 'UpperCase', '|',
      'Formats', 'Alignments', 'OrderedList', 'UnorderedList',
      'Outdent', 'Indent', '|',
      'CreateLink', 'Image', '|', 'ClearFormat', 'Print',
      'SourceCode', 'FullScreen', '|', 'Undo', 'Redo']
};
public insertImageSettings: object = {
    saveUrl: "https://aspnetmvc.syncfusion.com/services/api/uploadbox/Save",
    path: "../Images/"
};

public onImageUploading = (args: UploadingEventArgs) => {
    console.log("file is uploading");
    let imgSize: number = 500000;
    let sizeInBytes: number = args.fileData.size;
    if (imgSize < sizeInBytes) {
        args.cancel = true;
    }

}

```

{% endtab %}