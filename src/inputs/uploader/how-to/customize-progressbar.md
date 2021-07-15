---
title: "Customize progressbar"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Customize progressbar

You can customize the progress bar’s size, color, and background by overriding the styles in uploader component. Refer to the following example.

{% tab template="uploader/progressbar", sourceFiles="app/**/*.ts,default.html,index.css" %}

```typescript
import { Component } from '@angular/core';

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
}
```

{% endtab %}

> You can also explore [Angular File Upload](https://www.syncfusion.com/angular-ui-components/angular-file-upload) feature tour page for its groundbreaking features. You can also explore our [Angular File Upload example](https://ej2.syncfusion.com/angular/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
