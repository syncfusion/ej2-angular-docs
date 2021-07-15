---
title: "Trigger click event of input file from external button"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Trigger click event of input file from external button

You can trigger the click event of input file from external button using `click` event of button. In the below sample, triggered click event of input file from `Essential JavaScript 2 Button`.

{% tab template="uploader/external-click", sourceFiles="app/**/*.ts,default.html" %}

```typescript
import { Component, AfterViewInit } from '@angular/core';

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
    ngAfterViewInit(): void {
        document.getElementById('browse').onclick = (args) => {
            document.getElementsByClassName('e-file-select-wrap')[0].querySelector('button').click();
        };
    }
}
```

{% endtab %}

> You can also explore [Angular File Upload](https://www.syncfusion.com/angular-ui-components/angular-file-upload) feature tour page for its groundbreaking features. You can also explore our [Angular File Upload example](https://ej2.syncfusion.com/angular/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
