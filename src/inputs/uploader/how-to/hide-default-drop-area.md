---
title: "Hide default drop area"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Hide default drop area

You can achieve this behavior by override the corresponding uploader styles. In the following example, override the below styles to hide the default drop area behavior.

    * .e-upload.e-control
    * .e-upload .e-file-select
    * .e-upload .e-file-drop

{% tab template="uploader/hide-drop",  sourceFiles="app/**/*.ts,default.html,index.css" %}

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
