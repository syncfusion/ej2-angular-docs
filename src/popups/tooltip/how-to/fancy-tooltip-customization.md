# Fancy tooltip customization

The arrow of the tooltip can be customized as needed by customizing CSS in the sample-side.
The EJ2 tooltip component is achieved through CSS3 format and positioned the tip arrow according to the tooltip positions like `TopCenter`, `BottomLeft`, `RightTop`, and more.

Here, the tip arrow is customized as Curved tooltip and Bubble tooltip.

** Curved tip **

The content for the tip pointer arrow has been added. To customize the curved tip arrow, override the following CSS class of tip arrow.

```typescript

      .e-arrow-tip-outer.e-tip-bottom,
      .e-arrow-tip-outer.e-tip-top {
           border-left: none !important;
           border-right: none !important;
           border-top: none !important;
      }
      .e-arrow-tip.e-tip-top {
           transform: rotate(170deg);
      }

```

** Bubble tip **

The two `divs`(inner div and outer div) have been added to achieve the bubble tip arrow. To customize the bubble tip arrow, override the following CSS class of tip arrow.

```typescript

    .e-arrow-tip-outer.e-tip-bottom, .e-arrow-tip-outer.e-tip-top
      {
         border-radius: 50px;
         height: 10px;
         width: 10px;
      }

      .e-arrow-tip-inner.e-tip-bottom, .e-arrow-tip-inner.e-tip-top
        {
         border-radius: 50px;
         height: 10px;
         width: 10px;
        }

```

These tip arrow customizations have been achieved through CSS changes in the sample level. The tooltip position can be changed by using the radio button click event.

The arrow tip pointer can also be disabled by using the [`showTipPointer`](https://ej2.syncfusion.com/angular/documentation/api/tooltip/#showtippointer) property in a tooltip.

{% tab template="tooltip/tip-custom", isDefaultActive=true, sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component, ViewChild, ViewEncapsulation } from '@angular/core';
import { TooltipComponent } from '@syncfusion/ej2-angular-popups';
import { RadioButtonComponent, ChangeArgs, ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'my-app',
    template: `
     <div id="customization">
      <ejs-tooltip #tooltipcurve cssClass='curvetips e-tooltip-css' content='Tooltip arrow customized'>
            <button id="target">
                Curve Tip Arrow
            </button>
        </ejs-tooltip>
       </div>
        <div id="positions">
            <ul>
             <li><ejs-radiobutton label="TopCenter" value="TopCenter" name="state" checked='true' (change)="onChange($event)"></ejs-radiobutton></li>
              <li><ejs-radiobutton label="BottomLeft" value="BottomLeft" name="state" (change)="onChange($event)"></ejs-radiobutton></li>
            </ul>
        </div>
     <div id="balloon">
      <ejs-tooltip #tooltip cssClass='bubbletip e-tooltip-css' content='Tooltip arrow customized as balloon tip' position='TopRight'>
            <button id="bubbletip">
                Bubble Tip Arrow
            </button>
        </ejs-tooltip>
       </div>
        <div id="btn">
            <ul>
             <li><ejs-radiobutton label="TopRight" value="TopRight" name="default" [checked]="true" (change)="onChanged($event)"></ejs-radiobutton></li>
              <li><ejs-radiobutton label="BottomLeft" value="BottomLeft" name="default" (change)="onChanged($event)"></ejs-radiobutton></li>
            </ul>
        </div>
        <ejs-tooltip #tooltip cssClass='pointertip e-tooltip-css' content='Disabled Tooltip Pointer' mouseTrail='true' [showTipPointer]='false'>
        <button id="tooltip">
            Disabled Tip Arrow
        </button>
        </ejs-tooltip>
    `,
    encapsulation: ViewEncapsulation.None,
})

export class AppComponent {
    @ViewChild('tooltip')
    public tooltipCustom: TooltipComponent;
    @ViewChild('tooltipcurve')
    public tooltipCurve: TooltipComponent;
    constructor() { }
    onChange(args: ChangeArgs): void {
        this.tooltipCurve.position = args.value as any;
        this.tooltipCurve.dataBind();
    }
    onChanged(args: ChangeArgs): void {
         this.tooltipCustom.position = args.value as any;
        if( this.tooltipCustom.position == 'BottomLeft'){
             this.tooltipCustom.offsetY = -30;
        } else {
             this.tooltipCustom.offsetY = 0;
        }
         this.tooltipCustom.dataBind();
    }
}

```

{% endtab %}
