# Custom tooltip with dynamic HTML

Tooltip loads HTML pages via HTML tags such as iframe, video, and map using the [`content`](https://ej2.syncfusion.com/angular/documentation/api/tooltip/#content) property, which supports both string and HTML tags.

To load an `iframe` element in tooltip, set the required iframe in the `content` of tooltip while initializing the tooltip component. Refer to the following code.

```typescript

content= '<iframe src="https://www.syncfusion.com/products/essential-js2"></iframe>

```

{% tab template="tooltip/html-page", isDefaultActive=true, sourceFiles="app/**/*.ts,index.css"  %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { TooltipComponent } from '@syncfusion/ej2-angular-popups';

@Component({
    selector: 'my-app',
    template: `
       <div id="tooltipContent">
            <div class="content">
            <ejs-tooltip cssClass='e-tooltip-css' position='BottomCenter' opensOn='Click'>
                <!-- iframe element -->
                 <ng-template #content>
                 <iframe src="https://www.syncfusion.com/products/essential-js2"></iframe>
                </ng-template>
                <button ejs-button class="text" id="iframeContent" cssClass='e-outline' isPrimary=true>Embedded Iframe</button>
            </ejs-tooltip>
            </div>
        </div>`,
    encapsulation: ViewEncapsulation.None,
})

export class AppComponent {
}

```

{% endtab %}
