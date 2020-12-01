# Drag and Drop

Drag and Drop is supported through two libraries of Syncfusion Angular UI Components. Those are
[`Draggable`](https://ej2.syncfusion.com/documentation/api/base/draggable) and [`Droppable`](https://ej2.syncfusion.com/documentation/api/base/droppable). Draggable makes DOM to be
dragged using mouse or touch gestures and Droppable mark required DOM as droppable zone.

## Initializing Draggable

You can make any element draggable by passing the element to Draggable constructor. Refer
the following code snippet to enable draggable for DOM element

 {% tab template="common/draggable-default" sourceFiles="app/**/*.ts,index.html" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { Draggable } from  '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template:` <div id='container'>
    <div #ele class='element'><p class='drag'>Draggable Element </p></div>
    </div> `
})

export class AppComponent {

@ViewChild('ele',{static: false})element:any;

    ngAfterViewInit() {
        let draggable:Draggable =
        new Draggable(this.element.nativeElement,{clone: false});
    }
}

 ```

 {% endtab %}

## Creating Droppable zone

You can convert any DOM element as a droppable zone, which accepts the draggable elements. Refer the following code snippet to enable droppable zone.

{% tab template="common/droppable-default" sourceFiles="app/**/*.ts,index.html" %}

 ```typescript
import { Component, ViewChild } from '@angular/core';
import { Droppable } from  '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template:` <div id='container'>
    <div #droppable class='droppable'><p class='drop'>Drop target </p></div>
    </div> `
})

export class AppComponent {
    @ViewChild('droppable',{static: false})element: any ;

    ngAfterViewInit() {
        let droppable: Droppable = new Droppable(document.getElementById('droppable'));
     }
}

```

 {% endtab %}

## Defining Drop Action

To define drop action set [`drop`](https://ej2.syncfusion.com/documentation/api/base/droppable#drop) callback function during droppable object
creation. You can get details of dropped element through dropped element property in event argument.
Refer the following  code snippet to use basic drag and drop action

{% tab template="common/drag-drop-action" sourceFiles="app/**/*.ts,index.html" %}

 ```typescript
 import { Component, ViewChild } from '@angular/core';
 import { Draggable, Droppable, DropEventArgs } from '@syncfusion/ej2-base';

 @Component({
    selector: 'app-root',
    template:` <div id='container'>
    <div id='droppable'><p class='drop'>Drop target </p></div>
    <div id='draggable'><p class='drag'>Draggable Element </p></div>
    </div> `
})

export class AppComponent {
    @ViewChild('droppable',{static: false})element: any;
    @ViewChild('draggable',{static: false})element1: any;

    ngAfterViewInit() {
        let draggable: Draggable = new Draggable(document.getElementById('draggable'), {clone: false});
        let droppable: Droppable = new Droppable(document.getElementById('droppable'), {
            drop: (e: DropEventArgs) => {
                e.droppedElement.querySelector('.drag').textContent = 'Dropped';
            }
        });
    }
}
 ```

 {% endtab %}