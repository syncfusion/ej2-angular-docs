---
title: "Context Menu"
component: "Diagram"
description: "Diagram context menu describes how to execute frequently used commands by using context menu items."
---

# Context Menu

<!-- markdownlint-disable MD010 -->

In graphical user interface (GUI), a context menu is a type of menu that appears when you perform right-click operation. Nested level of context menu items can be created.
Diagram provides some in-built context menu items and allows to define custom menu items through the [`contextMenuSettings`](../api/diagram#contextMenuSettings) property

## Customize context menu

The [`show`](../api/diagram/contextMenuSettings#show-boolean) property helps you to enable/disable the context menu. Diagram provides some default context menu items to ease the execution of some frequently used commands.
The following code illustrates how to enable the default context menu items.

{% tab template="diagram/contextmenu/contextmenu", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { DiagramComponent } from '@syncfusion/ej2-angular-diagrams';
import { ContextMenuSettingsModel, Diagram, NodeModel, ConnectorModel } from '@syncfusion/ej2-diagrams';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults] ='getNodeDefaults' [getConnectorDefaults]='getConnectorDefaults' [contextMenuSettings]="contextMenuSettings">
        <e-nodes>
            <e-node id='node1' [offsetX]=150 [offsetY]=150>
                <e-node-annotations>
                    <e-node-annotation id="label1" content="Rectangle1" [horizontalAlignment]="horizontalAlignment">
                    </e-node-annotation>
                </e-node-annotations>
            </e-node>
            <e-node id='node2' [offsetX]=350 [offsetY]=150>
                <e-node-annotations>
                    <e-node-annotation id="label1" content="Rectangle2" [horizontalAlignment]="horizontalAlignment">
                    </e-node-annotation>
                </e-node-annotations>
            </e-node>
        </e-nodes>
        <e-connectors>
            <e-connector id='connector' type='Orthogonal' sourceID='node1' targetID='node2'>
            </e-connector>
        </e-connectors>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public contextMenuSettings: ContextMenuSettingsModel
    ngOnInit(): void {
        //Enables the context menu
        this.contextMenuSettings = {
            show: true,
        }
    }
    public getNodeDefaults(node: NodeModel): NodeModel {
        node.height = 100;
        node.width = 100;
        node.style.fill = "#6BA5D7";
        node.style.strokeColor = "White";
        return node;
    }
    public getConnectorDefaults(obj: ConnectorModel): ConnectorModel {
        obj.style = {
            strokeColor: '#6BA5D7',
            fill: '#6BA5D7',
            strokeWidth: 2
        }
        obj.targetDecorator = {
            style: {
                fill: '#6BA5D7',
                strokeColor: '#6BA5D7'
            }
        }
    }
}
```

{% endtab %}

Context menu can be defined for individual node with the desired context menu items.

* Apart from the default context menu items, define some additional context menu items. Those additional items have to be defined and added to the [`items`](../api/diagram/contextMenuSettingsModel#items) property of the context menu.

* Set text and ID for context menu item using the context menu [`text`](../api/diagram/contextMenuItemModel#text-string) and [`ID`](../api/diagram/contextMenuItemModel#id-string) properties respectively.

* Set an image for the context menu item using the context menu [url](../api/diagram/contextMenuItemModel#url) property.

* The [`iconCss`](../api/diagram/contextMenuItemModel#iconCss-string) property defines the class/multiple classes separated by a space for the menu item that is used to include an icon. Menu item can include font icon and sprite image.

* The [`target`](../api/diagram/contextMenuItemModel#target-string) property used to set the target to show the menu item.

* The [`separator`](../api/diagram/contextMenuItemModel#separator-boolean) property defines the horizontal lines that are used to separate the menu items. You cannot select the separators. You can enable separators to group the menu items using the separator property.

The following code example illustrates how to add custom context menu items.

{% tab template="diagram/contextmenu/custom", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { DiagramComponent } from '@syncfusion/ej2-angular-diagrams';
import { ContextMenuSettingsModel, Diagram, NodeModel, ConnectorModel } from '@syncfusion/ej2-diagrams';
import { MenuEventArgs } from '@syncfusion/ej2-navigations';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults] ='getNodeDefaults' [getConnectorDefaults]='getConnectorDefaults' [contextMenuSettings]="contextMenuSettings">
        <e-nodes>
            <e-node id='node1' [offsetX]=150 [offsetY]=150>
                <e-node-annotations>
                    <e-node-annotation id="label1" content="Rectangle1" [horizontalAlignment]="horizontalAlignment">
                    </e-node-annotation>
                </e-node-annotations>
            </e-node>
            <e-node id='node2' [offsetX]=350 [offsetY]=150>
                <e-node-annotations>
                    <e-node-annotation id="label1" content="Rectangle2" [horizontalAlignment]="horizontalAlignment">
                    </e-node-annotation>
                </e-node-annotations>
            </e-node>
        </e-nodes>
        <e-connectors>
            <e-connector id='connector' type='Orthogonal' sourceID='node1' targetID='node2'>
            </e-connector>
        </e-connectors>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public contextMenuSettings: ContextMenuSettingsModel
    ngOnInit(): void {
        //Enables the context menu
        this.contextMenuSettings = {
            //Enables the context menu
            show: true,
            // Defines the custom context menu items
            items: [{
                    // Text to be displayed
                    text: 'Save',
                    //Sets the id for the item
                    id: 'save',
                    //ContextMenu can be visible based on the target in which you open the ContextMenu.
                    target: '.e-elementcontent',
                    // Sets the css icons for the item
                    iconCss: 'e-save'
                },
                {
                    text: 'Load',
                    id: 'load',
                    target: '.e-elementcontent',
                    iconCss: 'e-load'
                },
                {
                    text: 'Clear',
                    id: 'clear',
                    target: '.e-elementcontent',
                    iconCss: 'e-clear'
                }
            ],
            // Hides the default context menu items
            showCustomMenuOnly: false,
        }
    }
    public getNodeDefaults(node: NodeModel): NodeModel {
        node.height = 100;
        node.width = 100;
        node.style.fill = "#6BA5D7";
        node.style.strokeColor = "White";
        return node;
    }
    public getConnectorDefaults(obj: ConnectorModel): ConnectorModel {
        obj.style = {
            strokeColor: '#6BA5D7',
            fill: '#6BA5D7',
            strokeWidth: 2
        }
        obj.targetDecorator = {
            style: {
                fill: '#6BA5D7',
                strokeColor: '#6BA5D7'
            }
        }
    }
}
```

{% endtab %}

To display the custom context menu items alone, set  the [`showCustomMenuOnly`](../api/diagram/contextMenuSettingsModel#showCustomMenuOnly) property to true.

## Template Support for Context menu

* Diagram provides template support for context menu. The context menu items can be customized by using the `contextMenuBeforeItemRender` event. The contextMenuBeforeItemRender event triggers while rendering each menu item.

* In the following sample, the menu item is rendered with key code for specified action in ContextMenu using the template. Here, the key code is specified for the cut and copy at right corner of the menu items by adding a span element in the `contextMenuBeforeItemRender` event.

{% tab template= "diagram/contextmenu/menutemplate", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { createElement } from "@syncfusion/ej2-base";
import { DiagramComponent } from '@syncfusion/ej2-angular-diagrams';
import { ContextMenuSettingsModel, Diagram, NodeModel, ConnectorModel } from '@syncfusion/ej2-diagrams';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults] ='getNodeDefaults' [getConnectorDefaults]='getConnectorDefaults' [contextMenuSettings]="contextMenuSettings" (contextMenuBeforeItemRender)='contextMenuBeforeItemRender($event)'>
        <e-nodes>
            <e-node id='node1' [offsetX]=150 [offsetY]=150>
                <e-node-annotations>
                    <e-node-annotation id="label1" content="Rectangle1" [horizontalAlignment]="horizontalAlignment">
                    </e-node-annotation>
                </e-node-annotations>
            </e-node>
            <e-node id='node2' [offsetX]=350 [offsetY]=150>
                <e-node-annotations>
                    <e-node-annotation id="label1" content="Rectangle2" [horizontalAlignment]="horizontalAlignment">
                    </e-node-annotation>
                </e-node-annotations>
            </e-node>
        </e-nodes>
        <e-connectors>
            <e-connector id='connector' type='Orthogonal' sourceID='node1' targetID='node2'>
            </e-connector>
        </e-connectors>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public contextMenuSettings: ContextMenuSettingsModel
    ngOnInit(): void {
        //Enables the context menu
        this.contextMenuSettings = {
          //Enables the context menu
          show: true,
          items: [{
            text: 'Cut  ', id: 'cut', target: '.e-diagramcontent',
            iconCss: 'e-Cut'
          },
          {
            text: 'Copy  ', id: 'copy', target: '.e-diagramcontent',
            iconCss: 'e-Copy'
          }],
          // Hides the default context menu items
          showCustomMenuOnly: true,
        }
    }
    public getNodeDefaults(node: NodeModel): NodeModel {
        node.height = 100;
        node.width = 100;
        node.style.fill = "#6BA5D7";
        node.style.strokeColor = "White";
        return node;
    }
    public getConnectorDefaults(obj: ConnectorModel): ConnectorModel {
        obj.style = {
            strokeColor: '#6BA5D7',
            fill: '#6BA5D7',
            strokeWidth: 2
        }
        obj.targetDecorator = {
            style: {
                fill: '#6BA5D7',
                strokeColor: '#6BA5D7'
            }
        }
        return obj;
    }
    public contextMenuBeforeItemRender(args: MenuEventArgs) {
    // To render template in li.
         let shortCutSpan: HTMLElement = createElement('span');
         let text: string = args.item.text;
         let shortCutText: string = text === 'Cut  ' ? 'Ctrl + S' : (text === 'Copy  ' ?
         'Ctrl + U' : 'Ctrl + Shift + I');
         shortCutSpan.textContent = shortCutText;
         args.element.appendChild(shortCutSpan);
         shortCutSpan.setAttribute('class', 'shortcut');
  }
}

```

{% endtab %}

## Context menu events

You would be notified with events, when you try to open the context menu items [`contextMenuOpen`](../api/diagram/diagramBeforeMenuOpenEventArgs#DiagramBeforeMenuOpenEventArgs) and when you click the menu items `contextMenuClick`.
The following code example illustrates how to define those events.

{% tab template="diagram/contextmenu/events", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation, OnInit, ViewChild } from '@angular/core';
import { DiagramComponent } from '@syncfusion/ej2-angular-diagrams';
import { ContextMenuSettingsModel,DiagramBeforeMenuOpenEventArgs, Diagram, NodeModel, ConnectorModel } from '@syncfusion/ej2-diagrams';
import { MenuEventArgs } from '@syncfusion/ej2-navigations';

@Component({
    selector: "app-container",
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" [getNodeDefaults] ='getNodeDefaults' [getConnectorDefaults]='getConnectorDefaults' [contextMenuSettings]="contextMenuSettings">
        <e-nodes>
            <e-node id='node1' [offsetX]=150 [offsetY]=150>
                <e-node-annotations>
                    <e-node-annotation id="label1" content="Rectangle1" [horizontalAlignment]="horizontalAlignment">
                    </e-node-annotation>
                </e-node-annotations>
            </e-node>
            <e-node id='node2' [offsetX]=350 [offsetY]=150>
                <e-node-annotations>
                    <e-node-annotation id="label1" content="Rectangle2" [horizontalAlignment]="horizontalAlignment">
                    </e-node-annotation>
                </e-node-annotations>
            </e-node>
        </e-nodes>
        <e-connectors>
            <e-connector id='connector' type='Orthogonal' sourceID='node1' targetID='node2'>
            </e-connector>
        </e-connectors>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public contextMenuSettings: ContextMenuSettingsModel
    ngOnInit(): void {
        //Enables the context menu
        this.contextMenuSettings = {
            //Enables the context menu
            show: true,
            items: [{
                text: 'zoom',
                id: 'zoom'
            }],
            // Hides the default context menu items
            showCustomMenuOnly: false,
            contextMenuOpen: function(args: DiagramBeforeMenuOpenEventArgs) {
                //do your custom action here.
                for (let item of args.items) {
                    if (item.text === 'delete') {
                        if (!diagram.selectedItems.nodes.length && !diagram.selectedItems.connectors.length) {
                            args.hiddenItems.push(item.text);
                        }
                    }
                }
            },
            contextMenuClick: function(args: MenuEventArgs) {
                //do your custom action here.
                if (args.item.id === 'delete') {
                    if ((diagram.selectedItems.nodes.length + diagram.selectedItems.connectors.length) > 0) {
                        diagram.cut();
                    }
                }
            }
        }
    }
    public getNodeDefaults(node: NodeModel): NodeModel {
        node.height = 100;
        node.width = 100;
        node.style.fill = "#6BA5D7";
        node.style.strokeColor = "White";
        return node;
    }
    public getConnectorDefaults(obj: ConnectorModel): ConnectorModel {
        obj.style = {
            strokeColor: '#6BA5D7',
            fill: '#6BA5D7',
            strokeWidth: 2
        }
        obj.targetDecorator = {
            style: {
                fill: '#6BA5D7',
                strokeColor: '#6BA5D7'
            }
        }
    }
}
```

{% endtab %}