---
title: "Layers"
component: "Diagram"
description: "Layer is used to organize the shapes on the diagram control"
---

# Layers

**Layer** is used to organize related shapes on a diagram control. A layer is a named category of shapes. By assigning shapes to different layers, you can selectively view, remove, and lock different categories of shapes.

In diagram, [Layers](../api/diagram) provide a way to change the properties of all shapes that have been assigned to that layer. The following properties can be set.

* Visible
* Lock
* Objects
* AddInfo

## Visible

The layer's [visible](../api/diagram/layer#visible-boolean) property is used to control the visibility of the elements assigned to the layer.

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, PointModel, LayerModel } from '@syncfusion/ej2-angular-diagrams';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [layers]="layers">
    <e-connectors>
            <e-connector id='connector' type='Straight' [sourcePoint]='sourcePoint' [targetPoint]='targetPoint'>
            </e-connector>
    </e-connectors>
    <e-nodes>
            <e-node id='node1' [offsetX]=150 [offsetY]=150></e-node>
    </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public sourcePoint: PointModel;
    public targetPoint: PointModel;
    public pageSettings: PageSettingsModel;
    ngOnInit(): void {
        this.sourcePoint = { x: 100, y: 100 };
        this.targetPoint = { x: 200, y: 200 };
        this.layers = {
            id: 'layer1',
            visible: true,
            objects: ['node1', 'connector']
        }
    }
}
```

## Lock

The layer's [lock](../api/diagram/layer#lock-boolean) property is used to prevent or allow changes to the elements dimension and position.

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, PointModel, LayerModel } from '@syncfusion/ej2-angular-diagrams';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [layers]="layers">
    <e-connectors>
            <e-connector id='connector' type='Straight' [sourcePoint]='sourcePoint' [targetPoint]='targetPoint'>
            </e-connector>
    </e-connectors>
    <e-nodes>
            <e-node id='node1' [offsetX]=150 [offsetY]=150></e-node>
            <e-node id='node2' [offsetX]=350 [offsetY]=350></e-node>
    </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public sourcePoint: PointModel;
    public targetPoint: PointModel;
    public layers: LayerModel;
    ngOnInit(): void {
        this.sourcePoint = { x: 100, y: 100 };
        this.targetPoint = { x: 200, y: 200 };
        this.layers = [{
            id: 'layer1',
            visible: true,
            objects: ['node1', 'connector'],
            lock: true
        },
        {
            id: 'layer2',
            visible: true,
            objects: ['node2'],
            lock: false
        }];
    }
}
```

## Objects

The layer's [objects](../api/diagram/layer#objects-string[]) property defines the diagram elements to the layer.

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, PointModel, LayerModel } from '@syncfusion/ej2-angular-diagrams';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [layers]="layers">
    <e-connectors>
            <e-connector id='connector' type='Straight' [sourcePoint]='sourcePoint' [targetPoint]='targetPoint'>
            </e-connector>
    </e-connectors>
    <e-nodes>
            <e-node id='node1' [offsetX]=150 [offsetY]=150></e-node>
            <e-node id='node2' [offsetX]=350 [offsetY]=350></e-node>
    </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public sourcePoint: PointModel;
    public targetPoint: PointModel;
    public layers: LayerModel;
    ngOnInit(): void {
        this.sourcePoint = { x: 100, y: 100 };
        this.targetPoint = { x: 200, y: 200 };
        this.layers = [{
            id: 'layer1',
            visible: true,
            objects: ['node1', 'connector'],
            lock: true
        },
        {
            id: 'layer2',
            visible: true,
            objects: ['node2'],
            lock: false
        }];
    }
}
```

## AddInfo

The [`addInfo`](../api/diagram/layer#addinfo-Object) property of layers allow you to maintain additional information to the layers.

The following code illustrates how to add additional information to the layers.

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, PointModel, LayerModel } from '@syncfusion/ej2-angular-diagrams';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [layers]="layers">
    <e-connectors>
            <e-connector id='connector' type='Straight' [sourcePoint]='sourcePoint' [targetPoint]='targetPoint'>
            </e-connector>
    </e-connectors>
    <e-nodes>
            <e-node id='node1' [offsetX]=150 [offsetY]=150></e-node>
            <e-node id='node2' [offsetX]=350 [offsetY]=350></e-node>
    </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public sourcePoint: PointModel;
    public targetPoint: PointModel;
    public layers: LayerModel;
    public addInfo: Object = { Description: 'Layer1' };
    ngOnInit(): void {
        this.sourcePoint = { x: 100, y: 100 };
        this.targetPoint = { x: 200, y: 200 };
        this.layers = [{
            id: 'layer1',
            visible: true,
            objects: ['node1', 'connector'],
            lock: true,
            addInfo: this.addInfo

        },
        {
            id: 'layer2',
            visible: true,
            objects: ['node2'],
            lock: false
        }];
    }
}
```

### Add layer at runtime

Layers can be added at runtime by using the [`addLayer`](../api/diagram#addLayer) public method.

The layer's [`ID`](../api/diagram/layer#id-string) property defines the ID of the layer, and its further used to find the layer at runtime and do any customization.

The following code illustrates how to add a layer.

```typescript
// add the layers to the existing diagram layer collection
this.diagram.addLayer({
    id: 'newlayer',
    objects: [],
    visible: true,
    lock: false,
    zIndex: -1
}, [{
    type: 'Straight',
    sourcePoint: {
        x: 100,
        y: 300
    },
    targetPoint: {
        x: 200,
        y: 400
    }
}]);
```

### Remove layer at runtime

Layers can be removed at runtime by using the [`removeLayer`](../api/diagram#removeLayer) public method.

The following code illustrates how to remove a layer.

```typescript
// remove the diagram layers
this.diagram.removeLayer([diagram.model.layers[i]]);

```

### moveObjects

Objects of the layers can be moved by using the [`moveObjects`](../api/diagram#moveObjects) public method.

The following code illustrates how to move objects from one layer to another layer from the diagram.

```typescript
// move the objects of diagram layers
this.diagram.moveObjects(['connector1'], 'layer2');

```

### bringLayerForward

Layers can be moved forward at runtime by using the [`bringLayerForward`](../api/diagram#bringLayerForward) public method.

The following code illustrates how to bring forward to layer.

```typescript
// move the layer forward
this.diagram.bringLayerForward('layer1');

```

### sendLayerBackward

Layers can be moved backward at runtime by using the [`sendLayerBackward`](../api/diagram#sendLayerBackward) public method.

The following code illustrates how to send backward to layer.

```typescript
// move the layer backward
this.diagram.sendLayerBackward('layer1');

```

### cloneLayer

Layers can be cloned with its object by using the [`cloneLayer`](../api/diagram#cloneLayer) public method.

The following code illustrates how to bring forward to layer.

```typescript
// clone a layer with its object
this.diagram.cloneLayer('layer2');

```

### getActiveLayer

To get the active layers back in diagram, use the [`getActiveLayer`](../api/diagram#getActiveLayer) public method.

The following code illustrates how to bring forward to layer.

```typescript
// gets the active layer back
this.diagram.getActiveLayer();

```

### setActiveLayer

Set the active layer by using the [`setActiveLayer`](../api/diagram#setActiveLayer) public method.

The following code illustrates how to bring forward to layer.

```typescript

// set the active layer
//@param layerName defines the name of the layer which is to be active layer
this.diagram.setActiveLayer('layer2');

```