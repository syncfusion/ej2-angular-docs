
# User Interaction

## Tooltip for pointers

Circular gauge will displays the pointer details through [tooltip](../api/circular-gauge/tooltipSettings),
when the mouse is moved over the pointer.

<!-- markdownlint-disable MD036 -->

**Enable Tooltip**

By default, tooltip is not visible. Enable the tooltip by setting
[`enable`](../api/circular-gauge/tooltipSettings/#enable-boolean) property to true and by injecting `GaugeTooltipService` into the `NgModule.providers`.

{% tab template="circulargauge/gauge-user-interaction", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" [tooltip]="tooltip">
        <e-axes>
            <e-axis>
                <e-pointers>
                    <e-pointer value=70></e-pointer>
                </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public tooltip: object;
    ngOnInit(): void {
        // Initialize objects
        this.tooltip = {
            enable: true
        };
    }

}

```

{% endtab %}

<!-- markdownlint-disable MD036 -->

**Template**

Any HTML elements can be displayed in the tooltip by using the
[`template`](../api/circular-gauge/tooltipSettings/#template-string) property of the tooltip.

{% tab template="circulargauge/gauge-user-interaction", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" [tooltip]="tooltip">
        <e-axes>
            <e-axis>
                <e-pointers>
                    <e-pointer value=70></e-pointer>
                </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public tooltip: object;
    ngOnInit(): void {
        // Initialize objects
        this.tooltip = {
            enable: true,
            template: '<div id="templateWrap">Pointer value:${value}</div>'
        };
    }

}

```

{% endtab %}

## Tooltip for ranges

Circular gauge displays the information about the ranges through tooltip when hovering the mouse over the ranges. You can enable this feature by setting the type property of tooltip to ‘Range’ in the array collection.

**Tooltip customization for ranges**

To customize the range tooltip, use the `rangeSettings` property in tooltip. The following options are available to customize the range tooltip:

* `fill` - Specifies the range tooltip fill color.
* `textStyle` - Specifies the range tooltip text style.
* `format` - Specifies the range content format.
* `template` - Specifies the custom template for tooltip.
* `enableAnimation` - Animates as it moves from one point to another.
* `border` - Specifies the tooltip border.
* `showMouseAtPosition` - Displays the position of the tooltip on the cursor position.

## Tooltip for annotations

Circular gauge displays the information about the annotations through tooltip when hovering the mouse over the annotation. You can enable this feature by setting the type property of tooltip to ‘Annotation’ in the array collection.

**Tooltip customization for annotations**

To customize the annotation tooltip, use the `annotationSettings` property in tooltip. The following options are available to customize the annotation tooltip:

* `fill` - Specifies the annotation tooltip fill color.
* `textStyle` - Specifies the annotation tooltip text style.
* `format` - Specifies the annotation content format.
* `template` - Specifies the tooltip content with custom template.
* `enableAnimation` - Animates as it moves from one point to another.
* `border` - Specifies the tooltip border.

The following code example shows the tooltip for the pointers, ranges and annotations.

{% tab template="circulargauge/gauge-user-interaction", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" [tooltip]="tooltip" enablePointerDrag=true>
        <e-axes>
            <e-axis minimum=0 maximum=120 radius="90%" startAngle= 240 endAngle=120 [majorTicks]="majorTicks" [minorTicks]="minorTicks" [lineStyle]="lineStyle" [annotations]='annotaions'>
                <e-pointers>
                    <e-pointer value=70 radius="60%" [cap]="cap"></e-pointer>
                </e-pointers>
                 <e-ranges>
                        <e-range start=0 end=50 radius='102%' startWidth=10 endWidth=10 color='#3A5DC8'></e-range>
                        <e-range start=50 end=120 radius='102%' startWidth=10 endWidth=10 color='#33BCBD'></e-range>
                </e-ranges>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public lineStyle: object;
    public majorTicks: object;
    public minorTicks: object;
    public tooltip: object;
    public cap: object;
    public annotaions;
    ngOnInit(): void {
        // Initialize objects
        this.tooltip = {
            type:['Pointer', 'Range', 'Annotation'],
            enable: true,
            enableAnimation: false,
            annotationSettings: { template:'<div>CircularGauge</div>' },
            rangeSettings: { fill:'red' }
        };
        this.lineStyle= {
            width: 0
        };
         this.majorTicks = {
            color: 'white', offset: -5, height: 12
        };
        this.minorTicks = {
            width: 0
        };
        this.annotaions = [{
        content: 'CircularGauge',
        angle: 180, zIndex: '1',
        }];
        this.cap= {
            radius: 10,
            border: {
                color: '#33BCBD',
                width: 5
                }
        };
    }

}

```

{% endtab %}

## Pointer Drag

Pointers can be dragged over the axis value.
This can be achieved by clicking and dragging the pointer.
To enable or disable the pointer drag, you can use [`enablePointerDrag`](../api/circular-gauge/#enablepointerdrag-boolean) property.

{% tab template="circulargauge/gauge-user-interaction", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'app-container',
    template:
    `<ejs-circulargauge id="circular-container" [tooltip]="tooltip" enablePointerDrag=true>
        <e-axes>
            <e-axis>
                <e-pointers>
                    <e-pointer value=70></e-pointer>
                </e-pointers>
            </e-axis>
        </e-axes>
    </ejs-circulargauge>`
})
export class AppComponent implements OnInit {
    public tooltip: object;
    ngOnInit(): void {
        // Initialize objects.
        this.tooltip = {
            enable: true,
            template: '<div id="templateWrap"><div style="float: right; padding-left:10px; line-height:30px;"><span>Pointer &nbsp;&nbsp;:&nbsp; ${Math.round(pointers[0].value)}</span></div></div>'
        };
    }

}

```

{% endtab %}