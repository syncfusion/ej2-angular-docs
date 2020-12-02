---
title: "Globalization"
component: "Splitter"
description: "This section explains the localization support of Syncfusion Splitter component."
---

# Globalization

## RTL

Specifies the direction of the Splitter component using the enableRtl property. For writing systems that require it like Arabic, Hebrew, etc., the direction can be switched to right-to-left.

The following code shows how to enable RTL behavior.

{% tab template="splitter/rtl", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
      <div id='container'>
         <ejs-splitter #plain height='200px' width='600' enableRtl='true'>
            <e-panes>
                <e-pane size='200px' content='<div class="content">Left pane</div>'>
                </e-pane>
                <e-pane size='200px' content='<div class="content">Middle pane</div>'>
                </e-pane>
                <e-pane size='200px' content='<div class="content">Right pane</div>'>
                </e-pane>
            </e-panes>
          </ejs-splitter>
      </div>`
})
export class AppComponent {
    constructor() {
    }
}

```

{% endtab %}

## See Also

* [Construct different layouts using Splitter](./different-layouts)