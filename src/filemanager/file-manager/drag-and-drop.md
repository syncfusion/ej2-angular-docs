---
title: "Drag and Drop"
component: "File Manager"
description: "Drag and Drop Support in file manager"
---

# Drag And Drop

The file manager allows files or folders to be moved from one folder to another by using the  [allowDragAndDrop](../api/file-manager/#allowdraganddrop) property. It also supports uploading a file by dragging it from Windows Explorer to  FileManager control. You can enable or disable this support by using the [allowDragAndDrop](../api/file-manager/#allowdraganddrop) property of file manager.

The event triggered in drag and drop support are

* [fileDragStart](../api/file-manager/#filedragstart) - Triggers when the file/folder dragging is started.
* [fileDragging](../api/file-manager/#filedragging) - Triggers while dragging the file/folder.
* [fileDragStop](../api/file-manager/#filedragstop) - Triggers when the file/folder is about to be dropped at the target.
* [fileDropped](../api/file-manager/#filedropped) - Triggers when the file/folder is dropped.

{% tab template="file-manager/drag-and-drop", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public allowDragAndDrop: boolean;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        this.allowDragAndDrop = true;
       };
    // File Manager's file drag start event function
    onFileDragStart(args: any) {
        console.log("File drag start");
    }
    // File Manager's file drag stop event function
    onFileDragStop(args: any) {
        console.log("File drag stop");
    }
    // File Manager's file dragging event function
    onFileDragging(args: any) {
        console.log("File dragging");
    }
    // File Manager's file dropped event function
    onFileDropped(args: any) {
        console.log("File dropped");
    }
}

```

{% endtab %}