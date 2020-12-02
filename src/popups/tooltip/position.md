---
title: "Tooltip Position"
component: "Tooltip"
description: "Angular tooltip can be displayed in 12 (twelve) different positions of target element that automatically collide based on view port."
---

# Tooltip Positioning

Tooltips can be attached to 12 static locations around the target.
On initializing the Tooltip, you can set the position property with any one of the following values:

* `TopLeft`

* `TopCenter`

* `TopRight`

* `BottomLeft`

* `BottomCenter`

* `BottomRight`

* `LeftTop`

* `LeftCenter`

* `LeftBottom`

* `RightTop`

* `RightCenter`

* `RightBottom`

> By default, Tooltip is placed at the `TopCenter` of the target element.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild, ViewEncapsulation } from '@angular/core';
import { TooltipComponent, Position } from '@syncfusion/ej2-angular-popups';

@Component({
    selector: 'my-app',
    template: `
    <div style='display: inline-flex;position:  relative;left:  50%;transform:  translateX(-50%);margin-top:  100px;'>
      <div>
        <ejs-tooltip #tooltip id='tooltip' content='Tooltip content' >
            <button ejs-button id="target">Show Tooltip</button>
        </ejs-tooltip>
    </div>
    <div>
         <select id="positions" (change)="onChange($event.target.value)" class="form-control">
             <option value="TopLeft">Top Left</option>
             <option value="TopCenter" selected>Top Center</option>
             <option value="TopRight">Top Right</option>
             <option value="BottomLeft">Bottom Left</option>
             <option value="BottomCenter">Bottom Center</option>
             <option value="BottomRight">Bottom Right</option>
             <option value="LeftTop">Left Top</option>
             <option value="LeftCenter">Left Center</option>
             <option value="LeftBottom">Left Bottom</option>
             <option value="RightTop">Right Top</option>
             <option value="RightCenter">Right Center</option>
             <option value="RightBottom">Right Bottom</option>
        </select>
    </div>
    </div>
    `,
    styles: [
        `
    #tooltip {
        padding: 5px;
        margin-right: 20px;
    }
    `,
    ],
    encapsulation: ViewEncapsulation.None,
})
export class AppComponent {
    @ViewChild('tooltip') public control: TooltipComponent;
    onChange(value: string) {
        this.control.position = value as Position;
    }
}
```

{% endtab %}

## Tip pointer positioning

The Tooltip pointer can be attached or detached from the Tooltip by using the `showTipPointer` property.
Pointer positions can be adjusted using the `tipPointerPosition` property that can be assigned to one of the following values:

* `Auto`

* `Start`

* `Middle`

* `End`

The following code example illustrates how to set the pointer to the start position of the Tooltip.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
        <ejs-tooltip id="tooltip" content='Tooltip content' tipPointerPosition='Start'>
            <button ejs-button>Show tooltip</button>
        </ejs-tooltip>
        `,
    styles: [`
        #tooltip {
           display: block;
            margin: 80px auto;
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

By default, tip pointers are auto adjusted so that the arrow does not point outside the target element.

## Dynamic positioning

The Tooltip and its tip pointer can be positioned dynamically based on the target's location. This can be achieved by using the `refresh`
 method, which auto adjusts the Tooltip over the target.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild, Inject } from '@angular/core';
import { TooltipComponent } from '@syncfusion/ej2-angular-popups';
import { Draggable } from '@syncfusion/ej2-base';

@Component({
    selector: 'my-app',
    template: `
    <ejs-tooltip #tooltip id='targetContainer' content='Drag me !!!' target='#demoSmart' [animation]='tooltipAnimation'>
        <div id="demoSmart">
        </div>
    </ejs-tooltip>
    `,
    styles: [`
    #targetContainer {
        position: relative;
        height: 360px;
        overflow: hidden;
        border: 1px solid #c8c8c8;
        display: block;
    }

    #demoSmart {
        width: 50px;
        height: 50px;
        background: rebeccapurple;
        position: absolute;
        left: 35%;
        top: 35%;
    }
    `]
})

export class AppComponent {
    @ViewChild('tooltip')
    public tooltipControl: TooltipComponent;
    public tooltipAnimation: Object = {
        open: { effect: 'None' },
        close: { effect: 'None' }
    };

    ngOnInit(): void {
        let ele: HTMLElement = document.getElementById('demoSmart');
        let drag: Draggable = new Draggable(ele, {
            clone: false,
            dragArea: '#targetContainer',
            drag: (args: any) => {
                this.tooltipControl.refresh(args.element);
            },
            dragStart: (args: any) => {
                this.tooltipControl.open(args.element);
            },
            dragStop: (args: any) => {
                this.tooltipControl.close();
            }
        });
    }
}

```

{% endtab %}

## Mouse trailing

Tooltips can be positioned relative to the mouse pointer. This behavior can be enabled or disabled by using the `mouseTrail` property.
 By default, it is set to `false`.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
        <ejs-tooltip id="tooltip" content='Tooltip content' [mouseTrail]='true'>
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

> When mouse trailing option is enabled, the tip pointer position gets auto adjusted based on the target, and
> other position values like start, end, and middle are not applied (to prevent the pointer from moving out of target).

## Setting offset values

Offset values are set to specify the distance between the target and tooltip element.
`offsetX` and `offsetY` properties are used to specify the offset left and top values.

* `offsetX` specifies the distance between the target and Tooltip element in X axis.
* `offsetY` specifies the distance between the target and Tooltip element in Y axis.

The following code example illustrates how to set offset values.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
        <ejs-tooltip id="tooltip" content='Tooltip content' [offsetX]='30' [offsetY]='30' [mouseTrail]='true' [showTipPointer]='false'>
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

> By default, collision is handled automatically and therefore when collision is detected the Tooltip fits horizontally and flips vertically.
