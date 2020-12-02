---
title: "WAI-ARIA Accessibility"
component: "Uploader"
description: "Describes the accessibility standard of the file upload control such as WAI-ARIA attributes, keyboard interaction, theming, etc."
---

# Accessibility

The uploader component characterized with complete ARIA accessibility support that helps to be accessible by on-screen
readers and other assistive technology devices.

## Keyboard interaction

The following are the standard keys that works on uploader component:

| **Keyboard shortcuts** | **Actions** |
| --- | --- |
| <kbd>Tab</kbd> | Move focus to next element. |
| <kbd>Shift + Tab</kbd> | Move focus to previous element. |
| <kbd>Enter</kbd> | Triggers corresponding action to button element. |
| <kbd>Esc</kbd> | Close the file browser dialog alone and cancels the upload on drop the file. |

{% tab template="uploader/uploader", sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
               <ejs-uploader #defaultupload  [asyncSettings]='path'></ejs-uploader>
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