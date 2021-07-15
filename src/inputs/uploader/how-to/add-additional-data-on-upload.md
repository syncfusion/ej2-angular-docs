---
title: "Add additional data on upload"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Add additional data on upload

The uploader component allows you to add additional data on file upload, which is used to get in the server-side.
By using the [uploading](../../api/uploader/#uploading) event and its customFormData argument, you can achieve this behavior. Refer to the following example

In the following code snippet, explains about how to add additional data on file upload.

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

    public onFileUpload: EmitType<SelectedEventArgs> = (args: any) =>  {
        // add addition data as key-value pair.
        args.customFormData = [{'name': 'Syncfusion INC'}];
    };
}
```

## Server side for adding additional data

```csharp
    // Get the additional data in server end by corresponding key.
    var data = HttpContext.Current.Request.Form["name"];
```

> You can also explore [Angular File Upload](https://www.syncfusion.com/angular-ui-components/angular-file-upload) feature tour page for its groundbreaking features. You can also explore our [Angular File Upload example](https://ej2.syncfusion.com/angular/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
