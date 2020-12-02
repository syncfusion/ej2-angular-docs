# Dynamic tooltip content with HTML elements

The Tooltip component loads HTML tags using the [content](https://ej2.syncfusion.com/angular/documentation/tooltip/content/) template.

The HTML tags such as `<div>`, `<span>`, `bold`, `italic`, `underline`, etc., can be used. Style attributes can also be applied with HTML tags.

Here, Bold, Italic, Underline, and Anchor tags are used.

{% tab template="tooltip/load-html", isDefaultActive=true, sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component, ViewChild, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
    <div id="content">
        <h2>HTML Tags</h2>
          Through templates, <b><span style="color:#e3165b">tooltip content</span></b> can be loaded with <u><i> inline HTML, images, iframe, videos, maps </i></u>. A title can be added to the content
      </div>
      <div class="tooltipContent">
        <ejs-tooltip #tooltip id="tooltip" position='BottomCenter'>
          <ng-template #content>
            <div>
              Through templates,<b><span style="color:#e3165b">tooltip content</span></b> can be loaded with <u><i> inline HTML, images, iframe, videos, maps </i></u>. A title can be added to the content
            </div>
          </ng-template>
          <input ejs-button type="button" class="text" id="Title" value="HTML(With Title)" />
        </ejs-tooltip>
      </div>
    `,
    encapsulation: ViewEncapsulation.None,
})

export class AppComponent {
}

```

{% endtab %}
