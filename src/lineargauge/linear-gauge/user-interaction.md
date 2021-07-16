---
title: " User Interaction in Angular Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about the User Interaction feature of Syncfusion Angular Linear Gauge component and more."
---

# User Interaction in Angular Linear Gauge

<!-- markdownlint-disable MD036 -->

## Tooltip

<!-- markdownlint-disable MD036 -->

Linear Gauge displays the details about a pointer value through [`tooltip`](../api/linear-gauge/tooltipSettings/), when the mouse hovers over the pointer. To enable the tooltip, set [`enable`](../api/linear-gauge/tooltipSettingsModel/#enable) property as "**true**" and and inject the **GaugeTooltipService** in the **providers**.

{% tab template= "linear-gauge/user-interaction", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
        <ejs-lineargauge id='tooltipContainer' style='display:block;' [tooltip]='tooltip'>
            <e-axes>
                <e-axis>
                    <e-pointers>
                        <e-pointer value=80></e-pointer>
                    </e-pointers>
                </e-axis>
            </e-axes>
        </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public tooltip:Object;
    ngOnInit(): void {
        this.tooltip = {
            enable: true
        };
    }
}
```

{% endtab %}

<!-- markdownlint-disable MD013 -->

### Tooltip format

<!-- markdownlint-disable MD013 -->

Tooltip in the Linear Gauge control can be formatted using the [`format`](../api/linear-gauge/tooltipSettings/#format) property in [`tooltip`](../api/linear-gauge/tooltipSettings/). It is used to render the tooltip in certain format or to add a user-defined unit in the tooltip. By default, the tooltip shows the pointer value only. In addition to that, more information can be added in the tooltip. For example, the format "**{value}km**" shows pointer value with kilometer unit in the tooltip.

{% tab template= "linear-gauge/user-interaction", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" style='display:block;' [tooltip]='tooltip'>
        <e-axes>
            <e-axis>
            <e-pointers>
               <e-pointer value=80></e-pointer>
             </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public tooltip:Object;
    ngOnInit(): void {
        this.tooltip = {
             enable: true,
             format: '{value}km'
        };
    }
}
```

{% endtab %}

### Tooltip Template

The HTML element can be rendered in the tooltip of the Linear Gauge using the [`template`](../api/linear-gauge/tooltipSettings/#template) property in [`tooltip`](../api/linear-gauge/tooltipSettings/). The "**${value}**" can be used as placeholders in the HTML element to display the pointer values of the corresponding axis.

{% tab template= "linear-gauge/user-interaction", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" style='display:block;' [tooltip]='tooltip'>
        <e-axes>
            <e-axis>
            <e-pointers>
               <e-pointer value=80></e-pointer>
             </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public tooltip:Object;
    ngOnInit(): void {
        this.tooltip = {
            enable: true,
            //tooltip template for Linear gauge
            template: '<div>Pointer: 80 </div>'
        };
    }
}
```

{% endtab %}

### Customize the appearance of the tooltip

The tooltip can be customized using the following properties in [`tooltip`](../api/linear-gauge/tooltipSettings/).

* [`fill`](../api/linear-gauge/tooltipSettings/#fill) - To fill the color for tooltip.
* [`enableAnimation`](../api/linear-gauge/tooltipSettings/#enableanimation) - To enable or disable the tooltip animation.
* [`border`](../api/linear-gauge/tooltipSettings/#border) - To set the color and width for the border of the tooltip.
* [`textStyle`](../api/linear-gauge/tooltipSettings/#textstyle) - To customize the style of the text in tooltip.
* [`showAtMousePosition`](../api/linear-gauge/tooltipSettings/#showatmouseposition) - To show the tooltip at the mouse position.

{% tab template= "linear-gauge/user-interaction", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" style='display:block;' [tooltip]='tooltip'>
        <e-axes>
            <e-axis>
            <e-pointers>
               <e-pointer value=80></e-pointer>
             </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public tooltip:Object;
    ngOnInit(): void {
        this.tooltip = {
            enable: true,
            fill: '#e5bcbc',
            border: {
                color: '#d80000',
                width: 2
            }
        };
    }
}
```

{% endtab %}

### Positioning the tooltip

The tooltip is positioned at the "**End**" of the pointer. To change the position of the tooltip at the start, or center of the pointer, set the [`position`](../api/linear-gauge/tooltipSettings/#position) property to "**Start**" or "**Center**".

{% tab template= "linear-gauge/user-interaction", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" style='display:block;' [tooltip]='tooltip'>
        <e-axes>
            <e-axis>
            <e-pointers>
               <e-pointer value=50 type="Bar" color="blue"></e-pointer>
             </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    public tooltip:Object;
    ngOnInit(): void {
        this.tooltip = {
          enable: true,
          position: "Center"
        };
    }
}
```

{% endtab %}

## Pointer Drag

To drag either marker or bar pointer to the desired axis value, set the [`enableDrag`](../api/linear-gauge/pointer/#enabledrag) property as "**true**" in the [`pointer`](../api/linear-gauge/pointerModel/).

{% tab template= "linear-gauge/user-interaction", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-lineargauge id="gauge-container" style='display:block;' height='350'>
        <e-axes>
            <e-axis>
            <e-pointers>
               <e-pointer value=80 [enableDrag]=true></e-pointer>
             </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {
    }
}
```

{% endtab %}