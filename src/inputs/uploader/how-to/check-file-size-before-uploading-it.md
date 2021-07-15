---
title: "Check file size before uploading it"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Check file size before uploading it

By using [uploading](../../api/uploader/#uploading) event, you can get the file size before upload it to server.
File object contains the file size in bytes only.
You can convert the size to standard formats (`KB` or `MB`) using [bytesToSize](../../api/uploader/#bytestosize) method.

{% tab template="uploader/check-file-size", sourceFiles="app/**/*.ts,default.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { EmitType } from '@syncfusion/ej2-base';
import { UploaderComponent } from '@syncfusion/ej2-angular-inputs';
@Component({
    selector: 'app-root',
    templateUrl: 'default.html',
    styleUrls: ['index.css']
})

export class AppComponent {
    @ViewChild('defaultupload')
    public uploadObj: UploaderComponent;
    public autoUpload: boolean = false;
    public path: Object = {
        saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
        removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove'
    };
    public onBeforeUpload: EmitType<Object> = (args: any) => {
        // get the file size in bytes
        let sizeInBytes: number = args.fileData.size;
        // get the file size in standard format
        alert("File size is: " + this.uploadObj.bytesToSize(sizeInBytes));
    }
}
```

{% endtab %}

> You can also explore [Angular File Upload](https://www.syncfusion.com/angular-ui-components/angular-file-upload) feature tour page for its groundbreaking features. You can also explore our [Angular File Upload example](https://ej2.syncfusion.com/angular/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
