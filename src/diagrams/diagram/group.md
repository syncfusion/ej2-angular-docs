---
title: "Group"
component: "Diagram"
description: "Diagram supports Grouping feature to group two or more nodes."
---

# Group

Group is used to cluster multiple nodes and connectors into a single element. It acts like a container for its children (nodes, groups, and connectors). Every change made to the group also affects the children. Child elements can be edited individually.

## Create group

## Add group when initializing diagram

A group can be added to the diagram model through [`nodes`](../api/diagram#nodes-NodeModel) collection. To define an object as group, add the child objects to the [`children`](../api/diagram/node#children-string) collection of the group. The following code illustrates how to create a group node.

* While creating group, its child node need to be declared before the group declaration.

* Add a node to the existing group child by using the `diagram.group` method.

* The group’s `diagram.unGroup` method is used to define whether the group can be ungrouped or not.

* A group can be added into a child of another group.

{% tab template="diagram/groups/group", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, IconShapeModel } from '@syncfusion/ej2-angular-diagrams';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults] ='getNodeDefaults' (created)='created($event)'>
        <e-nodes>
            <e-node id='node1' [offsetX]=100 [offsetY]=100>
            </e-node>
            <e-node id='node2' [offsetX]=200 [offsetY]=200>
            </e-node>
            <e-node id='node3' [offsetX]=400 [offsetY]=300 >
            </e-node>
            <e-node id='group' [children]='children'>
            </e-node>
        </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public getNodeDefaults(node: NodeModel): NodeModel {
        node.height = 100;
        node.width = 100;
        node.style.fill = "#6BA5D7";
        node.style.strokeColor = "White";
        return node;
    }
    public children: string[];
    ngOnInit(): void {
        this.children = ['node1', 'node2']
    }
    public created(args: Object): void {
        this.diagram.selectAll();
        // Adding the third node into the existing group
        this.diagram.group();
    }
}
```

{% endtab %}

The following code illustrates how a ungroup  at runtime.

{% tab template="diagram/groups/ungroup", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, IconShapeModel } from '@syncfusion/ej2-angular-diagrams';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults] ='getNodeDefaults' (created)='created($event)'>
        <e-nodes>
            <e-node id='node1' [offsetX]=100 [offsetY]=100>
            </e-node>
            <e-node id='node2' [offsetX]=200 [offsetY]=200>
            </e-node>
            <e-node id='node3' [offsetX]=400 [offsetY]=300 >
            </e-node>
            <e-node id='group' [children]='children'>
            </e-node>
        </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public getNodeDefaults(node: NodeModel): NodeModel {
        node.height = 100;
        node.width = 100;
        node.style.fill = "#6BA5D7";
        node.style.strokeColor = "White";
        return node;
    }
    public children: string[];
    ngOnInit(): void {
        this.children = ['node1', 'node2']
    }
    public created(args: Object): void {
        this.diagram.selectAll();
        // Ungroup the selected group into nodes
        this.diagram.unGroup();
    }
}
```

{% endtab %}

Connectors can be added to a group. The following code illustrates how to add connectors into a group.

{% tab template="diagram/groups/groupaddconnector", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, ViewChild, } from '@angular/core';
import {
    DiagramComponent, NodeModel, ConnectorModel,
} from '@syncfusion/ej2-angular-diagrams';

@Component({
    selector: 'app-container',
    template: `<ejs-diagram #diagram id="diagram" width="1000px" height="700px" [nodes]='nodes' [connectors]="connectors">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
    @ViewChild('diagram')
    public diagram: DiagramComponent;
    public connectors: ConnectorModel[] = [{
      id: 'connector1', type: 'Orthogonal', sourceID: 'node1', targetID: 'node2'
    },
   ];
    public nodes: NodeModel[] = [{
     id: 'node1', height: 100, width: 100, offsetX: 100, offsetY: 100, annotations: [{ content: 'Node1'}]
   },
   {
     id: 'node2', height: 100, width: 100, offsetX: 300, offsetY: 100, annotations: [{ content: 'Node2'}]
   },
   {
     id: 'group', children: ['node1', 'node2', 'connector1',], style: { strokeWidth: 0}
   }];
}
```

{% endtab %}

## Add group at runtime

A group node can be added at runtime by using the client-side method `diagram.add`.

The following code illustrates how a group node is added at runtime.

{% tab template="diagram/groups/groupadd", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, IconShapeModel } from '@syncfusion/ej2-angular-diagrams';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults] ='getNodeDefaults' (created)='created($event)'>
        <e-nodes>
            <e-node id='node1' [offsetX]=100 [offsetY]=100>
            </e-node>
            <e-node id='node2' [offsetX]=200 [offsetY]=200>
            </e-node>
        </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public getNodeDefaults(node: NodeModel): NodeModel {
        node.height = 100;
        node.width = 100;
        node.style.fill = "#6BA5D7";
        node.style.strokeColor = "White";
        return node;
    }
    public group: NodeModel[] = [{
            id: 'group2',
            children: ['node1', 'node2']
        }]
    public created(args: Object): void {
        // Add the group into the diagram
        this.diagram.add(this.group);
    }
}
```

{% endtab %}

## Container

Containers are used to automatically measure and arrange the size and position of the child elements in a predefined manner.
There are two types of containers available.

## Canvas

* The canvas panel supports absolute positioning and provides the least layout functionality to its contained diagram elements.

* Canvas allows you to position its contained elements by using the margin and alignment properties.

* Rendering alone possible in canvas container.

* It allows elements to be either vertically or horizontally aligned.

* Child can be defined with the collection [`canvas.children`](../api/diagram/canvas#children-DiagramElement) property.

* Basic element can be defined with the collection of [`basicElements`](../api/diagram#basicElements-DiagramElement)

The following code illustrates how to add canvas panel

## Stack

* Stack panel is used to arrange its children in a single line or stack order, either vertically or horizontally.

* It controls spacing by setting margin properties of child and padding properties of group. By default, a stack panel’s [`orientation`](../api/diagram/stackPanel#orientation-Orientation) is vertical.

The following code illustrates how to add a stack panel.

{% tab template="diagram/groups/stack", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, TextElement, StackPanel, PointModel, VerticalAlignment } from '@syncfusion/ej2-angular-diagrams';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults] ='getNodeDefaults'>
        <e-nodes>
            <e-node id='node1' [offsetX]=100 [offsetY]=100>
                <e-node-annotations>
                    <e-node-annotation content="Custom Template" [offset]='offset' [verticalAlignment]='verticalAlignment'>
                </e-node-annotation>
        </e-node-annotations>
            </e-node>
        </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public offset: PointModel
    public verticalAlignment: VerticalAlignment
    public getTextElement(text: string): TextElement {
        let textElement: TextElement = new TextElement();
        textElement.width = 50;
        textElement.height = 20;
        textElement.content = text;
        return textElement;
    };

    public addRows(column: StackPanel) {
        column.children.push(this.getTextElement('Row1'));
        column.children.push(this.getTextElement('Row2'));
        column.children.push(this.getTextElement('Row3'));
        column.children.push(this.getTextElement('Row4'));
    };
    public getNodeDefaults(node: NodeModel): NodeModel {
        node.height = 100;
        node.width = 100;
        node.style.fill = '#6BA5D7';
        node.style.strokeColor = 'white';
        return node;
    }
    ngOnInit(): void {
        this.verticalAlignment = 'Top';
        this.offset = {y: 1};
        this.diagram.setNodeTemplate = (obj: NodeModel, diagram: Diagram): StackPanel => {
            if (obj.id.indexOf('node1') !== -1) {
                // It will be replaced with grid panel
                let table: StackPanel = new StackPanel();
                table.orientation = 'Horizontal';
                let column1: StackPanel = new StackPanel();
                column1.children = [];
                column1.children.push(this.getTextElement('Column1'));
                this.addRows(column1);
                let column2: StackPanel = new StackPanel();
                column2.children = [];
                column2.children.push(this.getTextElement('Column2'));
                this.addRows(column2);
                table.children = [column1, column2];
                return table;
            }
            return null
        }
    }
}
```

{% endtab %}

## Difference between a basic group and containers

| Group | Container |
| -------- | -------- |
| It arranges the child elements based on the child elements position and size properties. | Each container has a predefined behavior to measure and arrange its child elements. Canvas and stack containers are supported in the diagram. |
| The Padding, Min, and Max Size properties are not applicable for basic group. | It is applicable for container. |
| The Children’s margin and alignment properties are not applicable for basic group. |  It is applicable for container. |

## Interaction

You can edit the group and its children at runtime. For more information about how to interact with a group, refer to `Edit Groups`.

## See Also

* [How to add annotations to the node](./labels)
* [How to add ports to the node](./ports)
* [How to enable/disable the behavior of the node](./constraints)
* [How to add nodes to the symbol palette](./symbol-palette)
* [How to create diagram nodes using drawing tools](./tools)
* [How to perform the interaction on the group](./interaction#selection)