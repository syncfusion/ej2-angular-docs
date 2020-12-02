# Show tooltip on disabled elements and disable tooltip

By default, Tooltips will not be displayed on disabled elements. However, it is possible to enable this behavior by following the steps below.
1. Add a disabled element like the `button` element into a div whose display style is set to `inline-block`.
2. Set the pointer event as `none` for the disabled element (button) through CSS.
3. Now, initialize the Tooltip for outer div element that holds the disabled button element.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
    <ejs-tooltip id="tooltip" content='Tooltip from disabled element'>
        <div><input ejs-button type="button" disabled value="Disabled button" /></div>
    </ejs-tooltip>
    `,
    styles: [`
    #tooltip {
        display: inline-block;
        position: relative;
        top:50px;
        left: 40%;
    }
    #tooltip [disabled] {
        pointer-events: none;
        font-size: 22px;
        padding: 10px;
    }
    `]
})

export class AppComponent {
}

```

{% endtab %}
