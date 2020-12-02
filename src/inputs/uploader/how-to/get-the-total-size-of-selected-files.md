---
title: "Get the total size of selected files"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Get the total size of selected files

You can get the total size of selected files before uploading it to the designated server.
This can be achieved by using the selected event. Refer to the following example to calculate the total file size.

In the following example, explains about how to calculate total file size before upload.

{% tab template="uploader/file-size",  sourceFiles="app/**/*.ts,default.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { UploaderComponent, SelectedEventArgs } from '@syncfusion/ej2-angular-inputs';
@Component({
    selector: 'app-root',
    templateUrl: 'default.html',
    styleUrls: ['index.css']
})

export class AppComponent {
   @ViewChild('defaultupload')
    public uploadObj: UploaderComponent;

    public path: Object = {
        saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
        removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove'
    };
  public onSelect(args: SelectedEventArgs): void {
    let totalSize: number = 0;
    for (let file of args.filesData) {
        totalSize = totalSize + file.size;
    }
    let size: string = this.uploadObj.bytesToSize(totalSize);
    alert("Total select file's size is " + size)
}
}
```

{% endtab %}
