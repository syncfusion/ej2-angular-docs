# Ruler

The Ruler provides a horizontal and vertical guide for measuring in the Diagram control. The Ruler can be used to measure the diagram objects, indicate positions, and align diagram elements. This is especially useful in creating scale models.

## Adding Rulers to the Diagram

* The [`rulerSettings`](https://ej2.syncfusion.com/angular/documentation/api/diagram/rulerSettings/)property is used to control the visibility and appearance of the ruler in the diagram.

* The RulerSettings [`showRulers`](https://ej2.syncfusion.com/angular/documentation/api/diagram/rulerSettings/#showrulers)property is used to show or hide the rulers in the diagram.

* The RulerSettings [`horizontalRuler`](https://ej2.syncfusion.com/angular/documentation/api/diagram/rulerSettings/#horizontalruler) and [`verticalRuler`](https://ej2.syncfusion.com/angular/documentation/api/diagram/rulerSettings/#verticalruler) properties are used to customize the rulers appearance in the diagram.

The following code shows how to add a ruler to the diagram.

{% tab template="diagram/ruler/ruler", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent,OverviewComponent, Diagram, NodeModel, ConnectorModel,OverviewModel, SnapSettingsModel, LayoutModel, DataSourceModel,  } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<div><ejs-diagram #diagram id="diagram" width="100%" height="600px" [rulerSettings]='rulerSettings'></ejs-diagram></div>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
     @ViewChild('diagram')
    public diagram: DiagramComponent;
    public rulerSettings: RulerSettingsModel = { showRulers: true}
}
```

{% endtab %}

## Customizing the Ruler

By default, the ruler segments are arranged based on pixel values.

* The HorizontalRuler’s [`interval`](https://ej2.syncfusion.com/angular/documentation/api/diagram/diagramRuler/#interval)property allows you to define the interval between ruler segments and the [`segmentWidth`](https://ej2.syncfusion.com/angular/documentation/api/diagram/diagramRuler/#segmentwidth) property allows you to define the segment width of the ruler. Similarly, you can use the VerticalRuler’s [`interval`](https://ej2.syncfusion.com/angular/documentation/api/diagram/diagramRuler/#interval) and [`segmentWidth`](https://ej2.syncfusion.com/angular/documentation/api/diagram/diagramRuler/#segmentwidth) properties are used to define the interval and segment width of the vertical ruler

* The HorizontalRuler’s [`tickAlignment`](https://ej2.syncfusion.com/angular/documentation/api/diagram/diagramRuler/#tickalignment) property is used to align the ruler tick either left or right side of the ruler. The VerticalRuler’s [`tickAlignment`](https://ej2.syncfusion.com/angular/documentation/api/diagram/diagramRuler/#tickalignment) property is used to align the ruler tick either top or bottom side of the ruler.

* The HorizontalRuler’s [`arrangeTick`](https://ej2.syncfusion.com/angular/documentation/api/diagram/diagramRuler/#arrangetick) and VerticalRuler’s [`arrangeTick`](https://ej2.syncfusion.com/angular/documentation/api/diagram/diagramRuler/#arrangetick) function is provided for the purpose of customizing the appearance of ruler ticks. It will be called for each tick rendering.

* The HorizontalRuler’s [`markerColor`](https://ej2.syncfusion.com/angular/documentation/api/diagram/diagramRuler/#markercolor) and VerticalRuler’s [`markerColor`](https://ej2.syncfusion.com/angular/documentation/api/diagram/diagramRuler/#markercolor) properties are used to define the ruler marker color and marker will be shown when performing the interaction in the diagram.

The following code shows how the diagram ruler can be customized.

{% tab template="diagram/ruler/ruler", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent,OverviewComponent, Diagram, NodeModel, ConnectorModel,OverviewModel, SnapSettingsModel, LayoutModel, DataSourceModel,  } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<div><ejs-diagram #diagram id="diagram" width="100%" height="600px" [rulerSettings]='rulerSettings'></ejs-diagram></div>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
     @ViewChild('diagram')
    public diagram: DiagramComponent;
    public rulerSettings: RulerSettingsModel = { showRulers: true, horizontalRuler:{interval:8, segmentWidth:100, thickness:25, tickAlignment:"LeftOrTop"},verticalRuler:{interval:10, segmentWidth:150, thickness:35, tickAlignment:"RightOrBottom"}  }
}
```

{% endtab %}
>Note : The MarkerColor property can be customized using the [`marker`](./style/#customizing-the-ruler) CSS style.
