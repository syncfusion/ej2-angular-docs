---
title: "Animation For Tooltip"
component: "Tooltip"
description: "Angular tooltip component supports various animation effects while showing or hiding the tooltip."
---

# Animation

To animate the Tooltip, a set of specific animation effects are available, and it can be controlled using the `animation` property.
 The animation property also allows you to set delay, duration, and various other effects of your choice.

[`AnimationModel`](../api/tooltip/animationModel) is derived from base to apply the chosen animation effect, duration, etc. on Tooltips.

By default, Tooltip entrance occurs over 150 ms using the `ease-out` timing function. It exits also at 150 ms,
but uses `ease-in` timing function.

The default animation effect for the Tooltip is set to `FadeIn` for its open action, and `FadeOut` for its close action.
The default `duration` is set to 150 ms and `delay` is set to 0.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
    <ejs-tooltip id="tooltip" content='Tooltip animation effect' [animation]='TooltipAnimation'>
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
    public TooltipAnimation: Object = {
        open: { effect: 'ZoomIn', duration: 1000, delay: 0 },
        close: { effect: 'ZoomOut', duration: 500, delay: 0 }
    };
}

```

{% endtab %}

## Animation effects

The animation effects that are applicable to Tooltips are:

* FadeIn
* FadeOut
* FadeZoomIn
* FadeZoomOut
* FlipXDownIn
* FlipXDownOut
* FlipXUpIn
* FlipXUpOut
* FlipYLeftIn
* FlipYLeftOut
* FlipYRightIn
* FlipYRightOut
* ZoomIn
* ZoomOut
* None

When the `effect` is specified as `none`, no effect will be applied to the Tooltip, and animation is considered to be set to `off`.

> Some of the above animation effects suits the Tooltip better when its tip pointer is hidden.
> This can be achieved by setting the `showTipPointer` to false.

## Animating via open/close methods

Animations can also be applied on Tooltips dynamically through `open` and `close` methods. These methods accept the animation model as an
 optional parameter. If you pass `TooltipAnimationSettings`, animation takes this model; otherwise, it takes the values from the
  `animation` property. It is also possible to pass different animations for Tooltips on each target.

Refer to the code snippet below to apply animations using public methods.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { TooltipComponent, TooltipAnimationSettings } from '@syncfusion/ej2-angular-popups';

@Component({
    selector: 'my-app',
    template: `
    <ejs-tooltip id="tooltip" #tooltipAnimate content='Tooltip animation effect' opensOn='Custom' (click)='onCustomClick($event)'>
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
    @ViewChild('tooltipAnimate')
    public tooltipControl: TooltipComponent;
    onCustomClick(args: any): void {
        if (args.target.getAttribute('data-tooltip-id')) {
            let closeAnimation: TooltipAnimationSettings = { effect: 'FadeOut', duration: 1000 }
            this.tooltipControl.close(closeAnimation);
        } else {
            let openAnimation: TooltipAnimationSettings = { effect: 'FadeIn', duration: 1000 }
            this.tooltipControl.open(args.target, openAnimation);
        }
    }
}

```

{% endtab %}

## Apply transition

The transition effect can be applied on Tooltips by using the `beforeOpen` event as given in the
 following work-around code example.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { TooltipComponent, TooltipEventArgs } from '@syncfusion/ej2-angular-popups';

@Component({
    selector: 'my-app',
    template: `
    <h3> Transition effect </h3>
    <ejs-tooltip id="tooltip" #tooltip class="e-prevent-select" target='.circle-tool' [closeDelay]='1000' [animation]='Animation'
     (beforeRender)='onBeforeRender($event)' (beforeOpen)='onBeforeOpen($event)' (afterClose)='onAfterClose($event)'>
        <div class="circle-tool" style="top:18%;left:5%" title="This is Turtle !!!"></div>
        <div class="circle-tool" style="top:30%;left:30%" title="This is Snake !!!"></div>
        <div class="circle-tool" style="top:80%;left:80%" title="This is Croc !!!"></div>
        <div class="circle-tool" style="top:65%;left:50%" title="This is String Ray !!!"></div>
        <div class="circle-tool" style="top:75%;left:15%" title="This is Blob Fish !!!"></div>
        <div class="circle-tool" style="top:30%;left:70%" title="This is Mammoth !!!"></div>
    </ejs-tooltip>
    `,
    styles: [`
    #tooltip {
        display: block;
        border: 1px solid #c8c8c8;
        height: 200px;
        margin-left: 10px;
        margin-right: 10px;
        position: relative;
    }

    .circle-tool {
        position: absolute;
        width: 20px;
        height: 20px;
        background: #9acd32;
        -moz-border-radius: 50px;
        -webkit-border-radius: 50px;
        border-radius: 50px;
    }
    `],
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
    @ViewChild('tooltip')
    public tooltipControl: TooltipComponent;
    public Animation: Object = {
        open: { effect: 'ZoomIn', duration: 500 },
        close: { effect: 'ZoomOut', duration: 500 }
    };
    onBeforeRender(args: TooltipEventArgs): void {
        if (args.element) {
            this.tooltipControl.animation = { open: { effect: 'None' } };
        }
    }
    onBeforeOpen(args: TooltipEventArgs): void {
        if (args.element) {
            args.element.style.display = 'block';
            args.element.style.transitionProperty = 'left,top';
            args.element.style.transitionDuration = '1000ms';
        }
    }
    onAfterClose(args: TooltipEventArgs): void {
        this.tooltipControl.animation = {
            open: { effect: 'ZoomIn', duration: 500 },
            close: { effect: 'ZoomOut', duration: 500 }
        };
    }
}

```

{% endtab %}
