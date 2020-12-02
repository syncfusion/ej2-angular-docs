---
title: "Validation"
component: "Uploader"
description: "Explains how to validate files before uploading it to a server such as valid file extensions, min and max file size, and duplicate files."
---

# Validation

The uploader component validate the selected files extension and size using the `allowedExtentions`,
`minFileSize` and `maxFileSize`properties.
The files can be validated before uploading to the server and can be ignored on uploading.
Also, you can validate the files by setting the HTML attributes to the original input element.
The validation process occurs on drag-and-drop the files also.

## File type

You can allow the specific types of files alone to upload using the `allowedExtentions` property.
The extension can be represented as collection by comma separators. The uploader component
filters the selected or dropped files matched against the specified file types and processes the
upload operation. The validation happens when you specify value to inline attribute accept to original input element.

{% tab template="uploader/uploader", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
               <ejs-uploader #defaultupload  [asyncSettings]='path' allowedExtensions = '.jpg,.png'></ejs-uploader>
              `
})
export class AppComponent {
     public path: Object = {
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove' };
    constructor() {
    }
}

```

{% endtab %}

## File size

The uploader component allows you to validate the files based on its size.
The validation helps to restrict uploading large files or empty files to the server. The size can be represented in `bytes`.
By default, the uploader component allows you to upload **minimum file size** as 0 byte and
 **maximum file size** as 28.4 MB using using `minFileSize` and `maxFileSize` properties.

{% tab template="uploader/uploader", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
               <ejs-uploader #defaultupload  [asyncSettings]='path' minFileSize = 10000 maxFileSize = 1500000></ejs-uploader>
              `
})
export class AppComponent {
     public path: Object = {
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove' };
    constructor() {
    }
}

```

{% endtab %}

## Maximum files count

You can restrict uploading the maximum number of files using the **selected** event. In the selected event arguments,
you can get the currently selected files details using the `getFilesData()`.
You can modify the files details and assign the modified file list to the `eventArgs.modifiedFilesData`.

{% tab template="uploader/uploader", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import {  FileInfo, SelectedEventArgs  } from '@syncfusion/ej2-inputs';
import { detach } from '@syncfusion/ej2-base';
import { createSpinner, showSpinner, hideSpinner } from '@syncfusion/ej2-popups';

@Component({
    selector: 'app-root',
    template: `
               <ejs-uploader #defaultupload autoUpload='false'  [asyncSettings]='path' minFileSize = 10000 allowedExtensions = '.doc, .docx, .xls, .xlsx' (selected)="onFileSelected($event)" (success)="onUploadSuccess($event)"></ejs-uploader>
              `
})
export class AppComponent {
    public path: Object = {
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove' };
    @ViewChild('defaultupload')
    public uploadObj: UploaderComponent;
    public onFileSelected(args : SelectedEventArgs) : void {
        // Filter the 5 files only to showcase
        args.filesData.splice(5);
        let filesData : FileInfo[] = this.uploadObj.getFilesData();
        let allFiles : FileInfo[] = filesData.concat(args.filesData);
        if (allFiles.length > 5) {
            for (let i : number = 0; i < allFiles.length; i++) {
                if (allFiles.length > 5) {
                    allFiles.shift();
                }
            }
            args.filesData = allFiles;
            // set the modified custom data
            args.modifiedFilesData = args.filesData;
        }
        args.isModified = true;
    }
    public onUploadSuccess(args: any): void {
        let li: HTMLElement = this.uploadObj.uploadWrapper.querySelector('[data-file-name="' + args.file.name + '"]');
        if (args.operation === 'upload') {
            (li.querySelector('.e-file-delete-btn') as HTMLElement).onclick = () => {
                this.generateSpinner(this.uploadObj.uploadWrapper);
            };
            (li.querySelector('.e-file-delete-btn') as HTMLElement).onkeydown = (e: any) => {
                if (e.keyCode === 13) {
                    this.generateSpinner(e.target.closest('.e-upload'));
                }
            };
        } else {
            hideSpinner(this.uploadObj.uploadWrapper);
            detach(this.uploadObj.uploadWrapper.querySelector('.e-spinner-pane'));
        }
    }
    public generateSpinner(targetElement: HTMLElement): void {
        createSpinner({ target: targetElement, width: '25px' });
        showSpinner(targetElement);
    }
    constructor() {
    }
}

```

{% endtab %}

## Duplicate files

You can validate the duplicate files before uploading to server using the selected event.
Compare the selected files with the existing files data and filter the file list by removing the duplicate files.

{% tab template="uploader/uploader", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import {  FileInfo } from '@syncfusion/ej2-inputs';
import { isNullOrUndefined } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
               <ejs-uploader #defaultupload autoUpload='false'  [asyncSettings]='path' (selected)="onFileSelect($event)" ></ejs-uploader>
              `
})
export class AppComponent {
    public path: Object = {
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove' };
    @ViewChild('defaultupload')
    public uploadObj: UploaderComponent;
    public onFileSelect(args : any) {
    let existingFiles: FileInfo[] = this.uploadObj.getFilesData();
    for (let i: number = 0; i < args.filesData.length; i++) {
        for(let j: number = 0; j < existingFiles.length; j++) {
            if (!isNullOrUndefined(args.filesData[i])) {
                if (existingFiles[j].name == args.filesData[i].name) {
                    args.filesData.splice(i, 1);
                }
            }
        }
    }
    existingFiles = existingFiles.concat(args.filesData);
    args.modifiedFilesData = existingFiles;
    args.isModified = true;
}
    constructor() {
    }
}

```

{% endtab %}

## See Also

* [Validate image/* on drop](./how-to/validate-image-on-drop)
* [Determine whether uploader has file input (required validation)](./how-to/determine-whether-uploader-has-file-input)
* [Check file size before uploading it](./how-to/check-file-size-before-uploading-it)
* [Check the MIME type of file before uploading it](./how-to/check-the-mime-type-of-file-before-upload-it)
