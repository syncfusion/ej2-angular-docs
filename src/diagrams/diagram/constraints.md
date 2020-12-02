---
title: "Constraints"
component: "Diagram"
description: "Diagram constraints allow you to enable/disable certain behaviors of the diagram, nodes and connectors."
---

# Constraints

Constraints are used to enable/disable certain behaviors of the diagram, nodes and connectors. Constraints are provided as flagged enumerations, so that multiple behaviors can be enabled/disabled using Bitwise operators (&, |, ~, <<, etc.).

To know more about Bitwise operators, refer to [`Bitwise Operations`](#bitwise-operations).

## Diagram constraints

Diagram constraints allow to enable or disable the following behaviors:

* Page editing
* Bridging
* Zoom and pan
* Undo/redo
* Tooltip

The following example illustrates how to give page editing using the diagram constraints.

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { DiagramConstraints } from '@syncfusion/ej2-diagrams';
@Component({
  selector: "app-container",
  // specifies the template string for the diagram component
  template: `<ejs-diagram id="diagram" width="100%" height="580px" [constraints]='diagramConstraints'></ejs-diagram>`
})
export class AppComponent {
    @ViewChild("diagram")
    public diagramConstraints: DiagramConstraints;
    ngOnInit(): void {
        this.diagramConstraints = DiagramConstraints.Default & ~DiagramConstraints.PageEditable;
    }
}

```

For more information about diagram constraints, refer to [`DiagramConstraints`](../api/diagram/diagramConstraints).

## Node constraints

Node constraints allows to enable or disable the following behaviors of node. They are as follows:

* Selection
* Deletion
* Drag
* Resize
* Rotate
* Connect
* Shadow
* Tooltip

The following example illustrates how to disable rotation using the node constraints.

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { NodeConstraints } from "@syncfusion/ej2-angular-diagrams";

@Component({
    selector: "app-container",
    template: `<ejs-diagram id="diagram" width="100%" height="580px">
        <e-nodes>
            <e-node id='node1' [height]=60 [width]=100 [offsetX]=300 [offsetY]=80 [constraints]='nodeConstraints'>
            </e-node>
        </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public nodeConstraints: NodeConstraints;
    ngOnInit(): void {
        this.nodeConstraints = NodeConstraints.Default & ~NodeConstraints.Rotate;
    }
}
```

For more information about node constraints, refer to [`NodeConstraints`](../api/diagram/nodeConstraints).

## Connector constraints

Connector constraints allow to enable or disable certain behaviors of connectors.

* Selection
* Deletion
* Drag
* Segment editing
* Tooltip
* Bridging

The following code illustrates how to disable selection by using connector constraints.

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { ConnectorConstraints, PointModel } from "@syncfusion/ej2-angular-diagrams";

@Component({
    selector: "app-container",
    template: `<ejs-diagram id="diagram" width="100%" height="580px">
        <e-connectors>
            <e-connector id='connector' type='Straight' [sourcePoint]='sourcePoint' [targetPoint]='targetPoint' [constraints]='connectorConstraints'>
            </e-connector>
        </e-connectors>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public connectorConstraints: ConnectorConstraints;
    public sourcePoint: PointModel;
    public targetPoint:PointModel;
    ngOnInit(): void {
        this.sourcePoint: { x: 100, y: 100 },
        this.targetPoint: { x: 200, y: 200 },
        this.connectorConstraints = ConnectorConstraints.Default & ~ConnectorConstraints.Select;
    }
}
```

For more information about connector constraints, refer to [`ConnectorConstraints`](../api/diagram/connectorConstraints).

## Port constraints

You can enable or disable certain behaviors of port. They are as follows:

* Connect
* ConnectOnDrag

The following code illustrates how to disable creating connections with a port.

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { PointPortModel, PortConstraints } from "@syncfusion/ej2-angular-diagrams";

@Component({
    selector: "app-container",
    template: `<ejs-diagram id="diagram" width="100%" height="580px">
        <e-nodes>
            <e-node id='node1' [height]=60 [width]=100 [offsetX]=300 [offsetY]=80 [ports]='port1'>
            </e-node>
        </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public port1: PointPortModel[];
    ngOnInit(): void {
        this.port1 = [{
            id: 'port1',
            shape: 'Circle',
            offset: { x: 0, y: 0.5 },
            text: 'In - 1',
            constraints: PortConstraints.None
        }];
    }
}
```

For more information about port constraints, refer to [`PortConstraints`](../api/diagram/portConstraints).

## Annotation constraints

You can enable or disable read-only mode for the annotations by using the annotation constraints.

The following code illustrates how to enable read-only mode for the annotations.

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { AnnotationConstraints } from "@syncfusion/ej2-angular-diagrams";

@Component({
    selector: "app-container",
    template: `<ejs-diagram id="diagram" width="100%" height="580px">
        <e-nodes>
            <e-node id='node1' [height]=60 [width]=100 [offsetX]=300 [offsetY]=80>
            <e-node-annotations>
                <e-node-annotation content='Start' [constraints]='annotationConstraints'></e-node-annotation>
            </e-node-annotations>
        </e-node>
        </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public annotationConstraints: AnnotationConstraints;
    ngOnInit(): void {
        this.annotationConstraints = AnnotationConstraints.ReadOnly;
    }
}
```

For more details about annotation constraints, refer to [`AnnotationConstraints`](../api/diagram/annotationConstraints#AnnotationConstraints).

## Selector constraints

Selector visually represents the selected elements with certain editable thumbs. The visibility of the thumbs can be controlled with selector constraints. The part of selector is categorized as follows:

* Resizer
* Rotator
* User handles

The following code illustrates how to hide rotator.

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { SelectorModel, SelectorConstraints } from '@syncfusion/ej2-diagrams';
@Component({
  selector: "app-container",
  // specifies the template string for the diagram component
  template: `<ejs-diagram id="diagram" width="100%" height="580px" [selectedItems]='selectedItems'></ejs-diagram>`
})
export class AppComponent {
    @ViewChild("diagram")
    public selectedItems: SelectorModel;
    ngOnInit(): void {
        this.selectedItems = { constraints: SelectorConstraints.All & ~SelectorConstraints.Rotate };
    }
}
```

For more information about selector constraints, refer to [`SelectorConstraints`](../api/diagram/selectorConstraints).

## Snap constraints

Snap constraints control the visibility of gridlines and enable/disable snapping. Snap constraints allow to set the following behaviors.

* Show only horizontal or vertical gridlines.
* Show both horizontal and vertical gridlines.
* Snap to either horizontal or vertical gridlines.
* Snap to both horizontal and vertical gridlines.

The following code illustrates how to show only horizontal gridlines.

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { SnapSettingsModel, SnapConstraints } from '@syncfusion/ej2-diagrams';
@Component({
  selector: "app-container",
  // specifies the template string for the diagram component
  template: `<ejs-diagram id="diagram" width="100%" height="580px" [snapSettings]='snapSettings'></ejs-diagram>`
})
export class AppComponent {
    @ViewChild("diagram")
    public snapSettings: SnapSettingsModel;
    ngOnInit(): void {
        this.snapSettings: {
            constraints: SnapConstraints.ShowHorizontalLines
        };
    }
}
```

For more information about snap constraints, refer to [`SnapConstraints`](../api/diagram/snapConstraints).

## Boundary constraints

Boundary constraints defines a boundary for the diagram inside which the interaction should be done. Boundary constraints allow to set the following behaviors.

* Infinite boundary
* Diagram sized boundary
* Page sized boundary

The following code illustrates how to limit the interaction done inside a diagram within a page.

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { PageSettingsModel, BoundaryConstraints } from '@syncfusion/ej2-diagrams';
@Component({
  selector: "app-container",
  template: `<ejs-diagram id="diagram" width="100%" height="580px" [pageSettings]='pageSettings'></ejs-diagram>`
})
export class AppComponent {
    @ViewChild("diagram")
    public pageSettings: PageSettingsModel;
    ngOnInit(): void {
        this.pageSettings: {
            boundaryConstraints: 'Page'
        };
    }
}
```

For more information about selector constraints, refer to [`BoundaryConstraints`](../api/diagram/boundaryConstraints).

## Inherit behaviors

Some of the behaviors can be defined through both the specific object (node/connector) and diagram. When the behaviors are contradictorily defined through both, the actual behavior is set through inherit options.

The following code example illustrates how to inherit the line bridging behavior from the diagram model.

```typescript

import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { DiagramConstraints, ConnectorBridging, ConnectorConstraints, PointModel } from "@syncfusion/ej2-angular-diagrams";
Diagram.Inject(ConnectorBridging);

@Component({
    selector: "app-container",
    template: `<ejs-diagram id="diagram" width="100%" height="580px" [constraints]='diagramConstraints'>
        <e-connectors>
            <e-connector id='connector' type='Straight' [sourcePoint]='sourcePoint' [targetPoint]='targetPoint' [constraints]='connectorConstraints'>
            </e-connector>
        </e-connectors>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagramConstraints: DiagramConstraints;
    public connectorConstraints: ConnectorConstraints;
    public sourcePoint: PointModel;
    public targetPoint:PointModel;
    ngOnInit(): void {
        this.diagramConstraints = DiagramConstraints.Default | DiagramConstraints.Bridging;
        this.sourcePoint: { x: 100, y: 100 },
        this.targetPoint: { x: 200, y: 200 },
        this.connectorConstraints = ConnectorConstraints.Default & ConnectorConstraints.InheritBridging;
    }
}
```

## Bitwise operations

Bitwise operations are used to manipulate the flagged enumerations [enum]. In this section, Bitwise operations are illustrated by using node constraints. The same is applicable while working with node constraints, connector constraints, or port constraints.

## Add operation

You can add or enable multiple values at a time by using Bitwise ‘|’ (OR) operator.

```typescript
node.constraints = NodeConstraints.Select | NodeConstraints.Rotate;
```

In the previous example, you can do both the selection and rotation operation.

## Remove Operation

You can remove or disable values by using Bitwise ‘&~’ (XOR) operator.

```typescript
node.constraints = node.constraints & ~(NodeConstraints.Rotate);
```

In the previous example, rotation is disabled but other constraints are enabled.

## Check operation

You can check any value by using Bitwise ‘&’ (AND) operator.

```typescript
if ((node.constraints & (NodeConstraints.Rotate)) == (NodeConstraints.Rotate));
```

In the previous example, check whether the rotate constraints are enabled in a node. When node constraints have rotate constraints, the expression returns a rotate constraint.