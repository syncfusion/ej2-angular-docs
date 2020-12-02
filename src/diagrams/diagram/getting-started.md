---
title: "Getting Started"
component: "Diagram"
description: "Diagram getting started creates your first flow diagram and organizational chart diagram."
---

# Getting Started

This section explains you the steps required to create a simple diagram and demonstrate the basic usage of the diagram control.

## Setup Angular Environment

You can use [`Angular CLI`](https://github.com/angular/angular-cli) to setup your Angular applications.
To install Angular CLI use the following command.

```bash
npm install -g @angular/cli
```

## Create an Angular Application

Start a new Angular application using below Angular CLI command.

```bash
ng new my-app
cd my-app
```

## Adding Syncfusion Diagram package

All the available Essential JS 2 packages are published in [`npmjs.com`](https://www.npmjs.com/~syncfusionorg) registry.

To install Diagram component, use the following command.

```bash
npm install @syncfusion/ej2-angular-diagrams --save
```

> The **--save** will instruct NPM to include the diagram package inside of the `dependencies` section of the `package.json`.

## Registering Diagram Module

Import Diagram module into Angular application(app.module.ts) from the package `@syncfusion/ej2-angular-diagrams` [src/app/app.module.ts].

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the DiagramMOdule for the Diagram component
import { DiagramModule } from '@syncfusion/ej2-angular-diagrams';
import { AppComponent }  from './app.component';

@NgModule({
  //declaration of ej2-angular-diagrams module into NgModule
  imports:      [ BrowserModule, DiagramModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

## Adding CSS reference

Combined CSS files are available in the Essential JS 2 package root folder.
This can be referenced in [src/styles.css] using following code.

```css
@import '../node_modules/@syncfusion/ej2-angular-diagrams/styles/material.css';
```

## Add Diagram component

Modify the template in [src/app/app.component.ts] file to render the diagram component.
Add the Angular Diagram by using `<ejs-diagram>` selector in `template` section of the app.component.ts file.

```typescript
import { Component, OnInit, ViewEncapsulation} from '@angular/core';

@Component({
  selector: 'app-container',
  // specifies the template string for the Diagram component
  template: `<ejs-diagram id='diagram-container'></ejs-diagram>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent implements OnInit {

    ngOnInit(): void {
    }
}

```

## Defining Basic Diagram

The below example shows a basic Diagrams

{% tab template="diagram/getting-started/initialize", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-container",
  // specifies the template string for the diagram component
  template: `<ejs-diagram id="diagram" width="100%" height="580px"></ejs-diagram>`
})
export class AppComponent {}
```

{% endtab %}

Now, run the application by using npm start command. Open the browser with the generated link and you can see an empty diagram.

```bash
npm start
```

## Module Injection

The diagram component is divided into individual feature-wise modules. In order to use a particular feature, inject the required module. The following list describes the module names and their description.

* `BpmnDiagramsService` - Inject this provider to add built-in BPMN Shapes to diagrams.
* `ConnectorBridgingService` - Inject this provider to add bridges to connectors.
* `ConnectorEditingService` - Inject this provider to edit the segments for connector.
* `ComplexHierarchicalTreeService` - Inject this provider to complex hierarchical tree like structure.
* `DataBindingService` - Inject this provider to populate nodes from given data source.
* `DiagramContextMenuService` - Inject this provider to manipulate context menu.
* `HierarchicalTreeService` - Inject this provider to use hierarchical tree like structure.
* `LayoutAnimationService` - Inject this provider animation to layouts.
* `MindMapService` - Inject this provider to use mind map.
* `PrintAndExportService` - Inject this provider to print or export the objects.
* `RadialTreeService` - Inject this provider to use Radial tree like structure.
* `SnappingService` - Inject this provider to Snap the objects.
* `SymmetricLayoutService` - Inject this provider to render layout in symmetrical method.
* `UndoRedoService` - Inject this provider to revert and restore the changes.

These modules should be imported and injected into the Diagram component using `Diagram.Inject` method as follows.

```javascript
   import { NgModule } from '@angular/core';
   import { BrowserModule } from '@angular/platform-browser';
   import { AppComponent } from './app.component';
   import { DiagramModule } from '@syncfusion/ej2-angular-diagrams';
   import { HierarchicalTreeService, MindMapService, RadialTreeService, ComplexHierarchicalTreeService } from '@syncfusion/ej2-angular-diagrams';
   import { DataBindingService, SnappingService, PrintAndExportService, BpmnDiagramsService} from '@syncfusion/ej2-angular-diagrams';
   import { SymmetricLayoutService, ConnectorBridgingService, UndoRedoService, LayoutAnimationService} from '@syncfusion/ej2-angular-diagrams';
   import { DiagramContextMenuService, ConnectorEditingService } from '@syncfusion/ej2-angular-diagrams';

   @NgModule({
       imports: [
           BrowserModule, DiagramModule
       ],
       declarations: [AppComponent],
       bootstrap: [AppComponent],
       providers: [ HierarchicalTreeService, MindMapService, RadialTreeService, ComplexHierarchicalTreeService, DataBindingService, SnappingService, PrintAndExportService, BpmnDiagramsService, SymmetricLayoutService, ConnectorBridgingService, UndoRedoService, LayoutAnimationService, DiagramContextMenuService, ConnectorEditingService ]
   })
```

## Flow Diagram

### Create and Add Node

Create and add a `node` (JSON data) with specific position, size, label, and shape.

{% tab template="diagram/getting-started/connectnode", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { BasicShapeModel } from "@syncfusion/ej2-angular-diagrams";

@Component({
  selector: "app-container",
  template: `<ejs-diagram id="diagram" width="100%" height="580px" mode="SVG">
    <e-nodes>
        <e-node id='node1' [height]=60 [width]=100 [offsetX]=300 [offsetY]=80 [shape]='shape'>
            <e-node-annotations>
                <e-node-annotation content='Start'></e-node-annotation>
            </e-node-annotations>
        </e-node>
        <e-node id='node2' [height]=60 [width]=100 [offsetX]=300 [offsetY]=160 [shape]='shape'>
            <e-node-annotations>
                <e-node-annotation content='var i = 0;'></e-node-annotation>
            </e-node-annotations>
        </e-node>
    </e-nodes>
    <e-connectors>
        <e-connector id='connector1' sourceID='node1' targetID='node2'></e-connector>
    </e-connectors>
  </ejs-diagram>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  @ViewChild("diagram")
  public shape: BasicShapeModel;
  ngOnInit(): void {
    this.shape = { type: "Basic", shape: "Rectangle" };
  }
}
```

{% endtab %}

### Connect two Nodes with a Connector

Add two node to the diagram as shown in the previous example. Connect these nodes by adding a connector using the `connector` property and refer the source and target end by using the `sourceNode` and `tagetNode` properties.

{% tab template="diagram/getting-started/connectnode", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { BasicShapeModel } from "@syncfusion/ej2-angular-diagrams";

@Component({
  selector: "app-container",
  template: `<ejs-diagram id="diagram" width="100%" height="580px" mode="SVG">
    <e-nodes>
        <e-node id='node1' [height]=60 [width]=100 [offsetX]=300 [offsetY]=80 [shape]='shape'>
            <e-node-annotations>
                <e-node-annotation content='Start'></e-node-annotation>
            </e-node-annotations>
        </e-node>
        <e-node id='node2' [height]=60 [width]=100 [offsetX]=300 [offsetY]=160 [shape]='shape'>
            <e-node-annotations>
                <e-node-annotation content='var i = 0;'></e-node-annotation>
            </e-node-annotations>
        </e-node>
    </e-nodes>
    <e-connectors>
        <e-connector id='connector1' sourceID='node1' targetID='node2'></e-connector>
    </e-connectors>
  </ejs-diagram>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  @ViewChild("diagram")
  public shape: BasicShapeModel;
  ngOnInit(): void {
    this.shape = { type: "Basic", shape: "Rectangle" };
  }
}
```

{% endtab %}

Default values for all `nodes` and `connectors` can be set using the `getNodeDefaults` and `getConnectorDefaults` properties, respectively. For example, if all nodes have the same width and height, such properties can be moved into `getNodeDefaults`.

### Complete Flow Diagram

Similarly, the required nodes and connectors can be added to form a complete flow diagram.

{% tab template="diagram/getting-started/flowdiagram", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import {
  FlowShapeModel,
  NodeModel,
  ConnectorModel,
  OrthogonalSegmentModel
} from "@syncfusion/ej2-angular-diagrams";

@Component({
  selector: "app-container",
  template: `<ejs-diagram id="diagram" width="100%" height="580px" [getNodeDefaults]='nodeDefaults' [getConnectorDefaults]='connectorDefaults'>
    <e-nodes>
        <e-node id='node1' [offsetY]=50 [shape]='terminator'>
            <e-node-annotations>
                <e-node-annotation content='Start'></e-node-annotation>
            </e-node-annotations>
        </e-node>
        <e-node id='node2' [offsetY]=140 [shape]='process'>
            <e-node-annotations>
                <e-node-annotation content='var i = 0;'></e-node-annotation>
            </e-node-annotations>
        </e-node>
        <e-node id='node3' [offsetY]=230 [shape]='decision'>
            <e-node-annotations>
                <e-node-annotation content='i < 10?'></e-node-annotation>
            </e-node-annotations>
        </e-node>
        <e-node id='node4' [offsetY]=320 [shape]='preDefinedProcess'>
            <e-node-annotations>
                <e-node-annotation content='print(\"Hello!!\");'></e-node-annotation>
            </e-node-annotations>
        </e-node>
        <e-node id='node5' [offsetY]=410 [shape]='process'>
            <e-node-annotations>
                <e-node-annotation content='i++;'></e-node-annotation>
            </e-node-annotations>
        </e-node>
        <e-node id='node6' [offsetY]=500 [shape]='terminator'>
            <e-node-annotations>
                <e-node-annotation content='End'></e-node-annotation>
            </e-node-annotations>
        </e-node>
    </e-nodes>
    <e-connectors>
        <e-connector id='connector1' sourceID='node1' targetID='node2'></e-connector>
        <e-connector id='connector2' sourceID='node2' targetID='node3'></e-connector>
        <e-connector id='connector3' sourceID='node3' targetID='node4'>
            <e-connector-annotations>
                <<e-connector-annotation content='Yes'></e-connector-annotation>
            </e-connector-annotations>
        </e-connector>
        <e-connector id='connector4' sourceID='node3' targetID='node6' [segments]='segment1'>
            <e-connector-annotations>
                <e-connector-annotation content='No'></e-connector-annotation>
            </e-connector-annotations>
        </e-connector>
        <e-connector id='connector5' sourceID='node4' targetID='node5'></e-connector>
        <e-connector id='connector6' sourceID='node5' targetID='node3' [segments]='segment2'></e-connector>
    </e-connectors>
</ejs-diagram>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  @ViewChild("diagram")
  public terminator: FlowShapeModel;
  public process: FlowShapeModel;
  public decision: FlowShapeModel;
  public preDefinedProcess: FlowShapeModel;
  public segment1: OrthogonalSegmentModel;
  public segment2: OrthogonalSegmentModel;
  public nodeDefaults(node: NodeModel): NodeModel {
    node.height = 50;
    node.width = 140;
    node.offsetX = 300;
    return node;
  },

  public connectorDefaults(obj: ConnectorModel): ConnectorModel {
    obj.type = "Orthogonal";
    obj.targetDecorator = { shape: "Arrow", width: 10, height: 10 };
    return obj;
  }
  ngOnInit(): void {
    this.terminator = { type: 'Flow', shape: 'Terminator' };
    this.process = { type: 'Flow', shape: 'Process' };
    this.decision = { type: 'Flow', shape: 'Decision' };
    this.preDefinedProcess = { type: 'Flow', shape: 'PreDefinedProcess' };
    this.segment1 = [{ length: 30, direction: "Right" }, { length: 300, direction: "Bottom" }];
    this.segment2 = [{ length: 30, direction: "Left" }, { length: 200, direction: "Top" }];
  }
}
```

{% endtab %}

## Automatic Organization Chart

In the 'Flow Diagram' section, how to create a diagram manually was discussed. This section explains how to create and position the diagram automatically.

### Business object (Employee information)

Define Employee Information as JSON data. The following code example shows an employee array whose, `Name` is used as an unique identifier and `ReportingPerson` is used to identify the person to whom an employee report to, in the organization.

```typescript
    public data: Object[] = [
        {
            Name: "Elizabeth",
            Role: "Director"
        },
        {
            Name: "Christina",
            ReportingPerson: "Elizabeth",
            Role: "Manager"
        },
        {
            Name: "Yoshi",
            ReportingPerson: "Christina",
            Role: "Lead"
        },
        {
            Name: "Philip",
            ReportingPerson: "Christina",
            Role: "Lead"
        },
        {
            Name: "Yang",
            ReportingPerson: "Elizabeth",
            Role: "Manager"
        },
        {
            Name: "Roland",
            ReportingPerson: "Yang",
            Role: "Lead"
        },
        {
            Name: "Yvonne",
            ReportingPerson: "Yang",
            Role: "Lead"
        }
    ];
```

### Map data source

You can configure the above "Employee Information" with diagram, so that the nodes and connectors are automatically generated using the mapping properties. The following code example show how `dataSourceSettings` is used to map ID and parent with property name identifiers for employee information.

```typescript
@Component({
  selector: "app-container",
  template: `<ejs-diagram id="diagram" width="100%" height="580px" [dataSourceSettings]='dataSourceSettings'></ejs-diagram>`
})
export class AppComponent {
  @ViewChild("diagram")
  public dataSourceSettings: DataSourceModel;
  public data: Object[] = [
    {
      Name: "Elizabeth",
      Role: "Director"
    },
    {
      Name: "Christina",
      ReportingPerson: "Elizabeth",
      Role: "Manager"
    },
    {
      Name: "Yoshi",
      ReportingPerson: "Christina",
      Role: "Lead"
    },
    {
      Name: "Philip",
      ReportingPerson: "Christina",
      Role: "Lead"
    },
    {
      Name: "Yang",
      ReportingPerson: "Elizabeth",
      Role: "Manager"
    },
    {
      Name: "Roland",
      ReportingPerson: "Yang",
      Role: "Lead"
    },
    {
      Name: "Yvonne",
      ReportingPerson: "Yang",
      Role: "Lead"
    }
  ];
  ngOnInit(): void {
    this.dataSourceSettings = {
      id: "Name",
      parentId: "ReportingPerson",
      dataManager: new DataManager(this.data as JSON[])
    };
  }
}
```

### Visualize employee

The following code examples indicate how to define the default appearance of nodes and connectors. The `setNodeTemplate` is used to update each node based on employee data.

{% tab template="diagram/getting-started/orgchart", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewChild } from "@angular/core";
import {
  NodeModel,
  ConnectorModel,
  LayoutModel,
  Diagram,
  DataSourceModel
} from "@syncfusion/ej2-diagrams";
import { DataManager } from "@syncfusion/ej2-data";
export interface EmployeeInfo {
  Name: string;
  Role: string;
  color: string;
}

@Component({
  selector: "app-container",
  template: `<ejs-diagram id="diagram" width="100%" height="580px" [layout]='layout' [dataSourceSettings]='dataSourceSettings' [getNodeDefaults]='nodeDefaults' [getConnectorDefaults]='connectorDefaults'>
</ejs-diagram>`
})
export class AppComponent {
  @ViewChild("diagram") public layout: LayoutModel;
  public dataSourceSettings: DataSourceModel;
  public data: Object[] = [
    {
      Name: "Elizabeth",
      Role: "Director"
    },
    {
      Name: "Christina",
      ReportingPerson: "Elizabeth",
      Role: "Manager"
    },
    {
      Name: "Yoshi",
      ReportingPerson: "Christina",
      Role: "Lead"
    },
    {
      Name: "Philip",
      ReportingPerson: "Christina",
      Role: "Lead"
    },
    {
      Name: "Yang",
      ReportingPerson: "Elizabeth",
      Role: "Manager"
    },
    {
      Name: "Roland",
      ReportingPerson: "Yang",
      Role: "Lead"
    },
    {
      Name: "Yvonne",
      ReportingPerson: "Yang",
      Role: "Lead"
    }
  ];

  public nodeDefaults(node: NodeModel): NodeModel {
    let codes: Object = {
      Director: "rgb(0, 139,139)",
      Manager: "rgb(30, 30,113)",
      Lead: "rgb(0, 100,0)"
    };
    node.width = 70;
    node.height = 30;
    node.annotations = [
      { content: (node.data as EmployeeInfo).Name, style: { color: "white" } }
    ];
    node.style.fill = codes[(node.data as EmployeeInfo).Role];
    return node;
  }

  public connectorDefaults(connector: ConnectorModel): ConnectorModel {
    connector.type = "Orthogonal";
    connector.cornerRadius = 7;
    return connector;
  }
  ngOnInit(): void {
    this.layout = {
      type: "OrganizationalChart"
    };
    this.dataSourceSettings = {
      id: "Name",
      parentId: "ReportingPerson",
      dataManager: new DataManager(this.data as JSON[])
    };
  }
}
```

{% endtab %}

>Note: Please note that project generated through angular CLI project will always the changes made into application and compiled it automatically. We don’t need to run “npm start” command for each changes made into the application.