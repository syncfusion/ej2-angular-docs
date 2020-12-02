---
title: "Tooltip Open Mode"
component: "Tooltip"
description: "Angular tooltip supports the mode on which the Tooltip is to be opened on a page, i.e., on hovering, focusing, or clicking on the target elements."
---

# Open Mode

You can decide the mode on which the Tooltip is to be opened on a page, i.e., on hovering, focusing, or clicking on the target elements.

> On mobile devices, Tooltips appear when you tap and hold the element, even if the `opensOn` option is assigned with `Hover`.
> Tooltips are also displayed as long as you continue to tap and hold the element. On lift, it  disappears in the next 1.5 seconds.
> If there is another action before that time ends, then the Tooltip disappears.

The `opensOn` property can take either a single or a combination of multiple values, separated by space from the following options.
 The table  below explains how the Tooltip opens on both desktop and mobile based on the value(s) assigned to the `opensOn` property.
  By default, it takes `Auto` value.

| Values | Desktop | Mobile |
| ------------- | ------------- | ------------- |
| `Auto` | Tooltip appears when you hover over the target or when the target element receives the focus. | Tooltip opens on tap and hold of the target element. |
| `Hover` | Tooltip appears when you hover over the target. | Tooltip opens on tap and hold of the target element. |
| `Click` | Tooltip appears when you click a target element. | Tooltip appears when you single tap the target element. |
| `Focus` | Tooltip appears when you focus (say through tab key) on a target element. | Tooltip appears with a single tap on the target element. |
| `Custom` | Tooltip is not triggered by any default action. So, you have to bind your own events and use either `open` or `close` public methods. | Same as Desktop. |

To open the Tooltip for multiple actions, say while hovering over or clicking on a target element, the `opensOn` property can be assigned
 with multiple values, separated by space as `hover click`.

> `Auto` value cannot be used with any combination for multiple values.

The following code example shows how to set the open mode for Tooltips.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { TooltipComponent } from '@syncfusion/ej2-angular-popups';

@Component({
    selector: 'my-app',
    template: `
    <div id='container'>
        <table style="margin: 150px auto 0 auto;transform: translateY(-50%);">
            <tbody>
                <tr>
                    <td style="padding:25px">
                      <ejs-tooltip id="tooltipHover" opensOn='Hover' content='Tooltip from hover' >
                       <div>
                        <input ejs-button  class="blocks" type="button" value="Hover Me!"/></div>
                      </ejs-tooltip>
                    </td>
                    <td style="padding:25px">
                      <ejs-tooltip id="tooltipClick"  opensOn='Click' content='Tooltip from click'>
                       <div>
                        <input ejs-button  class="blocks" type="button" value="Click Me!"/></div>
                      </ejs-tooltip>
                    </td>
                </tr>
                <tr>
                    <td style="padding:25px">
                      <ejs-tooltip id="tooltipFocus" opensOn='Focus' content='Tooltip from focus' target='#input'>
                         <div>
                          <input id='input' class="blocks e-float-input" type="text" placeholder="Focus and blur"/>
                        </div>
                      </ejs-tooltip>
                    </td>
                    <td style="padding:25px">
                      <ejs-tooltip id="tooltipCustom" #tooltipCustom opensOn='custom' content='Tooltip from custom mode'>
                        <div>
                          <input ejs-button  class="blocks" id="tooltipOpen" type="button" value="Click to open tooltip manually" (click)='onCustomOpen($event)'/>
                        </div>
                      </ejs-tooltip>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
    `,
    styles: [`
    .blocks {
        width: 260px;
    }
    `]
})

export class AppComponent {
    @ViewChild('tooltipCustom')
    public tooltipCustom: TooltipComponent;
    constructor() { }
    onCustomOpen(args: any): void {
        if (args.target.getAttribute('data-tooltip-id')) {
            this.tooltipCustom.close();
        } else {
            this.tooltipCustom.open(args.target);
        }
    }
}

```

{% endtab %}

## Custom open mode

Other than the above specified options, the `custom` mode makes the Tooltip appear on screen for user-defined custom actions such as
 `right-click`, `double-click`, and so on. Here, the tooltip is not triggered by any default action, and you have to bind your own events
  and use either `open` or `close` public methods to show or hide the Tooltips.

The following code example shows how to define custom open mode for the Tooltip.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { TooltipComponent } from '@syncfusion/ej2-angular-popups';

@Component({
    selector: 'my-app',
    template: `
    <ejs-tooltip #tooltip id="tooltip" content='Tooltip from custom mode' opensOn='Custom' (dblclick)='customOpen($event)'>
            <span>Double-click to open Tooltip</span>
    </ejs-tooltip>
    `,
    styles: [`
    #tooltip {
        display: block;
        background-color: #cfd8dc;
        border: 3px solid #eceff1;
        box-sizing: border-box;
        margin: 80px auto;
        padding: 20px 0;
        width: 200px;
        text-align: center;
        color: #424242;
        font-size: 20px;
    }
    `]
})

export class AppComponent {
    @ViewChild('tooltip')
    public tooltipControl: TooltipComponent;
    constructor() { }
    customOpen(args: any): void {
        if (args.target.getAttribute("data-tooltip-id")) {
            this.tooltipControl.close();
        } else {
            this.tooltipControl.open(args.target);
        }
    }
}
```

{% endtab %}

## Sticky mode

With this mode set to `true`, Tooltips can be made to show up on the screen as long as the close icon is pressed. In this mode, close
 icon is attached to the Tooltip located at the top right corner. This mode can be enabled or disabled using the `isSticky` property.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
    <ejs-tooltip id="tooltip" content='Click close icon to close me' [isSticky]='true'>
            <span>Show tooltip</span>
    </ejs-tooltip>
    `,
    styles: [`
    #tooltip {
        display: block;
        background-color: #cfd8dc;
        border: 3px solid #eceff1;
        box-sizing: border-box;
        margin: 80px auto;
        padding: 20px 0;
        width: 200px;
        text-align: center;
        color: #424242;
        font-size: 20px;
    }
    `]
})

export class AppComponent {
}

```

{% endtab %}

## Open/Close Tooltip with delay

The Tooltips can be opened or closed after some delay by using the `openDelay` and `closeDelay` properties.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
    <ejs-tooltip id="tooltip" content='Tooltip with delay' [openDelay]='1000' [closeDelay]='1000'>
            Show tooltip
    </ejs-tooltip>
    `,
    styles: [`
    #tooltip {
        display: block;
        background-color: #cfd8dc;
        border: 3px solid #eceff1;
        box-sizing: border-box;
        margin: 80px auto;
        padding: 20px 0;
        width: 200px;
        text-align: center;
        color: #424242;
        font-size: 20px;
    }
    `]
})

export class AppComponent {
}

```

{% endtab %}
