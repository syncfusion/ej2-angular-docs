---
title: "Automatic Layout"
component: "Diagram"
description: "Diagram automatic layout allows you to arrange the nodes in the diagram area."
---

# Automatic Layout

Diagram provides support to auto-arrange the nodes in the diagram area that is referred as `Layout`. It includes the following layout modes:

## Layout modes

* Hierarchical layout
* Organization chart
* Radial tree
* Symmetric layout
* Mind Map layout
* Complex hierarchical tree layout

### Hierarchical layout

The hierarchical tree layout arranges nodes in a tree-like structure, where the nodes in the hierarchical layout may have multiple parents. There is no need to specify the layout root. To arrange the nodes in a hierarchical structure, specify the layout [`type`](../api/diagram/layout) as hierarchical tree.

>Note: If you want to use hierarchical tree layout in diagram, you need to inject HierarchicalTree in the diagram.

The following example shows how to arrange the nodes in a hierarchical structure.

{% tab template="diagram/automaticlayout/hierarchicallayout", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            Name: "Steve-Ceo"
        },
        {
            Name: "Kevin-Manager",
            ReportingPerson: "Steve-Ceo"
        },
        {
            Name: "Peter-Manager",
            ReportingPerson: "Steve-Ceo"
        },
        {
            Name: "John- Manager",
            ReportingPerson: "Peter-Manager"
        },
        {
            Name: "Mary-CSE ",
            ReportingPerson: "Peter-Manager"
        },
        {
            Name: "Jim-CSE ",
            ReportingPerson: "Kevin-Manager"
        },
        {
            Name: "Martin-CSE",
            ReportingPerson: "Kevin-Manager"
        }
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.shape = {
            type: 'Text',
            content: (obj.data as {Name: 'string'}).Name
        };
        obj.style = {
            fill: 'None',
            strokeColor: 'none',
            strokeWidth: 2,
            bold: true,
            color: 'white'
        };
        obj.borderColor = 'white';
        obj.width = 100;
        obj.height = 40;
        obj.backgroundColor = '#6BA5D7';
        obj.borderWidth = 1;
        (obj.shape as TextModel).margin = {
            left: 5,
            right: 5,
            top: 5,
            bottom: 5
        };
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.type = 'Orthogonal';
        return connector;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
        //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            //Sets layout type
            type: 'HierarchicalTree'
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Name',
            parentId: 'ReportingPerson',
            dataSource: this.items
        }
    }
}
```

{% endtab %}

### Radial tree layout

The radial tree layout arranges nodes on a virtual concentric circle around a root node. Sub-trees formed by the branching of child nodes are located radially around the child nodes. This arrangement result in an ever-expanding concentric arrangement with radial proximity to the root node indicating the node level in the hierarchy. The layout [`root`](../api/diagram/layout) property can be used to define the root node of the layout. When no root node is set, the algorithm automatically considers one of the diagram nodes as the root node.

To arrange nodes in a radial tree structure, set the [`type`](../api/diagram/layout) of the layout as `RadialTree`.

>Note: If you want to use radial tree layout in diagram, you need to inject DataBinding and RadialTree in the diagram.

The following code illustrates how to arrange the nodes in a radial tree structure.

{% tab template="diagram/automaticlayout/radiallayout", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            "Id": 1,
            "Name": "Ana Trujillo",
            "Designation": "Project Manager",
            "RatingColor": "#68C2DE"
        },
        {
            "Id": 2,
            "Name": "Lino Rodri",
            "Designation": "Project Manager",
            "RatingColor": "#68C2DE",
            "ReportingPerson": 1
        },
        {
            "Id": 3,
            "Name": "Philip Cramer",
            "Designation": "Project Manager",
            "RatingColor": "#68C2DE",
            "ReportingPerson": 1
        },
        {
            "Id": 4,
            "Name": "Pedro Afonso",
            "Designation": "Project Manager",
            "RatingColor": "#68C2DE",
            "ReportingPerson": 1
        },
        {
            "Id": 5,
            "Name": "Anto Moreno",
            "Designation": "Project Lead",
            "RatingColor": "#93B85A",
            "ReportingPerson": 1
        },
        {
            "Id": 6,
            "Name": "Elizabeth Roel",
            "Designation": "Project Lead",
            "RatingColor": "#93B85A",
            "ReportingPerson": 1
        },
        {
            "Id": 7,
            "Name": "Aria Cruz",
            "Designation": "Project Lead",
            "RatingColor": "#93B85A",
            "ReportingPerson": 1
        },
        {
            "Id": 8,
            "Name": "Eduardo Roel",
            "Designation": "Project Lead",
            "RatingColor": "#93B85A",
            "ReportingPerson": 1
        },
        {
            "Id": 9,
            "Name": "Howard Snyd",
            "Designation": "Project Lead",
            "RatingColor": "#68C2DE",
            "ReportingPerson": 1
        },
        {
            "Id": 10,
            "Name": "Daniel Tonini",
            "Designation": "Project Lead",
            "RatingColor": "#93B85A",
            "ReportingPerson": 1
        },
        {
            "Id": 11,
            "Name": "Nardo Batista",
            "Designation": "Project Lead",
            "RatingColor": "#68C2DE",
            "ReportingPerson": 1
        }
    ];
    public getNodeDefaults(obj: NodeModel): NodeModel {
        obj.height = 15;
        obj.width = 15;
        obj.borderWidth = 1;
        obj.style = {
            fill: '#6BA5D7',
            strokeWidth: 2,
            strokeColor: '#6BA5D7'
        };
        return obj;
    }
    //Sets the default properties for and connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.targetDecorator.shape = 'None';
        connector.type = 'Straight';
        return connector;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
        //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            //set the type as Radial Tree
            type: 'RadialTree',
            root: 'parent'
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Id',
            parentId: 'ReportingPerson',
            dataSource: this.items
        }
    }
}
```

{% endtab %}

### Organizational Chart

An organizational chart is a diagram that displays the structure of an organization and relationships. To create an organizational chart, the [`type`](../api/diagram/layout) of layout should be set as an `OrganizationalChart`.
The following code example illustrates how to create an organizational chart.

{% tab template="diagram/automaticlayout/organizationalchart", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            Id: "parent",
            Role: "Project Management"
        },
        {
            Id: 1,
            Role: "R&D Team",
            Team: "parent"
        },
        {
            Id: 3,
            Role: "Philosophy",
            Team: "1"
        },
        {
            Id: 4,
            Role: "Organization",
            Team: "1"
        },
        {
            Id: 5,
            Role: "Technology",
            Team: "1"
        },
        {
            Id: 7,
            Role: "Funding",
            Team: "1"
        },
        {
            Id: 8,
            Role: "Resource Allocation",
            Team: "1"
        },
        {
            Id: 9,
            Role: "Targeting",
            Team: "1"
        },
        {
            Id: 11,
            Role: "Evaluation",
            Team: "1"
        },
        {
            Id: 156,
            Role: "HR Team",
            Team: "parent"
        },
        {
            Id: 13,
            Role: "Recruitment",
            Team: "156"
        },
        {
            Id: 113,
            Role: "Training",
            Team: "12"
        },
        {
            Id: 112,
            Role: "Employee Relation",
            Team: "156"
        },
        {
            Id: 14,
            Role: "Record Keeping",
            Team: "12"
        },
        {
            Id: 15,
            Role: "Compensations & Benefits",
            Team: "12"
        },
        {
            Id: 16,
            Role: "Compliances",
            Team: "12"
        },
        {
            Id: 17,
            Role: "Production & Sales Team",
            Team: "parent"
        },
        {
            Id: 119,
            Role: "Design",
            Team: "17"
        },
        {
            Id: 19,
            Role: "Operation",
            Team: "17"
        },
        {
            Id: 20,
            Role: "Support",
            Team: "17"
        },
        {
            Id: 21,
            Role: "Quality Assurance",
            Team: "17"
        },
        {
            Id: 23,
            Role: "Customer Interaction",
            Team: "17"
        },
        {
            Id: 24,
            Role: "Support and Maintenance",
            Team: "17"
        },
        {
            Id: 25,
            Role: "Task Coordination",
            Team: "17"
        }
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.shape = {
            type: 'Text',
            content: (obj.data as {
                Role: 'string'
            }).Role
        };
        obj.style = {
            fill: 'None',
            strokeColor: 'none',
            strokeWidth: 2,
            bold: true,
            color: 'white'
        };
        obj.borderColor = 'white';
        obj.backgroundColor = '#6BA5D7';
        obj.borderWidth = 1;
        obj.width = 75;
        obj.height = 40;
        (obj.shape as TextModel).margin = {
            left: 5,
            right: 5,
            top: 5,
            bottom: 5
        };
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.type = 'Orthogonal';
        return connector;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(5));
        //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            //set the type as Organizational Chart
            type: 'OrganizationalChart'
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Id',
            parentId: 'Team',
            dataSource: this.items
        }
    }
}
```

{% endtab %}

Organizational chart layout starts parsing from root and iterate through all its child elements. The `getLayoutInfo` method provides necessary information of a node’s children and the way to arrange (direction, orientation, offsets, etc.) them. The arrangements can be customized by overriding this function as explained.

**GetLayoutInfo**
Set chart orientations, chart types, and offset to be left between parent and child nodes by overriding the method, `diagram.layout.getLayoutInfo`. The [`getLayoutInfo`](../api/diagram/layout) method is called to configure every subtree of the organizational chart. It takes the following arguments.

    * node: Parent node to that options are to be customized.
    * options: Object to set the customizable properties.

{% tab template="diagram/automaticlayout/getlayoutinfo", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            Id: 1,
            Role: "General Manager"
        },
        {
            Id: 2,
            Role: "Assistant Manager",
            Team: 1
        },
        {
            Id: 3,
            Role: "Human Resource Manager",
            Team: 1
        },
        {
            Id: 4,
            Role: "Design Manager",
            Team: 1
        },
        {
            Id: 5,
            Role: "Operation Manager",
            Team: 1
        },
        {
            Id: 6,
            Role: "Marketing Manager",
            Team: 1
        }
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.width = 150;
        obj.height = 50;
        obj.style.fill = '#6BA5D7';
        obj.annotations = [{
            content: obj.data['Role'],
            style: {
                color: 'white'
            }
        }];
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.targetDecorator.shape = 'None';
        connector.targetDecorator.shape = 'None';
        connector.type = 'Orthogonal';
        return connector;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
        //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            //Sets layout type
            type: 'OrganizationalChart',
            getLayoutInfo: (node: Node, options: TreeInfo) => {
                if (!options.hasSubTree) {
                    options.type = 'Center';
                    options.orientation = 'Horizontal';
                }
            }
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Id',
            parentId: 'Team',
            dataSource: this.items
        }
    }
}
```

{% endtab %}

The following table illustrates the properties that “options” argument takes.

| Property | Description | Default Value |
| -------- | ----------- | ------------- |
|options.assistants|By default, the collection is empty. When any of the child nodes have to be set as **Assistant**, you can remove from children collection and have to insert into assistants collection.|Empty array|
|options.orientation|Gets or sets the organizational chart orientation.|SubTreeOrientation.Vertical|
|options.type|Gets or sets the chart organizational chart type.|For horizontal chart orientation:SubTreeAlignments.Center and for vertical chart orientation:SubTreeAlignments.Alternate|
|options.offset|Offset is the horizontal space to be left between parent and child nodes.|20 pixels applicable only for vertical chart orientations.|
|options.hasSubTree|Gets whether the node contains subtrees.|Boolean|
|options.level|Gets the depth of the node from layout root.|Number|
|options.enableRouting|By default, connections are routed based on the chart type and orientations. This property gets or sets whether default routing is to be enabled or disabled.|true|
|options.rows|Sets the number of rows on which the child nodes will be arranged. Applicable only for balanced type horizontal tree.|Number|

The following table illustrates the different chart orientations and chart types.

|Orientation|Type|Description|Example|
| -------- | ----------- | ------------- |------|
|Horizontal|Left|Arranges the child nodes horizontally at the left side of the parent.|![Horizontal Left](images/hleft.jpg)|
||Right|Arranges the child nodes horizontally at the right side of the parent.|![Horizontal Right](images/hright.jpg)|
||Center|Arranges the children like standard tree layout orientation.|![Horizontal Center](images/hcenter.jpg)|
||Balanced|Arranges the leaf level child nodes in multiple rows.|![Horizontal Balanced](images/hbalanced.jpg)|
|Vertical|Left|Arranges the children vertically at the left side of the parent.|![Vertical Left](images/vleft.jpg)|
||Right|Arranges the children vertically at the right side of the parent.|![Vertical Right](images/vright.jpg)|
||Alternate|Arranges the children vertically at both left and right sides of the parent.|![Vertical Alternate](images/vAlternate.jpg)|

The following code example illustrates how to set the vertical right arrangement to the leaf level trees.

{% tab template="diagram/automaticlayout/illustration", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            Id: "parent",
            Role: "Board"
        },
        {
            Id: "1",
            Role: "General Manager",
            Manager: "parent"
        },
        {
            Id: "2",
            Role: "Human Resource Manager",
            Manager: "1"
        },
        {
            Id: "3",
            Role: "Trainers",
            Manager: "2"
        },
        {
            Id: "4",
            Role: "Recruiting Team",
            Manager: "2"
        },
        {
            Id: "6",
            Role: "Design Manager",
            Manager: "1"
        },
        {
            Id: "7",
            Role: "Design Supervisor",
            Manager: "6"
        },
        {
            Id: "8",
            Role: "Development Supervisor",
            Manager: "6"
        },
        {
            Id: "9",
            Role: "Drafting Supervisor",
            Manager: "6"
        },
        {
            Id: "10",
            Role: "Marketing Manager",
            Manager: "1"
        },
        {
            Id: "11",
            Role: "Oversea sales Manager",
            Manager: "10"
        },
        {
            Id: "12",
            Role: "Petroleum Manager",
            Manager: "10"
        },
        {
            Id: "13",
            Role: "Service Dept. Manager",
            Manager: "10"
        },
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.width = 150;
        obj.height = 50;
        obj.borderColor = 'white';
        obj.style.fill = '#6BA5D7';
        obj.borderWidth = 1;
        obj.annotations = [{
            content: obj.data['Role'],
            style: {
                color: 'white'
            }
        }];
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill = '#6BA5D7';
        connector.targetDecorator.style.strokeColor = '#6BA5D7';
        connector.targetDecorator.shape = 'None';
        connector.type = 'Orthogonal';
        return connector;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
        //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
        //Sets layout type
        type: 'OrganizationalChart',
        //Defines getLayoutInfo
        getLayoutInfo: (node: Node, options: TreeInfo) => {
            if (node.data['Role'] === 'General Manager') {
                options.assistants.push(options.children[0]);
                options.children.splice(0, 1);
            }
            if (!options.hasSubTree) {
                options.type = 'Right';
                options.orientation = 'Vertical';
            }
        }
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Id',
            parentId: 'Manager',
            dataSource: this.items
        }
    }
}
```

{% endtab %}

## Assistant

Assistants are child item that have a different relationship with the parent node. They are laid out in a dedicated part of the tree. A node can be specified as an assistant of its parent by adding it to the `assistants` property of the argument “options”.

The following code example illustrates how to add assistants to layout.

{% tab template="diagram/automaticlayout/assistant", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            Id: 1,
            Role: "General Manager"
        },
        {
            Id: 2,
            Role: "Assistant Manager",
            Team: 1
        },
        {
            Id: 3,
            Role: "Human Resource Manager",
            Team: 1
        },
        {
            Id: 4,
            Role: "Design Manager",
            Team: 1
        },
        {
            Id: 5,
            Role: "Operation Manager",
            Team: 1
        },
        {
            Id: 6,
            Role: "Marketing Manager",
            Team: 1
        }
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.width = 150;
        obj.height = 50;
        obj.borderColor = 'white';
        obj.style.fill = '#6BA5D7';
        obj.borderWidth = 1;
        obj.annotations = [{
            content: obj.data['Role'],
            style: {
                color: 'white'
            }
        }];
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.targetDecorator.shape = 'None';
        connector.type = 'Orthogonal';
        return connector;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
        //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            //Sets layout type
            type: 'OrganizationalChart',
            // define the getLayoutInfo
            getLayoutInfo: (node: Node, options: TreeInfo) => {
                if (node.data['Role'] === 'General Manager') {
                    options.assistants.push(options.children[0]);
                    options.children.splice(0, 1);
                }
                if (!options.hasSubTree) {
                    options.type = 'Center';
                    options.orientation = 'Horizontal';
                }
            }
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Id',
            parentId: 'Team',
            dataSource: this.items
        }
    }
}
```

{% endtab %}

### Symmetric layout

The symmetric layout has been formed using nodes position by closer together or pushing them further apart. This is repeated iteratively until the system comes to an equilibrium state.

The layout’s [`springLength`](../api/diagram/layout) defined as how long edges should be, ideally. This will be the resting length for the springs. Edge attraction and vertex repulsion forces to be defined by using layout’s [`springFactor`](../api/diagram/layout), the more sibling nodes repel each other. The relative positions do not change any more from one iteration to the next. The number of iterations can be specified by using layout’s [`maxIteration`](../api/diagram/layout).

>Note: If you want to use symmetric layout in diagram, you need to inject SymmetricLayout in the diagram.

### Mind Map layout

A mind map is a diagram that displays the nodes as a spider diagram organizes information around a central concept. To create mind map, the [`type`](../api/diagram/layout) of layout should be set as `MindMap`.

>Note: If you want to use mind map layout in diagram, you need to inject MindMap in the diagram.

The following code example illustrates how to create an organizational chart.

{% tab template="diagram/automaticlayout/mindmap", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, DataBinding,Diagram,HierarchicalTree, NodeModel, ConnectorModel, MindMap,SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';
Diagram.Inject( MindMap );

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            id: 1,
            Label: 'StackPanel'
        },
        {
            id: 2,
            Label: 'Label',
            parentId: 1
        },
        {
            id: 3,
            Label: 'ListBox',
            parentId: 1
        },
        {
            id: 4,
            Label: 'StackPanel',
            parentId: 2
        },
        {
            id: 5,
            Label: 'Border',
            parentId: 2
        },
        {
            id: 6,
            Label: 'Border',
            parentId: 4
        },
        {
            id: 7,
            Label: 'Button',
            parentId: 4
        },
        {
            id: 8,
            Label: 'ContentPresenter',
            parentId: 5
        },
        {
            id: 9,
            Label: 'Text Block',
            parentId: 5
        },
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.shape = {
            type: 'Text',
            content: (obj.data as {
                Label: 'string'
            }).Label,
        };
        obj.style = {
            fill: '#6BA5D7',
            strokeColor: 'none',
            strokeWidth: 2
        };
        obj.borderColor = 'white';
        obj.backgroundColor = '#6BA5D7';
        obj.borderWidth = 1;
        (obj.shape as TextModel).margin = {
            left: 5,
            right: 5,
            top: 5,
            bottom: 5
        };
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.targetDecorator.shape = 'None';
        connector.type = 'Orthogonal';
        return connector;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
        //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            //Sets layout type
            type: 'MindMap'
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'id',
            parentId: 'parentId',
            dataSource: this.items,
            root: String(1)
        }
    }
}
```

{% endtab %}

### Complex hierarchical tree

Complex hierarchical tree layout is the extended version of the hierarchical tree layout. The child had been two or more parents. To create a complex hierarchical tree, the [`type`](../api/diagram/layout) of layout should be set as `ComplexHierarchicalTree`.

The following code example illustrates how to create a complex hierarchical tree.

{% tab template="diagram/automaticlayout/complexhiertree", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent } from '@syncfusion/ej2-angular-diagrams';
import {
    NodeModel, ConnectorModel, DiagramTools, Diagram, DataBinding, ComplexHierarchicalTree,
    SnapConstraints, SnapSettingsModel, LayoutModel, LayoutOrientation
} from '@syncfusion/ej2-diagrams';
import { DataManager } from '@syncfusion/ej2-data';
import { ChangeEventArgs as NumericChangeEventArgs } from '@syncfusion/ej2-inputs';
import * as Data from '../diagram-data.json';
Diagram.Inject(DataBinding, ComplexHierarchicalTree);

export interface DataInfo {
    [key: string]: string;
}

/**
 * Sample for Multiple parent sample
 */
@Component({
    selector: 'app-container',
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getConnectorDefaults]='connDefaults'
    [getNodeDefaults]='nodeDefaults' [tool]='tool' [layout]='layout' [dataSourceSettings]='data' [snapSettings]='snapSettings'
    (created)="created()"></ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {
    @ViewChild('diagram')
    public diagram: DiagramComponent;

    public nodeDefaults(obj: NodeModel): NodeModel {
        obj.width = 40; obj.height = 40;
        //Initialize shape
        obj.shape = { type: 'Basic', shape: 'Rectangle', cornerRadius: 7 };
        return obj;
    };
    public data: Object = {
        id: 'Name', parentId: 'ReportingPerson',
        dataSource: new DataManager([
            {"Name": "node11","fillColor": "#e7704c","border": "#c15433"},
            {"Name": "node12","ReportingPerson": ["node114"],"fillColor": "#efd46e","border": "#d6b123"},
            {"Name": "node13","ReportingPerson": ["node12"],"fillColor": "#58b087","border": "#16955e"},
            {"Name": "node14","ReportingPerson": ["node12"],"fillColor": "#58b087","border": "#16955e"},
            {"Name": "node15","ReportingPerson": ["node12"],"fillColor": "#58b087","border": "#16955e"},
            {"Name": "node16","ReportingPerson": [],"fillColor": "#14ad85"},
            {"Name": "node17","ReportingPerson": ["node13","node14","node15"],"fillColor": "#659be5","border": "#3a6eb5"},
            {"Name": "node18","ReportingPerson": [],"fillColor": "#14ad85"},
            {"Name": "node19","ReportingPerson": ["node16","node17","node18"],"fillColor": "#8dbe6c","border": "#489911"},
            {"Name": "node110","ReportingPerson": ["node16","node17","node18"],"fillColor": "#8dbe6c","border": "#489911"},
            {"Name": "node111","ReportingPerson": ["node16","node17","node18","node116"],"fillColor": "#8dbe6c","border": "#489911"},
            {"Name": "node21","fillColor": "#e7704c","border": "#c15433"},
            {"Name": "node22","ReportingPerson": ["node114"],"fillColor": "#efd46e","border": "#d6b123"},
            {"Name": "node23","ReportingPerson": ["node22"],"fillColor": "#58b087","border": "#16955e"},
            {"Name": "node24","ReportingPerson": ["node22"],"fillColor": "#58b087","border": "#16955e"},
            {"Name": "node25","ReportingPerson": ["node22"],"fillColor": "#58b087","border": "#16955e"},
            {"Name": "node26","ReportingPerson": [],"fillColor": "#14ad85"},
            {"Name": "node27","ReportingPerson": ["node23","node24","node25"],"fillColor": "#659be5","border": "#3a6eb5"},
            {"Name": "node28","ReportingPerson": [],"fillColor": "#14ad85"},
            {"Name": "node29","ReportingPerson": ["node26","node27","node28","node116"],"fillColor": "#8dbe6c","border": "#489911"},
            {"Name": "node210","ReportingPerson": ["node26","node27","node28"],"fillColor": "#8dbe6c","border": "#489911"},
            {"Name": "node211","ReportingPerson": ["node26","node27","node28"],"fillColor": "#8dbe6c","border": "#489911"},
            {"Name": "node31","fillColor": "#e7704c","border": "#c15433"},
            {"Name": "node114","ReportingPerson": ["node11","node21","node31"],"fillColor": "#f3904a","border": "#d3722e"},
            {"Name": "node116","ReportingPerson": ["node12","node22"],"fillColor": "#58b087","border": "#16955e"}
        ],),
        //binds the external data with node
        doBinding: (nodeModel: NodeModel, data: DataInfo, diagram: Diagram) => {
            /* tslint:disable:no-string-literal */
            nodeModel.style = { fill: data['fillColor'], strokeWidth: 1, strokeColor: data['border'] };
        }
    };
    public created(): void {
        this.diagram.fitToPage();
    };
    public connDefaults(connector: ConnectorModel): void {
        connector.type = 'Orthogonal';
        connector.cornerRadius = 7;
        connector.targetDecorator.height = 7;
        connector.targetDecorator.width = 7;
        connector.style.strokeColor = '#6d6d6d';
    };

    public tool: DiagramTools = DiagramTools.ZoomPan;

    public snapSettings: SnapSettingsModel = { constraints: SnapConstraints.None };

    public layout: LayoutModel = {
        type: 'ComplexHierarchicalTree',
        horizontalSpacing: 40, verticalSpacing: 40, orientation: 'TopToBottom',
        margin: { left: 10, right: 0, top: 50, bottom: 0 }
    };
}
```

{% endtab %}

>Note: If you want to use Complex hierarchical layout in diagram, you need to inject ComplexHierarchicalTree in the diagram.

### Customize layout

Orientation, spacings, and position of the layout can be customized with a set of properties.

To explore layout properties, refer to [`Layout Properties`](../api/diagram/layout).

**Layout bounds**
Diagram provides support to align the layout within any custom rectangular area. For more information about bounds, refer to [`bounds`](../api/diagram/layout).

**Layout alignment**
The layout can be aligned anywhere over the layout bounds/viewport using the [`horizontalAlignment`](../api/diagram/layout) and [`verticalAlignment`](../api/diagram/layout) properties of the layout.

The following code illustrates how to align the layout at the top-left of the layout bounds.

{% tab template="diagram/automaticlayout/alignment", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            Name: "Steve-Ceo"
        },
        {
            Name: "Kevin-Manager",
            ReportingPerson: "Steve-Ceo"
        },
        {
            Name: "Peter-Manager",
            ReportingPerson: "Kevin-Manager"
        },
        {
            Name: "John- Manager",
            ReportingPerson: "Peter-Manager"
        },
        {
            Name: "Mary-CSE ",
            ReportingPerson: "Peter-Manager"
        },
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.shape = {
            type: 'Text',
            content: (obj.data as {
                Name: 'string'
            }).Name
        };
        obj.style = {
            fill: 'None',
            strokeColor: 'none',
            strokeWidth: 2,
            bold: true,
            color: 'white'
        };
        obj.width = 100;
        obj.height = 40;
        obj.borderColor = 'white';
        obj.backgroundColor = '#6BA5D7';
        obj.borderWidth = 1;
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.type = 'Orthogonal';
        return connector;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
            //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            //Sets layout type
            type: 'HierarchicalTree',
            //set layout alignment
            //bounds: new Rect(0, 0, 500, 500),
            horizontalSpacing: 25,
            verticalSpacing: 30,
            horizontalAlignment: 'Left',
            verticalAlignment: 'Top'
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Name',
            parentId: 'ReportingPerson',
            dataSource: this.items
        }
    }
}
```

{% endtab %}

**Layout spacing**
Layout provides support to add space horizontally and vertically between the nodes. The [`horizontalSpacing`](../api/diagram/layout) and [`verticalSpacing`](../api/diagram/layout) properties of the layout allows you to set the space between the nodes in horizontally and vertically.

**Layout margin**
Layout provides support to add some blank space between the layout bounds/viewport and the layout. The [`margin`](../api/diagram/layout) property of the layout allows you to set the blank space.

The following code illustrates how to set the layout margin.

{% tab template="diagram/automaticlayout/spacing", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            Name: "Steve-Ceo"
        },
        {
            Name: "Kevin-Manager",
            ReportingPerson: "Steve-Ceo"
        },
        {
            Name: "Peter-Manager",
            ReportingPerson: "Kevin-Manager"
        },
        {
            Name: "John- Manager",
            ReportingPerson: "Peter-Manager"
        },
        {
            Name: "Mary-CSE ",
            ReportingPerson: "Peter-Manager"
        },
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.shape = {
            type: 'Text',
            content: (obj.data as {
                Name: 'string'
            }).Name
        };
        obj.style = {
            fill: 'None',
            strokeColor: 'none',
            strokeWidth: 2,
            bold: true,
            color: 'white'
        };
        obj.width = 100;
        obj.height = 40;
        obj.borderColor = 'white';
        obj.backgroundColor = '#6BA5D7';
        obj.borderWidth = 1;
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.type = 'Orthogonal';
        return connector;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
            //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            //Sets layout type
            type: 'HierarchicalTree',
            //bounds: new Rect(0, 0, 500, 500),
            horizontalSpacing: 25,
            verticalSpacing: 30,
            horizontalAlignment: 'Left',
            verticalAlignment: 'Top'
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Name',
            parentId: 'ReportingPerson',
            dataSource: this.items
        }
    }
}
```

{% endtab %}

**Layout orientation**
Diagram provides support to customize the  [`orientation`](../api/diagram/layout) of layout. You can set the desired orientation using layout.orientation.

The following code illustrates how to arrange the nodes in a BottomToTop orientation.

{% tab template="diagram/automaticlayout/spacing", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            Name: "Steve-Ceo"
        },
        {
            Name: "Kevin-Manager",
            ReportingPerson: "Steve-Ceo"
        },
        {
            Name: "Peter-Manager",
            ReportingPerson: "Kevin-Manager"
        },
        {
            Name: "John- Manager",
            ReportingPerson: "Peter-Manager"
        },
        {
            Name: "Mary-CSE ",
            ReportingPerson: "Peter-Manager"
        },
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.shape = {
            type: 'Text',
            content: (obj.data as {
                Name: 'string'
            }).Name
        };
        obj.style = {
            fill: 'None',
            strokeColor: 'none',
            strokeWidth: 2,
            bold: true,
            color: 'white'
        };
        obj.width = 100;
        obj.height = 40;
        obj.borderColor = 'white';
        obj.backgroundColor = '#6BA5D7';
        obj.borderWidth = 1;
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.type = 'Orthogonal';
        return connector;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
            //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            //Sets layout type
            type: 'HierarchicalTree',
            //bounds: new Rect(0, 0, 500, 500),
            horizontalSpacing: 25,
            verticalSpacing: 30,
            horizontalAlignment: 'Left',
            verticalAlignment: 'Top',
            orientation: 'BottomToTop'
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Name',
            parentId: 'ReportingPerson',
            dataSource: this.items
        }
    }
}
```

{% endtab %}

**Fixed node**
Layout provides support to arrange the nodes with reference to the position of a fixed node and set it to the [`fixedNode`](../api/diagram/layout) of the layout property. This is helpful when you try to expand/collapse a node. It might be expected that the position of the double-clicked node should not be changed.

{% tab template="diagram/automaticlayout/fixed", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            Name: "Steve-Ceo",
            //set the offsetX and offsetY for the parent node
            offsetX: 250,
            offsetY: 50
        },
        {
            Name: "Kevin-Manager",
            ReportingPerson: "Steve-Ceo"
        },
        {
            Name: "Peter-Manager",
            ReportingPerson: "Steve-Ceo"
        },
        {
            Name: "John- Manager",
            ReportingPerson: "Peter-Manager"
        },
        {
            Name: "Mary-CSE ",
            ReportingPerson: "Peter-Manager"
        },
        {
            Name: "Jim-CSE ",
            ReportingPerson: "Kevin-Manager"
        },
        {
            Name: "Martin-CSE",
            ReportingPerson: "Kevin-Manager"
        }
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.shape = {
            type: 'Text',
            content: (obj.data as {
                Name: 'string'
            }).Name
        };
        obj.style = {
            fill: 'None',
            strokeColor: 'none',
            strokeWidth: 2,
            bold: true,
            color: 'white'
        };
        obj.width = 100;
        obj.height = 40;
        obj.borderColor = 'white';
        obj.backgroundColor = '#6BA5D7';
        obj.borderWidth = 1;
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.type = 'Orthogonal';
        return connector;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
            //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            type: 'HierarchicalTree',
            //bounds: new Rect(0, 0, 500, 500),
            horizontalSpacing: 25,
            verticalSpacing: 30,
            horizontalAlignment: 'Left',
            verticalAlignment: 'Top'
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Name',
            parentId: 'ReportingPerson',
            dataSource: this.items
        }
    }
}
```

{% endtab %}

**Expand and collapse**
Diagram allows to expand/collapse the subtrees of a layout. The node’s isExpanded property allows you to expand/collapse its children. The following code example shows how to expand/collapse the children of a node.

{% tab template="diagram/automaticlayout/expandandcollapse", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SelectorModel, SelectorConstraints, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [selectedItems]="selectedItems" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public selectedItems: SelectorModel;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            'Id': 'parent1',
            'Name': 'Maria ',
            'Designation': 'Managing Director',
            'RatingColor': '#C34444'
        },
        {
            'Id': 'parent',
            'Name': ' sam',
            'Designation': 'Managing Director',
            'ReportingPerson': 'parent1',
            'RatingColor': '#C34444'
        },
        {
            'Id': 'parent3',
            'Name': ' sam geo',
            'Designation': 'Managing Director',
            'ReportingPerson': 'parent1',
            'RatingColor': '#C34444'
        },
        {
            'Id': '80',
            'Name': ' david',
            'Designation': 'Managing Director',
            'ReportingPerson': 'parent3',
            'RatingColor': '#C34444'
        },
        {
            'Id': '82',
            'Name': ' pirlo',
            'Designation': 'Managing Director',
            'ReportingPerson': 'parent',
            'RatingColor': '#C34444'
        }
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.expandIcon = {
            height: 15,
            width: 15,
            shape: "Plus",
            fill: 'lightgray',
            offset: {
                x: .5,
                y: .85
            }
        }
        obj.collapseIcon.offset = {
            x: .5,
            y: .85
        }
        obj.collapseIcon.height = 15;
        obj.collapseIcon.width = 15;
        obj.collapseIcon.shape = "Minus";
        obj.height = 50;
        obj.borderColor = 'white';
        obj.backgroundColor = '#6BA5D7';
        obj.borderWidth = 1;
        obj.style = {
            fill: 'transparent',
            strokeWidth: 2
        };
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.targetDecorator.shape = 'None';
        connector.type = 'Orthogonal';
        return connector;
    }
    ngOnInit(): void {
        this.selectedItems = {
            constraints: ~SelectorConstraints.ResizeAll
        }
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
            //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            // set enableAnimation as true
            enableAnimation: true,
            type: 'OrganizationalChart',
            margin: {
                top: 20
            },// define the getLayoutInfo
            getLayoutInfo: (node: Node, tree: TreeInfo) => {
                if (!tree.hasSubTree) {
                    tree.orientation = 'vertical';
                    tree.type = 'alternate';
                }
            }
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Id',
            parentId: 'ReportingPerson',
            dataSource: this.items
        }
    }
}
```

{% endtab %}

In the previous example, while expanding/collapsing a node, it is set as fixed node in order to prevent it from repositioning.

**Refresh layout**
Diagram allows to refresh the layout at runtime. To refresh the layout, refer to [`Refresh layout`](../api/diagram/#dolayout).

**setNodeTemplate**
 The [`setNodeTemplate`](../api/diagram/#setnodetemplate) function is provided for the purpose of customizing nodes. It will be called for each node on node initialization. In this function, the node style and its properties can be customized and can bind the custom JSON with node.

 {% tab template="diagram/automaticlayout/nodetemplate", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent, Diagram, NodeModel, ConnectorModel, SnapSettingsModel, LayoutModel, DataSourceModel } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings" [setNodeTemplate]="setNodeTemplate">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public snapSettings: SnapSettingsModel;
    public items: DataManager;
    public layout: LayoutModel;
    public dataSourceSettings: DataSourceModel;
    //Initializes data source
    public data: object[] = [{
            Name: "Steve-Ceo"
        },
        {
            Name: "Kevin-Manager",
            ReportingPerson: "Steve-Ceo"
        },
        {
            Name: "Peter-Manager",
            ReportingPerson: "Kevin-Manager"
        },
        {
            Name: "John- Manager",
            ReportingPerson: "Peter-Manager"
        },
        {
            Name: "Mary-CSE ",
            ReportingPerson: "Peter-Manager"
        },
    ];
    //Sets the default properties for all the Nodes
    public getNodeDefaults(obj: NodeModel, diagram: Diagram): NodeModel {
        obj.shape = {
            type: 'Text',
            content: (obj.data as {
                Name: 'string'
            }).Name
        };
        obj.style = {
            fill: 'None',
            strokeColor: 'none',
            strokeWidth: 2,
            bold: true,
            color: 'white'
        };
        obj.width = 50;
        obj.height = 40;
        obj.borderColor = 'white';
        obj.backgroundColor = '#6BA5D7';
        obj.borderWidth = 1;
        (obj.shape as TextModel).margin = {
            left: 25,
            right: 25,
            top: 25,
            bottom: 25
        };
        return obj;
    }
    //Sets the default properties for all the connectors
    public getConnectorDefaults(connector: ConnectorModel, diagram: Diagram): ConnectorModel {
        connector.style = {
            strokeColor: '#6BA5D7',
            strokeWidth: 2
        };
        connector.targetDecorator.style.fill  =  '#6BA5D7';
        connector.targetDecorator.style.strokeColor  =  '#6BA5D7';
        connector.targetDecorator.shape = 'None';
        connector.type = 'Orthogonal';
        return connector;
    }
    public setNodeTemplate(obj, diagram): void {
        obj.style.borderColor = (obj.data as {
            color: 'string'
        }).color;
    }
    ngOnInit(): void {
        this.snapSettings = {
            constraints: 0
        }
        this.items = new DataManager(this.data as JSON[], new Query().take(7));
            //Uses layout to auto-arrange nodes on the Diagram page
        this.layout = {
            type: 'HierarchicalTree',
            //bounds: new Rect(0, 0, 500, 500),
            horizontalSpacing: 25,
            verticalSpacing: 30,
            horizontalAlignment: 'Left',
            verticalAlignment: 'Top'
        }
        //Configures data source for Diagram
        this.dataSourceSettings = {
            id: 'Name',
            parentId: 'ReportingPerson',
            dataSource: this.items
        }
    }
}
```

{% endtab %}