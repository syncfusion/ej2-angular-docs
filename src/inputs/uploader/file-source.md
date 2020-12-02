---
title: "File source"
component: "Uploader"
description: "Explains various sources to file upload such as drag and drop (customizable), paste the images, folder selection (directory upload)."
---

# File source

## Paste to upload

The uploader component allows you to upload the files using the select or drop files option from the file
explorer.  It also supports pasting to upload the image files. You can upload any currently copied images in the clipboard.

> When you paste the image, it will be saved in the server with the filename as `image.png`. The file name can
be renamed in the server end. You can generate a random name for the file name using `getUniqueID` method.
Refer to the following example.

{% tab template="uploader/uploader", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';
import { UploadingEventArgs } from '@syncfusion/ej2-inputs';
import { getUniqueID } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
               <ejs-uploader #defaultupload [asyncSettings]='path' autoUpload='false' (uploading)='onUploadBegin($event)'></ejs-uploader>
              `
})
export class AppComponent {
    public path: Object = {
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove' };
    constructor() {
    }
    public onUploadBegin(args: UploadingEventArgs) {
        // check whether the file is uploading from paste.
        if (args.fileData.fileSource === 'paste') {
            let newName: string = getUniqueID(args.fileData.name.substring(0, args.fileData.name.lastIndexOf('.'))) + '.png';
            args.customFormData = [{'fileName': newName}];
        }
    }
}

```

{% endtab %}

### Save action for paste to upload

```csharp
public void Save() {
    var httpPostedFile = System.Web.HttpContext.Current.Request.Files["UploadFiles"];
    var fileSave = System.Web.HttpContext.Current.Server.MapPath("UploadedFiles");
    var fileSavePath = Path.Combine(fileSave, httpPostedFile.FileName);

    if (!System.IO.File.Exists(fileSavePath)) {
        httpPostedFile.SaveAs(fileSavePath);
        var newName = System.Web.HttpContext.Current.Request.Form["fileName"];
        var filePath = Path.Combine(fileSavePath.Substring(0, fileSavePath.LastIndexOf("\\")), newName);
        // Rename the file
        System.IO.File.Move(fileSavePath, newName);
        HttpResponse Response = System.Web.HttpContext.Current.Response;
        Response.Clear();
        Response.ContentType = "application/json; charset=utf-8";
        Response.StatusDescription = fileSavePath;
        Response.End();
        }
    }
```

## Directory upload

The uploader component allows you to upload all files in the folders to server by using
the [directoryUpload](../api/uploader/#directoryupload) property. When this property is enabled,
the uploader component processes the files by iterating through the files and sub-directories in a directory.
It allows you to select only folders instead of files to upload.

> The directory upload is available only in browsers that supports **HTML5 directory**. The uploader will
process directory upload by dragging and dropping in the Edge browser.
Refer to the following example to upload files to the server.

{% tab template="uploader/directory", sourceFiles="app/**/*.ts"%}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
               <ejs-uploader #defaultupload  [asyncSettings]='path' directoryUpload='true'></ejs-uploader>
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

### Save action for directory upload

```csharp
public void Save() {
    var httpPostedFile = HttpContext.Current.Request.Files["UploadFiles"];
    var fileSave = HttpContext.Current.Server.MapPath("UploadedFiles");
    // split the folders by using file name
    string[] folders = httpPostedFile.FileName.Split('/');
    string fileSavePath = "";
    if (folders.Length > 1)
    {
        for (var i = 0; i < folders.Length - 1; i++)
        {
            var newFolder = Path.Combine(fileSave, folders[i]);
            // create folder
            Directory.CreateDirectory(newFolder);
            fileSave = newFolder;
        }
        fileSavePath = Path.Combine(fileSave, folders[folders.Length - 1]);
    }
    else
    {
        fileSavePath = Path.Combine(fileSave, httpPostedFile.FileName);
    }
    if (!System.IO.File.Exists(fileSavePath))
    {
        // save file in the corresponding server location
        httpPostedFile.SaveAs(fileSavePath);
        HttpResponse Response = System.Web.HttpContext.Current.Response;
        Response.Clear();
        Response.ContentType = "application/json; charset=utf-8";
        // Sending the file path to client side
        Response.StatusDescription = fileSavePath;
        Response.End();
    }
}
```

## Drag and drop

The uploader component allows you to drag and drop the files to upload.
You can drag the files from file explorer and drop into the drop area.
By default, the Uploader component act as drop area element.
The drop area gets highlighted when you drag the files over drop area.

### Custom drop area

The uploader component allows you to set external target element as drop area using the `dropArea` property.
The element can be represented as HTML element or element’s ID.

{% tab template="uploader/draganddrop", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `        <div id='droparea'> Drop files here to upload </div>
               <ejs-uploader #defaultupload [asyncSettings]='path' autoUpload='false' [dropArea]='ele'></ejs-uploader>
              `
})
export class AppComponent {
    public ele: HTMLElement;
    public path: Object = {
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove' };
    ngOnInit() {
        this.ele = document.getElementById('droparea');
        }
    constructor() {
    }
}
```

{% endtab %}

### Customize drop area

You can customize the appearance of drop area by overriding the default drop area styles.
The class **e-upload-drag-hover** is available to handle this customization.

{% tab template="uploader/cus_draganddrop", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id='dropArea' style='height: auto; overflow: auto'>
            <span id='drop'> Drop files here or <a href="" id='browse'><u>Browse</u></a> </span>
               <ejs-uploader #defaultupload [asyncSettings]='path'  [dropArea]='ele'></ejs-uploader>
        </div>
              `
})
export class AppComponent {
    public path: Object = {
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove' };
    public ele: HTMLElement;
    ngOnInit() {
        this.ele = document.getElementById('droparea');
        document.getElementById('browse').onclick = function() {
        document.getElementsByClassName('e-file-select-wrap')[0].querySelector('button').click();
    return false;
}
        }
    constructor() {
    }
}

```

{% endtab %}

## See Also

* [Achieve file upload programmatically](./how-to/achieve-file-upload-programmatically)
* [Validate image/* on drop](./how-to/validate-image-on-drop)
