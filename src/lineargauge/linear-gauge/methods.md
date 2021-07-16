---
title: " Methods in Angular Linear Gauge component | Syncfusion "

component: "Linear Gauge"

description: "Learn here all about the Methods of Syncfusion Angular Linear Gauge component and more."
---
# Methods in Angular Linear Gauge

The following methods are available in the Linear Gauge component.

## setPointerValue

To change the pointer value dynamically, use the [`setPointerValue`](../api/linear-gauge#setpointervalue) method in the Linear Gauge component. The following are the arguments for this method.

|   Argument name      |   Description                            |
|----------------------| -----------------------------------------|
|     axisIndex        |    Specifies the index of the axis in which the pointer value is to be updated.|
|     pointerIndex     |    Specifies the index of the pointer to be updated.           |
|     pointerValue     |    Specifies the value of the pointer to be updated.           |

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
@Component({
    selector: 'app-container',
    template: `
    <div> <button  id='btn' (click)='clicked()'>Click</button></div>
    <ejs-lineargauge id="gauge-container" #gauge>
        <e-axes>
         <e-axis>
           <e-pointers>
             <e-pointer value=80></e-pointer>
           </e-pointers>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`
})
export class AppComponent {
  @ViewChild('gauge')
  public gaugeObj: LinearGaugeComponent;
  clicked() {
    this.gaugeObj.setPointerValue(0, 0, 30);
  };
}
```

{% endtab %}

## setAnnotationValue

To change the annotation content dynamically, use the [`setAnnotationValue`](../api/linear-gauge#setannotationvalue) method in the Linear Gauge component. The following are the arguments for this method.

|   Argument name      |   Description                            |
|----------------------| -----------------------------------------|
|     annotationIndex  |    Specifies the index number of the annotation to be updated. |
|     content          |    Specifies the text for the annotation to be updated.        |
|     axisValue        |    Specifies the value of the axis where the annotation is to be placed.|

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { AnnotationsService, LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
@Component({
    selector: 'app-container',
    template: `
    <div> <button  id='btn' (click)='clicked()'>Click</button></div>
    <ejs-lineargauge id="gauge-container" #gauge>
        <e-annotations>
            <e-annotation zIndex='1' content='10' axisValue=0></e-annotation>
        </e-annotations>
        <e-axes>
         <e-axis>
           <e-pointers>
             <e-pointer value=10></e-pointer>
           </e-pointers>
         </e-axis>
      </e-axes>
    </ejs-lineargauge>`,
     providers: [AnnotationsService]
})
export class AppComponent {
  @ViewChild('gauge')
  public gaugeObj: LinearGaugeComponent;
  clicked() {
    this.gaugeObj.setAnnotationValue(0, '50', 50);
  };
}
```

{% endtab %}

## refresh

The [`refresh`](../api/linear-gauge#refresh) method can be used to change the state of the component and render it again. In the following example, the gauge is rendered again using the [`refresh`](../api/linear-gauge#refresh) method.

{% tab template= "linear-gauge/axis", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { LinearGaugeComponent } from '@syncfusion/ej2-angular-lineargauge';
@Component({
    selector: 'app-container',
    template: `
    <div> <button  id='btn' (click)='clicked()'>Click</button></div>
    <ejs-lineargauge id="gauge-container" #gauge>
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
  @ViewChild('gauge')
  public gaugeObj: LinearGaugeComponent;
  clicked() {
    this.gaugeObj.refresh();
  };
}
```

{% endtab %}