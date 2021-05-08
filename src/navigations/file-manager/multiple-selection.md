---
title: "Multiple Selection"
component: "File Manager"
description: "Multiple Selection present in file manager"
---

# Multiple Selection

The file manager allows you to select multiple files by enabling the [allowMultiSelection](../api/file-manager/#allowmultiselection) property (enabled by default). The multiple selection can be done by pressing the `Ctrl` key or `Shift` key and selecting the files. The check box can also be used to do multiple selection. `Ctrl + A` can be used to select all files in the current directory. The [fileSelect](../api/file-manager/#fileselect) event will be triggered when the items of file manager control is selected or unselected.

{% tab template="file-manager/multiselect", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';
import { FileSelectEventArgs } from '@syncfusion/ej2-filemanager';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public allowMultiSelection: boolean;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
       this.allowMultiSelection = true;
       }
    // File Manager's file select event function
    onFileSelect(args: FileSelectEventArgs) {
        console.log(args.fileDetails.name + " has been " + args.action + "ed");
    }
}

```

{% endtab %}

>Note: The File Manager has support to select files and folders initially or dynamically by specifying their names in [selectedItems](../api/file-manager/#selecteditems) property.