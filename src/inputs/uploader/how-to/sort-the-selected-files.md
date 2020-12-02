---
title: "Sort the selected files"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Sort the selected files

You can sort the selected files in an uploader component by using the [selected](../../api/uploader/#selected) event. Refer to the following example.

{% tab template="uploader/sorting", sourceFiles="app/**/*.ts,default.html,index.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';

import { UploaderComponent, SelectedEventArgs, FileInfo } from '@syncfusion/ej2-angular-inputs';

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
  public initial:boolean = true;
  public onSelect(args: SelectedEventArgs): void {
    if (this.initial) { this.initial = false; return; }
    args.isModified = true;
    let oldFiles: FileInfo[] = this.uploadObj.getFilesData();
    let filesData: FileInfo[] = args.filesData.concat(oldFiles);
    let modifiedData: FileInfo[] = this.sortFileList(filesData);
    args.modifiedFilesData = modifiedData;
}

public sortFileList(filesData: FileInfo[]): FileInfo[] {
    let files: FileInfo[] = filesData;
    let fileNames: string[] = [];
    for (let i: number = 0; i < files.length; i++) {
        fileNames.push(files[i].name);
    }
    let sortedFileNames: string[] = fileNames.sort();
    let sortedFilesData: FileInfo[] = [];
    let index: number = 0;
    for (let name of sortedFileNames) {
        for (let i: number = 0; i < files.length; i++) {
            if (name === files[i].name) {
                sortedFilesData.push(files[i]);
            }
        }
    }
    return sortedFilesData;
}
}

```

{% endtab %}
