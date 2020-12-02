---
title: "Tooltip for Button"
component: "Button"
description: "Angular Button how to section, block button, repeat button, tooltip for Button, customization of button appearance, input and anchor elements."
---

# Tooltip for Button

Tooltip can be shown on button hover and it can be achieved by setting `title` attribute.

The following snippets illustrates how to show tooltip on button hover.

{% tab template="button/block", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-root',
    styleUrls:['styles.css'],
    template:  `<button #btn ejs-button [isPrimary]="true">Button</button>`
})

export class AppComponent implements OnInit {
  @ViewChild('btn')
  private btn: ButtonComponent;
  ngOnInit() {
    this.btn.element.setAttribute("title", "Primary Button")
  }
}
```

{% endtab %}