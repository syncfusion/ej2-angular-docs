
# Drag and Drop list items

In ListView component, we don't have  drag and drop support. But we can achieve this requirement using [`TreeView`](https://ej2.syncfusion.com/angular/documentation/treeview/getting-started) component with ListView appearance.

Drag and Drop in TreeView component was enabled by setting [`allowDragAndDrop`](../../api/treeview#allowdraganddrop) to `true`.

```typescript

<ejs-treeview id='element' [fields]='fields' allowDragAndDrop='true'></ejs-treeview>

```

The TreeView component is used to represent hierarchical data in a tree like structure. So, list items in TreeView can be dropped to child of target element. we can prevent this behaviour by cancelling the [`nodeDragStop`](../../api/treeview#nodedragstop) and [`nodeDragging`](../../api/treeview#nodedragging) events.

```typescript

<ejs-treeview id='element' [fields]='fields' allowDragAndDrop='true' (nodeDragging)='onDragStop($event)' (nodeDragStop)='onDragStop($event)'></ejs-treeview>

fields= { dataSource: this.data, id: 'id', text: 'text' },

onDragStop(args) {
    //Block the Child Drop operation in TreeView
   let  draggingItem = document.getElementsByClassName("e-drop-in");
    if (draggingItem.length == 1) {
        draggingItem[0].classList.add('e-no-drop');
        args.cancel = true;
    }
}

```

In the below sample, we have rendered draggable list items.

{% tab template="listview/reorder", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
          <div id="sample">
    <ejs-treeview id='element' [fields]='fields' allowDragAndDrop='true' (nodeDragging)='onDragStop($event)' (nodeDragStop)='onDragStop($event)'></ejs-treeview>
   </div>
        `,
  })

export class AppComponent {

  public data=[
    { text: 'Hennessey Venom', id: 'list-01' },
    { text: 'Bugatti Chiron', id: 'list-02' },
    { text: 'Bugatti Veyron Super Sport', id: 'list-03' },
    { text: 'SSC Ultimate Aero', id: 'list-04' },
    { text: 'Koenigsegg CCR', id: 'list-05' },
    { text: 'McLaren F1', id: 'list-06' },
    { text: 'Aston Martin One- 77', id: 'list-07' },
    { text: 'Jaguar XJ220', id: 'list-08' },
    { text: 'McLaren P1', id: 'list-09' },
    { text: 'Ferrari LaFerrari', id: 'list-10' },
];

public fields = { dataSource: this.data, id: 'id', text: 'text' };

onDragStop(args) {
    //Block the Child Drop operation in TreeView
    let draggingItem = document.getElementsByClassName("e-drop-in");
    if (draggingItem.length == 1) {
        draggingItem[0].classList.add('e-no-drop');
        args.cancel = true;
    }
}
}
```

{% endtab %}
