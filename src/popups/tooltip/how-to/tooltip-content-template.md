# Tooltip Content Template

The Tooltip component [content](https://ej2.syncfusion.com/angular/documentation/tooltip/content/) can be loaded through template support. Refer to the below code snippet.

{% tab template="tooltip/load-html", isDefaultActive=true, sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component, ViewChild, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
    <ejs-tooltip style="display:block;position:absolute;left:calc( 50% - 60px);top:45%;">
            <button ejs-button >Show Tooltip</button>
            <ng-template #content >
              Tooltip content here!!!
            </ng-template>
        </ejs-tooltip>
    `,
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
}

```

{% endtab %}
