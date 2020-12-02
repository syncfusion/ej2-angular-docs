---
title: "Change the text content and styles of the ProgressButton during progress"
component: "ProgressButton"
description: "Angular ProgressButton how to section, change text content and styles, hide spinner, customize progress."
---

# Change the text content and styles of the ProgressButton during progress

You can change the text content and styles of the ProgressButton during progress by changing the text content and the  [`cssClass`](../../api/progress-button#cssClass) property at the [`begin`](../../api/progress-button#begin) and [`end`](../../api/progress-button#end) events.

{% tab template="progress-button/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `<!-- To render progress button. -->
               <button ejs-progressbutton  [content]='content' [cssClass]='cssClass' [enableProgress]='true' [duration]='4000' (begin)='begin()' (end)='end()'></button>`
})

export class AppComponent {
    private content: string = 'Upload';
    private cssClass: string = 'e-hide-spinner';

    private begin(): void {
        this.content = 'Uploading...';
        this.cssClass = 'e-hide-spinner e-info';
    }
    private end(): void {
        this.content = 'Success';
        this.cssClass = 'e-hide-spinner e-success';
        setTimeout(() => {
            this.content = 'Upload';
            this.cssClass = 'e-hide-spinner';
        }, 500)
    }
}
```

{% endtab %}