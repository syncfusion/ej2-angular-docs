---
title: "Validate image on drop"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Validate image/* on drop

The uploader component allows you to upload all type of images by setting
**image/* ** to [allowedExtensions](../../api/uploader/#allowedextensions) property.
You can directly set it to `accept` attribute of uploader element.

By default, the behavior is working with select a file using browse button. But, this behavior doesn’t support
on drag and drop the files. You can handle this behavior manually using `selected` event by filtering the file types from application.

In the following example, validated image files using images/*. You are able to drag and drop the image files with extension of PNG, JPG, BPG, GIF and TIFF to upload it.

{% tab template="uploader/validate-image", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';
import { EmitType } from '@syncfusion/ej2-base';
import { SelectedEventArgs } from '@syncfusion/ej2-angular-inputs';
@Component({
    selector: 'app-root',
    templateUrl: 'default.html',
    styleUrls: ['index.css']
})

export class AppComponent {

   public path: Object = {
       saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
       removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove'
   };
    public onSelected: EmitType<SelectedEventArgs> = (args: any) =>  {
        if (event.type === 'drop') {
            let allImages: Array<string> = ['png', 'jpg', 'jpeg', 'gif', 'tiff', 'bpg'];
            let files = args.filesData;
            let modifiedFiles = [];
            for (let file of files) {
              if (allImages.indexOf(file.type) === -1) {
                file.status = 'File type is not allowed';
                file.statusCode = '0';
              }
              modifiedFiles.push(file);
            }
            args.isModified = true;
        }
   };
}
```

{% endtab %}
