---
title: "Achieve file upload programmatically"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Achieve file upload programmatically

You can upload a file programmatically using [upload](../../api/uploader/#upload) method.
The selected files data, get from [getFilesData](../../api/uploader/#getfilesdata) public method in uploader.

The upload method behaves differently based on its arguments.
* If this method receives any files as arguments, those files only start to upload.
* If it has no argument then all the selected files are will start to upload.

{% tab template="uploader/dynamic-upload", sourceFiles="app/**/*.ts,default.html,index.css" %}

```typescript
import { Component, ViewChild, AfterViewInit } from '@angular/core';
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
    ngAfterViewInit(): void {
        document.getElementById('first').onclick = (args) => {
            this.uploadObj.upload(this.uploadObj.getFilesData()[0]);
        };
        document.getElementById('full').onclick = (args) => {
            this.uploadObj.upload(this.uploadObj.getFilesData());
        };
    }
}
```

{% endtab %}
