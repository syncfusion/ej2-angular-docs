---
title: "Customize progress using cssClass"
component: "ProgressButton"
description: "Angular ProgressButton how to section, change text content and styles, hide spinner, customize progress."
---

# Customize progress using cssClass

You can customize the background filler UI using the [`cssClass`](../../api/progress-button#cssClass) property.

* Adding `e-vertical` to `cssClass` shows vertical progress.
* Adding `e-progress-top` to `cssClass` shows progress at the top.

You can also show reverse progress by adding custom class to the [`cssClass`](../../api/progress-button#cssClass) property.

{% tab template="progress-button/default", sourceFiles="app/**/*.ts,progress.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<button ejs-progressbutton content='Vertical Progress' [enableProgress]='true' cssClass='e-hide-spinner e-vertical' [duration]='4000'></button>
    <button ejs-progressbutton content='Progress Top' [enableProgress]='true' cssClass='e-hide-spinner e-progress-top' [duration]='4000'></button>
    <button ejs-progressbutton content='Reverse Progress' [enableProgress]='true' cssClass='e-hide-spinner e-reverse-progress' [duration]='4000'></button>`
})

export class AppComponent {
}
```

{% endtab %}