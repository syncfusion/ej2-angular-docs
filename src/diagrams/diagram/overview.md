---
title: "Overview Control"
component: "Diagram"
description: "Overview control allows you to see a preview or an overall view of the entire content of a diagram."
---

# Overview Control

Overview control allows you to see a preview or an overall view of the entire content of a Diagram. This helps you to look at the overall picture of a large Diagram and also to navigate, pan, or zoom, on a particular position of the page.

When you work on a very large Diagram, you may not know the part you are actually working on, or navigation from one part to another might be difficult. One solution for navigation is to zoom out the entire Diagram and find where you are. Then, you can zoom in a particular area you want to. This solution is not suitable when you need some frequent navigation.

Overview control solves these problems by showing you a preview, that is, an overall view of the entire Diagram. A rectangle indicates viewport of the Diagram. Navigation becomes easy by dragging this rectangle.

## Create overview

The `sourceID` property of overview should be set with the corresponding Diagram ID for you need the overall view.

The `width` and `height` property of the overview allows you to define the size of the overview.

The following code illustrates how to create overview.

### Zoom and Pan

In overview, the view port of the Diagram is highlighted with a red colored rectangle. Diagram can be zoomed/panned by interacting with that. You can interact with overview as follows.

*Resize the rectangle - Zooms in/out the Diagram
*Drag the rectangle - Pans the Diagram
*Click at a position - Navigates to the clicked region
*Choose a particular region by clicking and dragging - Navigates to the specified region

The following image shows how the Diagram is zoomed/panned with overview.

{% tab template="diagram/overview/overview", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { DiagramComponent,OverviewComponent, Diagram, NodeModel, ConnectorModel,OverviewModel, SnapSettingsModel, LayoutModel, DataSourceModel,  } from '@syncfusion/ej2-angular-diagrams';
import { DataManager, Query } from '@syncfusion/ej2-data';

@Component({
    selector: "app-container",
    template: `<div><ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]="getNodeDefaults" [getConnectorDefaults]="getConnectorDefaults" [snapSettings]="snapSettings" [layout]="layout" [dataSourceSettings]="dataSourceSettings">
    </ejs-diagram></div>
    <div style=" width:50%; height: 200px padding:0px;right:5px;bottom:5px;background:#f7f7f7;position:absolute">
    <ejs-overview id="overview" width="100%" sourceID="diagram">
        </ejs-overview>
        </div>`,
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
