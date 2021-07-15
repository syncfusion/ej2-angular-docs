---
title: "Check the MIME type of file before upload it"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Check the MIME type of file before upload it

By using [uploading](../../api/uploader/#uploading) event, you can get the file MIME type before uploading it to server.
In the below sample, file MIME type is shown in the alert box before file start to upload.

{% tab template="uploader/mime-type", sourceFiles="app/**/*.ts,default.html" %}

```typescript
import { Component } from '@angular/core';
import { EmitType } from '@syncfusion/ej2-base';
@Component({
    selector: 'app-root',
    templateUrl: 'default.html',
    styleUrls: ['index.css']
})

export class AppComponent {
    public autoUpload: boolean = false;
    public path: Object = {
        saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
        removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove'
    };
    public onBeforeUpload: EmitType<Object> = (args: any) => {
        // get the file MIME type
        alert("File MIME type is: " + args.fileData.rawFile.type)
    }
}
```

{% endtab %}

> You can also explore [Angular File Upload](https://www.syncfusion.com/angular-ui-components/angular-file-upload) feature tour page for its groundbreaking features. You can also explore our [Angular File Upload example](https://ej2.syncfusion.com/angular/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
