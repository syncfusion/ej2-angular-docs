---
title: "Customize button with HTML element"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Customize button with HTML element

The uploader component allows you to customize the action buttons by using the [buttons](../../api/uploader/#buttons) &nbsp;property. Refer to the following example.

{% tab template="uploader/custom-buttons", sourceFiles="app/**/*.ts,default.html,index.css" %}

```typescript
import { Component } from '@angular/core';
import { createElement } from '@syncfusion/ej2-base';
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
   public uploadEle: HTMLElement = createElement('span', { className: 'upload e-icons', innerHTML : 'Upload All' });
   public clearEle = createElement('span', { className: 'remove e-icons', innerHTML : 'Clear All' });
   public buttons: Object = {
    browse: 'Choose file',
    clear: this.clearEle,
    upload: this.uploadEle
   };
}

```

{% endtab %}
