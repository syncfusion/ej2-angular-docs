---
title: "Symbol Palette"
component: "Diagram"
description: "The symbol palette displays a collection of palettes which shows a set of nodes and connectors."
---

# Symbol Palette

The **SymbolPalette** displays a collection of palettes. The palette shows a set of nodes and connectors. It allows to drag and drop the nodes and connectors into the diagram.

## Create symbol palette

The [`width`](../api/diagram/palette#width-number) and [`height`](../api/diagram/palette#height-number) properties of the symbol palette allows to define the size of the symbol palette.

```typescript
@Component({
    selector: "app-container",
    template: `<ejs-symbolpalette id="symbolpalette"width="100%" height="700px">
    </ejs-symbolpalette>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {}
```

## Add palettes to SymbolPalette

A palette allows to display a group of related symbols and it textually annotates the group with its header.
A [`Palettes`](../api/diagram/palette#palettes-PaletteModel[]) can be added as a collection of symbol groups.

The collection of predefined symbols can be added in palettes using the [`symbols`](../api/diagram/palette#symbols-[]) property.

To initialize a palette, define a JSON object with the property [`ID`](../api/diagram/palette#id-string) that is unique ID is set to the palettes.

The [`allowDrag`](../api/symbol-palette#allowdrag) property allows the user to drag the symbol from the symbol palette.

The following code example illustrates how to define a palette and how its added to symbol palette.

{% tab template="diagram/symbolpalette/palettes", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { SymbolPaletteComponent, SymbolPalette, NodeModel, ConnectorModel, PaletteModel } from '@syncfusion/ej2-angular-diagrams';
import { ExpandMode } from '@syncfusion/ej2-navigations';

@Component({
    selector: "app-container",
    template: `<ejs-symbolpalette id="symbolpalette"width="100%" height="700px" [expandMode]="expandMode" [palettes]="palettes" [symbolHeight]=80 [symbolWidth]=80>
    </ejs-symbolpalette>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public expandMode: ExpandMode;
    public palettes: PaletteModel[];
    public getBasicShapes(): NodeModel[] {
        let basicShapes: NodeModel[] = [{
                id: 'Rectangle',
                shape: {
                    type: 'Basic',
                    shape: 'Rectangle'
                }
            },
            {
                id: 'Ellipse',
                shape: {
                    type: 'Basic',
                    shape: 'Ellipse'
                }
            },
            {
                id: 'Hexagon',
                shape: {
                    type: 'Basic',
                    shape: 'Hexagon'
                }
            }
        ];
        return basicShapes;
    };
    public getFlowShapes(): NodeModel[] {
        let flowShapes: NodeModel[] = [{
                id: 'process',
                shape: {
                    type: 'Flow',
                    shape: 'Process'
                }
            },
            {
                id: 'document',
                shape: {
                    type: 'Flow',
                    shape: 'Document'
                }
            },
            {
                id: 'predefinedprocess',
                shape: {
                    type: 'Flow',
                    shape: 'PreDefinedProcess'
                }
            }
        ];
        return flowShapes;
    };
    public getConnectors(): ConnectorModel[] {
        let connectorSymbols: ConnectorModel[] = [{
                id: 'Link1',
                type: 'Orthogonal',
                sourcePoint: {
                    x: 0,
                    y: 0
                },
                targetPoint: {
                    x: 40,
                    y: 40
                },
                targetDecorator: {
                    shape: 'Arrow'
                }
            },
            {
                id: 'Link21',
                type: 'Straight',
                sourcePoint: {
                    x: 0,
                    y: 0
                },
                targetPoint: {
                    x: 40,
                    y: 40
                },
                targetDecorator: {
                    shape: 'Arrow'
                }
            },
            {
                id: 'link33',
                type: 'Bezier',
                sourcePoint: {
                    x: 0,
                    y: 0
                },
                targetPoint: {
                    x: 40,
                    y: 40
                },
                style: {
                    strokeWidth: 2
                },
                targetDecorator: {
                    shape: 'None'
                }
            }
        ];
        return connectorSymbols;
    };
    ngOnInit(): void {
        this.expandMode = 'Multiple'
        this.palettes = [{
                //Sets the id of the palette
                id: 'flow',
                //Sets whether the palette expands/collapse its children
                expanded: true,
                //Adds the palette items to palette
                symbols: this.getFlowShapes(),
                //Sets the header text of the palette
                title: 'Flow Shapes',
                iconCss: 'e-ddb-icons e-flow'
            },
            {
                id: 'basic',
                expanded: true,
                symbols: this.getBasicShapes(),
                title: 'Basic Shapes',
                iconCss: 'e-ddb-icons e-basic'
            },
            {
                id: 'connectors',
                expanded: true,
                symbols: this.getConnectors(),
                title: 'Connectors',
                iconCss: 'e-ddb-icons e-connector'
            }
        ]
    }
}
```

{% endtab %}

## Customize the palette header

Palettes can be annotated with its header texts.

The [`title`](../api/diagram/palette#title-string) displayed as the header text of palette.

The [`expanded`](../api/diagram/palette#expanded-boolean) property of palette allows to expand/collapse its palette items.

The [`height`](../api/diagram/palette#height-number) property of palette sets the height of the symbol group.

The [`iconCss`](../api/diagram/palette#iconCss-string) property sets the content of the symbol group.

The [`description`](../api/diagram/symbolDescription#description) defines the text to be displayed and how that is to be handled in `getSymbolInfo`.

Also, any HTML element into a palette header can be embedded by defining the getSymbolInfo property.
The following code example illustrates how to customize palette headers.

{% tab template= "diagram/symbolpalette/paletteheader", es5Template="es5description" %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { SymbolPaletteComponent, SymbolPalette, NodeModel, ConnectorModel,  PaletteModel } from '@syncfusion/ej2-angular-diagrams';
import { ExpandMode } from '@syncfusion/ej2-navigations';

@Component({
    selector: "app-container",
    template: `<ejs-symbolpalette id="symbolpalette"width="100%" height="700px" [expandMode]="expandMode" [palettes]="palettes" [symbolHeight]=80 [symbolWidth]=80>
    </ejs-symbolpalette>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public expandMode: ExpandMode;
    public palettes: PaletteModel[];
    public getBasicShapes(): NodeModel[] {
        let basicShapes: NodeModel[] = [{
                id: 'Rectangle',
                shape: {
                    type: 'Basic',
                    shape: 'Rectangle'
                }
            },
            {
                id: 'Ellipse',
                shape: {
                    type: 'Basic',
                    shape: 'Ellipse'
                }
            },
            {
                id: 'Hexagon',
                shape: {
                    type: 'Basic',
                    shape: 'Hexagon'
                }
            }
        ];
        return basicShapes;
    };
    public getFlowShapes(): NodeModel[] {
        let flowShapes: NodeModel[] = [{
                id: 'process',
                shape: {
                    type: 'Flow',
                    shape: 'Process'
                }
            },
            {
                id: 'document',
                shape: {
                    type: 'Flow',
                    shape: 'Document'
                }
            },
            {
                id: 'predefinedprocess',
                shape: {
                    type: 'Flow',
                    shape: 'PreDefinedProcess'
                }
            }
        ];
        return flowShapes;
    };
    public getConnectors(): ConnectorModel[] {
        let connectorSymbols: ConnectorModel[] = [{
                id: 'Link1',
                type: 'Orthogonal',
                sourcePoint: {
                    x: 0,
                    y: 0
                },
                targetPoint: {
                    x: 40,
                    y: 40
                },
                targetDecorator: {
                    shape: 'Arrow'
                }
            },
            {
                id: 'Link21',
                type: 'Straight',
                sourcePoint: {
                    x: 0,
                    y: 0
                },
                targetPoint: {
                    x: 40,
                    y: 40
                },
                targetDecorator: {
                    shape: 'Arrow'
                }
            },
            {
                id: 'link33',
                type: 'Bezier',
                sourcePoint: {
                    x: 0,
                    y: 0
                },
                targetPoint: {
                    x: 40,
                    y: 40
                },
                style: {
                    strokeWidth: 2
                },
                targetDecorator: {
                    shape: 'None'
                }
            }
        ];
        return connectorSymbols;
    };
    ngOnInit(): void {
        this.expandMode = 'Multiple'
        this.palettes = [{
                //Sets the id of the palette
                id: 'flow',
                //Sets whether the palette expands/collapse its children
                expanded: true,
                //Adds the palette items to palette
                symbols: this.getFlowShapes(),
                //Sets the header text of the palette
                title: 'Flow Shapes',
                iconCss: 'e-ddb-icons e-flow'
            },
            {
                id: 'basic',
                expanded: true,
                symbols: this.getBasicShapes(),
                title: 'Basic Shapes',
                iconCss: 'e-ddb-icons e-basic'
            },
            {
                id: 'connectors',
                expanded: true,
                symbols: this.getConnectors(),
                title: 'Connectors',
                iconCss: 'e-ddb-icons e-connector'
            }
        ]
    }
}
```

{% endtab %}

## Restrict expansion of the palette panel

The symbol palette panel can be restricted from getting expanded. The `cancel` argument of the `paletteExpanding` property defines whether the palette's panel should be expanded or collapsed. By default, the panel is expanded. This restriction can be done for each of the palettes in the symbol palette as desired.
In the following code example, the basic shapes palette is restricted from getting collapsed whereas the swimlane shapes palette can be expanded or collapsed.

{% tab template="diagram/symbolpalette/restrictexpand", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import {  NodeModel,  PaletteModel, SymbolPreviewModel } from '@syncfusion/ej2-angular-diagrams';
import { ExpandMode } from '@syncfusion/ej2-navigations';

@Component({
    selector: "app-container",
    template: `<ejs-symbolpalette id="symbolpalette"width="100%" height="100%" [expandMode]="expandMode" [enableSearch]=true [palettes]='palettes'
     [symbolHeight]=80 [symbolWidth]=80 [symbolPreview]='symbolPreview' (paletteExpanding)='paletteExpanding($event)'>
    </ejs-symbolpalette>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public expandMode: ExpandMode;
    public palettes: PaletteModel[];
    public symbolPreview: SymbolPreviewModel[];
    public paletteExpanding(args) {
        if(args.palette.id === 'basic') {
            // Basic shapes panel does not collapse
            args.cancel = true;
            } else {
            // Swimlane shapes panel collapse and expand
            args.cancel = false;
            }
      };
    public expandMode: ExpandMode;
    public getBasicShapes(): NodeModel[] {
        let basicShapes: NodeModel[] = [{
                id: 'Rectangle',
                shape: {
                    type: 'Basic',
                    shape: 'Rectangle'
                }
            },
            {
                id: 'Ellipse',
                shape: {
                    type: 'Basic',
                    shape: 'Ellipse'
                }
            },
            {
                id: 'Hexagon',
                shape: {
                    type: 'Basic',
                    shape: 'Hexagon'
                }
            }
        ];
        return basicShapes;
    };
    public getFlowShapes(): NodeModel[] {
        let flowShapes: NodeModel[] = [{
                id: 'process',
                shape: {
                    type: 'Flow',
                    shape: 'Process'
                }
            },
            {
                id: 'document',
                shape: {
                    type: 'Flow',
                    shape: 'Document'
                }
            }
        ];
        return flowShapes;
    };

    ngOnInit(): void {
        this.expandMode = 'Multiple'
        this.palettes = [{
                //Sets the id of the palette
                id: 'flow',
                //Sets whether the palette expands/collapse its children
                expanded: true,
                //Adds the palette items to palette
                symbols: this.getFlowShapes(),
                //Sets the header text of the palette
                title: 'Flow Shapes',
                iconCss: 'e-ddb-icons e-flow'
            },
            {
                id: 'basic',
                expanded: true,
                symbols: this.getBasicShapes(),
                title: 'Basic Shapes',
                iconCss: 'e-ddb-icons e-basic'
            }
        ],
        this.symbolPreview = [{
          height: 100,
          width: 100
        }]
    }
}

```

{% endtab %}

## Stretch the symbols into the palette

The [`fit`](../api/diagram/symbolInfo#fit-boolean) property defines whether the symbol has to be fit inside the size, that is defined by the symbol palette. For example, when you resize the rectangle in the symbol, ratio of the rectangle size has to be maintained rather changing into square shape. The following code example illustrates how to customize the symbol size.

{% tab template="diagram/symbolpalette/fit", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { SymbolPaletteComponent, SymbolPalette, NodeModel, ConnectorModel, PaletteModel } from '@syncfusion/ej2-angular-diagrams';
import { ExpandMode } from '@syncfusion/ej2-navigations';

@Component({
    selector: "app-container",
    template: `<ejs-symbolpalette id="symbolpalette"width="100%" height="700px" [symbolHeight]=80 [symbolWidth]=80 [expandMode]="expandMode" [palettes]="palettes" [getSymbolInfo]="getSymbolInfo">
    </ejs-symbolpalette>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public expandMode: ExpandMode;
    public palettes: PaletteModel[];
    public getBasicShapes(): NodeModel[] {
        let basicShapes: NodeModel[] = [{
                id: 'Rectangle',
                shape: {
                    type: 'Basic',
                    shape: 'Rectangle'
                }
            },
            {
                id: 'Ellipse',
                shape: {
                    type: 'Basic',
                    shape: 'Ellipse'
                }
            },
            {
                id: 'Hexagon',
                shape: {
                    type: 'Basic',
                    shape: 'Hexagon'
                }
            }
        ];
        return basicShapes;
    };
    public getSymbolInfo(symbol) {
        // Enables to fit the content into the specified palette item size
        return {
            fit: true
        };
        // When it is set as false, the element is rendered with actual node size
    };
    ngOnInit(): void {
        this.expandMode = 'Multiple'
        this.palettes = [{
            id: 'basic',
            expanded: true,
            symbols: this.getBasicShapes(),
            title: 'Basic Shapes',
            iconCss: 'e-ddb-icons e-basic'
        }]
    }
}
```

{% endtab %}

## Add/Remove symbols to palette at runtime

* Symbols can be added to palette at runtime by using public method, [`addPaletteItem`](https://ej2.syncfusion.com/angular/documentation/api/symbol-palette/#addpaletteitem).

* Symbols can be removed from palette at runtime by using public method, [`removePaletteItem`](https://ej2.syncfusion.com/angular/documentation/api/symbol-palette/#removepaletteitem).

## Customize the size of symbols

The size of the individual symbol can be customized. The [`symbolWidth`](../api/diagram/symbolPaletteModel/#symbolwidth) and  [`symbolHeight`](../api/diagram/symbolPaletteModel/#symbolheight) properties of node enables you to define the size of the symbols. The following code example illustrates how to change the size of a symbol.

{% tab template="diagram/symbolpalette/size", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
import { SymbolPaletteComponent, SymbolPalette, NodeModel, MarginModel, PaletteModel } from '@syncfusion/ej2-angular-diagrams';
import { ExpandMode } from '@syncfusion/ej2-navigations';

@Component({
    selector: "app-container",
    template: `<ejs-symbolpalette id="symbolpalette"width="100%" height="700px" [symbolHeight]=80 [symbolWidth]=80 [expandMode]="expandMode" [palettes]="palettes" [symbolMargin]="symbolMargin">
    </ejs-symbolpalette>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public expandMode: ExpandMode;
    public palettes: PaletteModel[];
    public symbolMargin: MarginModel;
    public getBasicShapes(): NodeModel[] {
        let basicShapes: NodeModel[] = [{
                id: 'Rectangle',
                shape: {
                    type: 'Basic',
                    shape: 'Rectangle'
                }
            },
            {
                id: 'Ellipse',
                shape: {
                    type: 'Basic',
                    shape: 'Ellipse'
                }
            },
            {
                id: 'Hexagon',
                shape: {
                    type: 'Basic',
                    shape: 'Hexagon'
                }
            }
        ];
        return basicShapes;
    };
    ngOnInit(): void {
        this.expandMode = 'Multiple'
        this.palettes = [{
            id: 'basic',
            expanded: true,
            symbols: this.getBasicShapes(),
            title: 'Basic Shapes',
            iconCss: 'e-ddb-icons e-basic'
        }]
        //Sets the space to be left around a symbol
        this.symbolMargin = {
            left: 15,
            right: 15,
            top: 15,
            bottom: 15
        }
    }
}
```

{% endtab %}

The [`symbolMargin`](../api/diagram/symbolPaletteModel/#symbolmargin) property is used to create the space around
elements, outside of any defined borders.

## Symbol preview

The symbol preview size of the palette items can be customized using [`symbolPreview`](../api/diagram/symbolPreview).
The [`width`](../api/diagram/symbolPreview#width-number) and [`height`](../api/diagram/symbolPreview#height-number) properties of SymbolPalette enables you to define the preview size to all the symbol palette items.
The [`offset`](../api/diagram/symbolPreview#offset-PointModel) of the dragging helper relative to the mouse cursor.

The following code example illustrates how to change the preview size of a palette item.

{% tab template="diagram/symbolpalette/fit", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
 import { SymbolPaletteComponent, SymbolPalette, SymbolPreviewModel, NodeModel, ConnectorModel, PaletteModel } from '@syncfusion/ej2-angular-diagrams';
import { ExpandMode } from '@syncfusion/ej2-navigations';

@Component({
    selector: "app-container",
    template: `<ejs-symbolpalette id="symbolpalette"width="100%" height="700px" [symbolHeight]=80 [symbolWidth]=80 [expandMode]="expandMode" [palettes]="palettes" [getSymbolInfo]="getSymbolInfo" [symbolMargin]="symbolMargin" [symbolPreview]="symbolPreview">
    </ejs-symbolpalette>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public expandMode: ExpandMode;
    public palettes: PaletteModel[];
    public symbolMargin: MarginModel;
    public symbolPreview: SymbolPreviewModel;
    public getBasicShapes(): NodeModel[] {
        let basicShapes: NodeModel[] = [{
                id: 'Rectangle',
                shape: {
                    type: 'Basic',
                    shape: 'Rectangle'
                }
            },
            {
                id: 'Ellipse',
                shape: {
                    type: 'Basic',
                    shape: 'Ellipse'
                }
            },
            {
                id: 'Hexagon',
                shape: {
                    type: 'Basic',
                    shape: 'Hexagon'
                }
            }
        ];
        return basicShapes;
    };
    public getSymbolInfo(symbol) {
        // Enables to fit the content into the specified palette item size
        return {
            fit: true
        };
        // When it is set as false, the element is rendered with actual node size
    };
    ngOnInit(): void {
        this.expandMode = 'Multiple'
        this.palettes = [{
            id: 'basic',
            expanded: true,
            symbols: this.getBasicShapes(),
            title: 'Basic Shapes',
            iconCss: 'e-ddb-icons e-basic'
        }],
        this.symbolMargin = {
            left: 15,
            right: 15,
            top: 15,
            bottom: 15
        },
        //Specifies the preview size and position to symbol palette items.
        this.symbolPreview = {
            height: 100,
            width: 100,
            offset: {
                x: 0.5,
                y: 0.5
            }
        }
    }
}
```

{% endtab %}

## Default settings

While adding more number of symbols such as nodes and connectors to the palette, define the default settings for those objects through the [`getNodeDefaults`](../api/diagram/symbolPaletteModel/#getnodedefaults) and the [`getConnectorDefaults`](../api/diagram/symbolPaletteModel/#getconnectordefaults) properties of diagram allows to define the default settings for nodes and connectors.

{% tab template="diagram/symbolpalette/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, OnInit, ViewEncapsulation, ViewChild } from '@angular/core';
 import { SymbolPaletteComponent, SymbolPalette, SymbolPreviewModel, NodeModel, ConnectorModel, PaletteModel } from '@syncfusion/ej2-angular-diagrams';
import { ExpandMode } from '@syncfusion/ej2-navigations';

@Component({
    selector: "app-container",
    template: `<ejs-symbolpalette id="symbolpalette"width="100%" height="700px" [symbolHeight]=80 [symbolWidth]=80 [expandMode]="expandMode" [palettes]="palettes" [getSymbolInfo]="getSymbolInfo" [symbolMargin]="symbolMargin" [symbolPreview]="symbolPreview" [getNodeDefaults]="">
    </ejs-symbolpalette>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public expandMode: ExpandMode;
    public palettes: PaletteModel[];
    public symbolMargin: MarginModel;
    public symbolPreview: SymbolPreviewModel;
    public getBasicShapes(): NodeModel[] {
        let basicShapes: NodeModel[] = [{
                id: 'Rectangle',
                shape: {
                    type: 'Basic',
                    shape: 'Rectangle'
                }
            },
            {
                id: 'Ellipse',
                shape: {
                    type: 'Basic',
                    shape: 'Ellipse'
                }
            },
            {
                id: 'Hexagon',
                shape: {
                    type: 'Basic',
                    shape: 'Hexagon'
                }
            }
        ];
        return basicShapes;
    };
    public getPaletteNodeDefaults(node: NodeModel): void {
        node.width = 100;
        node.height = 100;
        node.style.strokeColor = '#3A3A3A';
    }
    public getSymbolInfo(symbol) {
        // Enables to fit the content into the specified palette item size
        return {
            fit: true
        };
        // When it is set as false, the element is rendered with actual node size
    };
    ngOnInit(): void {
        this.expandMode = 'Multiple'
        this.palettes = [{
            id: 'basic',
            expanded: true,
            symbols: this.getBasicShapes(),
            title: 'Basic Shapes',
            iconCss: 'e-ddb-icons e-basic'
        }],
        this.symbolMargin = {
            left: 15,
            right: 15,
            top: 15,
            bottom: 15
        },
        //Specifies the preview size and position to symbol palette items.
        this.symbolPreview = {
            height: 100,
            width: 100,
            offset: {
                x: 0.5,
                y: 0.5
            }
        }
    }
}
```

{% endtab %}

## Adding symbol description for symbols in the palette

The diagram provides support to add symbol description below each symbol of a palette. This descriptive representation of each symbol will enhance the details of the symbol visually. The height and width of the symbol description can also be set individually.
* The property `getSymbolInfo`, can be used to add the symbol description at runtime.
 The following code is an example to set a symbol description for symbols in the palette.

{% tab template="diagram/symbolpalette/symboldesc", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import {  NodeModel,  PaletteModel, SymbolPreviewModel } from '@syncfusion/ej2-angular-diagrams';
import { ExpandMode } from '@syncfusion/ej2-navigations';

@Component({
    selector: "app-container",
    template: `<ejs-symbolpalette id="symbolpalette"width="100%" height="100%" [expandMode]="expandMode" [enableSearch]=true [palettes]='palettes'
     [symbolHeight]=80 [symbolWidth]=80 [symbolPreview]='symbolPreview' [getSymbolInfo]='getSymbolInfo'>
    </ejs-symbolpalette>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public expandMode: ExpandMode;
    public palettes: PaletteModel[];
    public symbolPreview: SymbolPreviewModel[];
    public getSymbolInfo(symbol) {
    //Defines the symbol description
      return { width: 75, height: 40, description: { text: symbol.shape['shape'] } }
    };
    public expandMode: ExpandMode;
    public getBasicShapes(): NodeModel[] {
        let basicShapes: NodeModel[] = [{
                id: 'Rectangle',
                shape: {
                    type: 'Basic',
                    shape: 'Rectangle'
                }
            },
            {
                id: 'Ellipse',
                shape: {
                    type: 'Basic',
                    shape: 'Ellipse'
                }
            },
            {
                id: 'Hexagon',
                shape: {
                    type: 'Basic',
                    shape: 'Hexagon'
                }
            }
        ];
        return basicShapes;
    };
    public getFlowShapes(): NodeModel[] {
        let flowShapes: NodeModel[] = [{
                id: 'process',
                shape: {
                    type: 'Flow',
                    shape: 'Process'
                }
            },
            {
                id: 'document',
                shape: {
                    type: 'Flow',
                    shape: 'Document'
                }
            }
        ];
        return flowShapes;
    };

    ngOnInit(): void {
        this.expandMode = 'Multiple'
        this.palettes = [{
                id: 'flow',
                expanded: true,
                symbols: this.getFlowShapes(),
                title: 'Flow Shapes',
                iconCss: 'e-ddb-icons e-flow'
            },
            {
                id: 'basic',
                expanded: true,
                symbols: this.getBasicShapes(),
                title: 'Basic Shapes',
                iconCss: 'e-ddb-icons e-basic'
            }
        ],
        this.symbolPreview = [{
          height: 100,
          width: 100
        }]
    }
}

```

{% endtab %}

## Palette interaction

Palette interaction notifies the element enter, leave, and dragging of the symbols into the diagram.

## DragEnter

[`DragEnter`] [`IDragEnterEventArgs`](../api/diagram/iDragEnterEventArgs) notifies, when the element enter into the diagram from symbol palette.

## DragLeave

[`DragLeave`] [`IDragLeaveEventArgs`](../api/diagram/iDragLeaveEventArgs) notifies, when the element leaves from  the diagram.

## DragOver

[`DragOver`] [`IDragOverEventArgs`](../api/diagram/iDragOverEventArgs) notifies, when an element drag over another diagram element.

>Note: The diagram provides support to cancel the drag and drop operation from the symbol palette to the diagram when the ESC key is pressed.

## See Also

* [How to add the symbol to the diagram](./nodes)