---
title: " Events in Angular Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about Events of Syncfusion Angular Linear Gauge component and more."
---

# Events in Angular Linear Gauge

This section describes the Linear Gauge component's event that gets triggered when corresponding operations are performed.

## animationComplete

When the pointer animation is completed, the [`animationComplete`](../api/linear-gauge#animationcomplete) event will be triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iAnimationCompleteEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IAnimationCompleteEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (animationComplete)='animationComplete($event)'>
        <e-axes>
         <e-axis>
           <e-pointers>
             <e-pointer value=10></e-pointer>
           </e-pointers>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    animationComplete(args: IAnimationCompleteEventArgs) {
    };
}
```

{% endtab %}

## annotationRender

Before the annotation is rendered in the Linear Gauge, the [`annotationRender`](../api/linear-gauge#annotationrender) event will be triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iAnnotationRenderEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { AnnotationService, LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IAnnotationRenderEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (annotationRender)='annotationRender($event)'>
        <e-annotations>
            <e-annotation zIndex='1' content='<div id="first"><h1>Gauge</h1></div>' axisValue=0></e-annotation>
        </e-annotations>
    </ejs-lineargauge>`,
    providers: [AnnotationService]
})
export class AppComponent {
    annotationRender(args: IAnnotationRenderEventArgs) {
    };
}
```

{% endtab %}

## axisLabelRender

Before each axis label is rendered in the Linear Gauge, the [`axisLabelRender`](../api/linear-gauge#axislabelrender) event is fired. To know more about the arguments of this event, refer [here](../api/linear-gauge/iAxisLabelRenderEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IAxisLabelRenderEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (axisLabelRender)='axisLabelRender($event)'>
    </ejs-lineargauge>`
})
export class AppComponent {
    axisLabelRender(args: IAxisLabelRenderEventArgs) {
    };
}
```

{% endtab %}

## beforePrint

The [`beforePrint`](../api/linear-gauge/#beforeprint) event is fired before the print begins. To know more about the arguments of this event, refer [here](../api/linear-gauge/iPrintEventArgs/).

{% tab template= "linear-gauge/print-and-export", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { PrintService, LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IPrintEventArgs } from '@syncfusion/ej2-lineargauge';
@Component({
    selector: 'app-container',
    template: `
    <div><button id='print' (click)='print()'>Print</button></div>
    <ejs-lineargauge id="gauge-container" [allowPrint]=true (beforePrint)='beforePrint($event)' #gauge>
    </ejs-lineargauge>`,
    providers: [PrintService]
})
export class AppComponent {
  @ViewChild('gauge')
  public gaugeObj: LinearGaugeComponent;
  print() {
    this.gaugeObj.print();
  };
  beforePrint(args: IPrintEventArgs) {
  };
}
```

{% endtab %}

## dragEnd

The [`dragEnd`](../api/linear-gauge#dragend) event will be fired before the pointer drag is completed. To know more about the argument of this event, refer [here](../api/linear-gauge/iPointerDragEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IPointerDragEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (dragEnd)='dragEnd($event)'>
        <e-axes>
         <e-axis>
           <e-pointers>
             <e-pointer enableDrag=true></e-pointer>
           </e-pointers>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    dragEnd(args: IPointerDragEventArgs) {
    }
}
```

{% endtab %}

## dragMove

The [`dragMove`](../api/linear-gauge#dragmove) event will be fired when the pointer is dragged. To know more about the arguments of this event, refer [here](../api/linear-gauge/iPointerDragEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IPointerDragEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (dragMove)='dragMove($event)'>
        <e-axes>
         <e-axis>
           <e-pointers>
             <e-pointer enableDrag=true></e-pointer>
           </e-pointers>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    dragMove(args: IPointerDragEventArgs) {
    }
}
```

{% endtab %}

## dragStart

When the pointer drag begins, the [`dragStart`](../api/linear-gauge#dragstart) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iPointerDragEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IPointerDragEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (dragStart)='dragStart($event)'>
        <e-axes>
         <e-axis>
           <e-pointers>
             <e-pointer enableDrag=true></e-pointer>
           </e-pointers>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    dragStart(args: IPointerDragEventArgs) {
    }
}
```

{% endtab %}

## gaugeMouseDown

When mouse is pressed down on the gauge, the [`gaugeMouseDown`](../api/linear-gauge#gaugemousedown) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iMouseEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IMouseEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (gaugeMouseDown)='gaugeMouseDown($event)'>
    </ejs-lineargauge>`
})
export class AppComponent {
    gaugeMouseDown(args: IMouseEventArgs) {
    }
}
```

{% endtab %}

## gaugeMouseLeave

When mouse pointer moves over the gauge, the [`gaugemouseleave`](../api/linear-gauge#gaugemouseleave) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iMouseEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IMouseEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (gaugeMouseLeave)='gaugeMouseLeave($event)'>
    </ejs-lineargauge>`
})
export class AppComponent {
    gaugeMouseLeave(args: IMouseEventArgs) {
    }
}
```

{% endtab %}

## gaugeMouseMove

When mouse pointer leaves the gauge, the [`gaugeMouseMove`](../api/linear-gauge#gaugemousemove) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iMouseEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IMouseEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (gaugeMouseMove)='gaugeMouseMove($event)'>
    </ejs-lineargauge>`
})
export class AppComponent {
    gaugeMouseMove(args: IMouseEventArgs) {
    }
}
```

{% endtab %}

## gaugeMouseUp

When the mouse pointer is released over the Linear Gauge, the [`gaugeMouseUp`](../api/linear-gauge#gaugemouseup) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iMouseEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IMouseEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (gaugeMouseUp)='gaugeMouseUp($event)'>
    </ejs-lineargauge>`
})
export class AppComponent {
    gaugeMouseUp(args: IMouseEventArgs) {
    }
}
```

{% endtab %}

## load

Before the Linear Gauge is loaded, the [`load`](../api/linear-gauge#load) event is fired. To know more about the arguments of this event, refer [here](../api/linear-gauge/iLoadEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { ILoadEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (load)='load($event)'>
    </ejs-lineargauge>`
})
export class AppComponent {
    load(args: ILoadEventArgs) {
    }
}
```

{% endtab %}

## loaded

After the Linear Gauge has been loaded, the [`loaded`](../api/linear-gauge#loaded) event will be triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iLoadedEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { ILoadedEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (loaded)='loaded($event)'>
    </ejs-lineargauge>`
})
export class AppComponent {
    loaded(args: ILoadedEventArgs) {
    }
}
```

{% endtab %}

## resized

After the window resizing, the [`resized`](../api/linear-gauge#resized) event is triggered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iResizeEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IResizeEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (resized)='resized($event)'>
    </ejs-lineargauge>`
})
export class AppComponent {
    resized(args: IResizeEventArgs) {
    }
}
```

{% endtab %}

## tooltipRender

The [`tooltipRender`](../api/linear-gauge#tooltiprender) event is fired before the tooltip is rendered. To know more about the arguments of this event, refer [here](../api/linear-gauge/iTooltipRenderEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { ITooltipRenderEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (tooltipRender)='tooltipRender($event)'>
    </ejs-lineargauge>`
})
export class AppComponent {
    tooltipRender(args: ITooltipRenderEventArgs) {
    }
}
```

{% endtab %}

## valueChange

The [`valueChange`](../api/linear-gauge#valuechange) event is triggered when the pointer is dragged from one value to another. To know more about the arguments of this event, refer [here](../api/linear-gauge/iValueChangeEventArgs/).

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
import { IValueChangeEventArgs } from '@syncfusion/ej2-lineargauge';

@Component({
    selector: 'app-container',
    template: `
    <ejs-lineargauge id="gauge-container" (valueChange)='valueChange($event)'>
        <e-axes>
         <e-axis>
           <e-pointers>
             <e-pointer value=40 enableDrag=true></e-pointer>
           </e-pointers>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
    valueChange(args: IValueChangeEventArgs) {
    }
}
```

{% endtab %}
