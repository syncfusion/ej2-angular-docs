---
title: "Setting Dimension for Tooltip"
component: "Tooltip"
description: "Angular tooltip component’s dimension can either be assigned auto height and width values or specific pixel values."
---

# Setting Dimension

## Height and width

The Tooltip can either be assigned auto height and width values or specific pixel values. The `width` and `height` properties are used to
 set the outer dimension of the Tooltip element. The default value for both the properties is `auto`.
  It also accepts string and number values in pixels.

The following sample explains how to set dimensions for the Tooltip.

{% tab template="tooltip/getting-started-002", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `
    <div id='container' >
        <ejs-tooltip style="display: inline-block; position: relative; left: 50%;top: 100px;transform: translateX(-50%); padding: 60px 40px 40px 0" id='tooltip' width= '180px' height= '40px' content= 'This tooltip has 180px width and 40px height' target="#target">
            <button ejs-button id="target">Show Tooltip</button>
        </ejs-tooltip>
    </div>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent  { }
```

{% endtab %}

### Scroll mode

When `height` is specified with a certain pixel value and the Tooltip content overflows, the scrolling mode gets enabled.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
        <p>A green home is a type of house designed to be
            <ejs-tooltip id='tooltip' width='300px' height='60px' isSticky='true' [content]='tooltipContent'>
            <a><u>environmentally friendly</u></a>
            </ejs-tooltip> and sustainable. And also focuses on the efficient use of "energy, water, and building materials." As green homes
            have become more prevalent we have also seen the emergence of green affordable housing.
        </p>
        `,
    encapsulation: ViewEncapsulation.None,
})
export class AppComponent {
    tooltipContent: HTMLElement = document.createElement('div');
    constructor() {
        this.tooltipContent =
            '<div id="tooltipContent"><p><b>Environmentally friendly</b> or environment-friendly, (also referred to as eco-friendly, nature-friendly, and green) are marketing and sustainability terms referring to goods and services, laws, guidelines and policies that inflict reduced, minimal, or no harm upon ecosystems or the environment.</p></div>';
    }
}
```

{% endtab %}

> The scrolling mode can best be seen when the sticky mode of the Tooltip is enabled. To enable sticky mode, set the `isSticky` property to true.
