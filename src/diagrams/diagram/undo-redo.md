---
title: "Undo and redo"
component: "Diagram"
description: "Undo and redo provides support to reverse and restore the performed changes."
---

# History List

Diagram tracks the history of actions that are performed after initializing the diagram and provides support to reverse and restore those changes.

## Undo and redo

Diagram provides built-in support to track the changes that are made through interaction and through public APIs. The changes can be reverted or restored either through shortcut keys or through commands.

>Note: If you want to use Undo-Redo in diagram, you need to inject UndoRedo in the diagram.

## Undo/redo through shortcut keys

Undo/redo commands can be executed through shortcut keys. Shortcut key for undo is Ctrl+z and shortcut key for redo is Ctrl+y.

## Undo/redo through public APIs

The client-side methods [`undo`](../api/diagram) and [`redo`](../api/diagram) help you to revert/restore the changes. The following code example illustrates how to undo/redo the changes through script.

```typescript
@Component({
  selector: "app-container",
  // Diagram template
  template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px"  (created)='created($event)'>
      </ejs-diagram>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public created(args: Object): void {
        // Reverts the last action performed
        this.diagram.undo();
        // Restores the last undone action
        this.diagram.redo();
    }
}
```

When a change in the diagram is reverted or restored (undo/redo), the historyChange event gets triggered.

### Group multiple changes

History list allows to revert or restore multiple changes through a single undo/redo command. For example, revert/restore the fill color change of multiple elements at a time.

The client-side method [`startGroupAction`](../api/diagram) is used to notify the diagram to start grouping the changes. The client-side method [`endGroupAction`](../api/diagram) is used to notify to stop grouping the changes. The following code illustrates how to undo/redo fillColor change of multiple elements at a time.

{% tab template="diagram/undoRedo/groupAction", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { DiagramComponent, Diagram, NodeModel } from "@syncfusion/ej2-angular-diagrams";
@Component({
    selector: "app-container",
    template: `<ejs-diagram  #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]='getNodeDefaults' (created)='created($event)'>
        <e-nodes>
            <e-node id='node1' [offsetX]=150 [offsetY]=150>
            </e-node>
        </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public getNodeDefaults(node: NodeModel): NodeModel {
        node.height =  100;
        node.width =  100;
        node.style.fill =  '#6BA5D7';
        node.style.strokeColor =  'white';
        return  node;
    };
    public created(args: Object): void {
        //Start to group the changes
        this.diagram.startGroupAction();
        //Makes the changes
        let color: string[] = ['black', 'red', 'green', 'yellow'];
        for (var i = 0; i < color.length; i++) {
            // Updates the fillColor for all the child elements.
            this.diagram.nodes[0].style.fill = color[i];
            this.diagram.dataBind();
        }
        //Ends grouping the changes
        this.diagram.endGroupAction();
    }
}

```

{% endtab %}

### Track custom changes

Diagram provides options to track the changes that are made to custom properties. For example, in case of an employee relationship diagram, track the changes in the employee information. The historyList of the diagram enables you to track such changes.
The following example illustrates how to track such custom property changes.

Before changing the employee information, save the existing information to historyList by using the client-side method push of historyList.
The historyList canLog method can be used which takes a history entry as argument and returns whether the specific entry can be added or not.

The following code example illustrates how to save the existing property values.

```typescript
@Component({
    selector: "app-container",
    // render initialized Diagram
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px"  (created)='create($event)'>
        </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public created(args: Object): void {
        //Creates a custom entry
        let entry: HistoryEntry = {
            undoObject: this.diagram.nodes[0];
        };
        // adds the history to history list
        this.diagram.historyList.push(entry);
        this.diagram.dataBind();
    }
}
```

## canLog

canLog in the history list, which takes a history entry as argument and returns whether the specific entry can be added or not.

{% tab template="diagram/undoRedo/canLog", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { DiagramComponent, Diagram, NodeModel, HistoryEntry } from "@syncfusion/ej2-angular-diagrams";
@Component({
    selector: "app-container",
    template: `<ejs-diagram  #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]='getNodeDefaults' (created)='created($event)'>
        <e-nodes>
            <e-node id='node1' [offsetX]=150 [offsetY]=150>
            </e-node>
        </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  @ViewChild("diagram")
    public diagram: DiagramComponent;
    public getNodeDefaults(node: NodeModel): NodeModel {
        node.height =  100;
        node.width =  100;
        node.style.fill =  '#6BA5D7';
        node.style.strokeColor =  'white';
        return  node;
    };
    public created(args: Object): void {
        // canLog decide whether the entry add or not in history List
        this.diagram.historyList.canLog = function(entry: HistoryEntry) {
            entry.cancel = true;
            return entry;
        }
    }
}
```

{% endtab %}

### Track undo/redo actions

The historyList undoStack property is used to get the collection of undo actions which should be performed in the diagram.
The undoStack/redoStack is the read-only property.

```typescript
@Component({
    selector: "app-container",
    // render initialized Diagram
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px">
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    //get the collection of undoStack objects
    public undoStack: HistoryEntry[] = this.diagram.historyList.undoStack;
    //get the collection of redoStack objects
    public redoStack: HistoryEntry[] = this.diagram.historyList.redoStack;
}
```

## History change event

The [`historyChange`](../api/diagram) event triggers, whenever the interaction of the node and connector is take place.

```typescript
@Component({
    selector: "app-container",
    // render initialized Diagram
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" (created)='create($event)'>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public created(args: Object): void {
        // history change event
        this.diagram.historyChange = (arg: IHistoryChangeArgs) => {
            //causes of history change
            let cause: string = arg.cause;
        }
    }
}
```

## Stack limit

The [`stackLimit`](../api/diagram) property of history manager is used to limits the number of actions to be stored on the history manager.
{% tab template="diagram/undoRedo/canLog", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from "@angular/core";
import { DiagramComponent, Diagram, NodeModel, HistoryEntry } from "@syncfusion/ej2-angular-diagrams";
@Component({
    selector: "app-container",
    template: `<ejs-diagram  #diagram id="diagram" width="100%" height="580px" [getNodeDefaults]='getNodeDefaults' (created)='created($event)'>
        <e-nodes>
            <e-node id='node1' [offsetX]=150 [offsetY]=150>
            </e-node>
        </e-nodes>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  @ViewChild("diagram")
    public diagram: DiagramComponent;
    public getNodeDefaults(node: NodeModel): NodeModel {
        node.height =  100;
        node.width =  100;
        node.style.fill =  '#6BA5D7';
        node.style.strokeColor =  'white';
        return  node;
    };
    public created(args: Object): void {
        // canLog decide whether the entry add or not in history List
        this.diagram.historyManager.stackLimit =3;
    }
}
```

{% endtab %}

## Retain selection

You can retain a selection at undo/redo operation by using the client-side API Method called `updateSelection`.  Using this method, we can select a diagram objects.

```typescript
@Component({
    selector: "app-container",
    // render initialized Diagram
    template: `<ejs-diagram #diagram id="diagram" width="100%" height="580px" (created)='create($event)'>
    </ejs-diagram>`,
    encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    @ViewChild("diagram")
    public diagram: DiagramComponent;
    public created(args: Object): void {
        // history change event
        this.diagram.updateSelection: (object: NodeModel, diagram: Diagram) => {
                    let selArr = [];
                    selArr.push(object)
                    diagram.select(selArr);
                },
    }
}
```