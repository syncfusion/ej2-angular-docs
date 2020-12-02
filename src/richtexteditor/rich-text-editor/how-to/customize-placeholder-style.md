---
title: "Rich Text Editor How To customize the placeholder style"
component: "Rich Text Editor"
description: "This section for Syncfusion Angular Rich Text Editor component explains the customization of placeholder style."
---

# How to customize the placeholder style

By using `e-rte-placeholder` class, you can customize the placeholder style.

{% tab template="rich-text-editor/how-to/placeholder", sourceFiles="app/**/*.ts,index.html" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService  } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
  selector: 'app-root',
  template: `<ejs-richtexteditor id='defaultRTE' #sample [placeholder]='placeholder'></ejs-richtexteditor>`,
  providers: [ToolbarService, LinkService, ImageService, HtmlEditorService ]
})
export class AppComponent  {
  public placeholder: String = 'Type Something';
}


```

{% endtab %}
