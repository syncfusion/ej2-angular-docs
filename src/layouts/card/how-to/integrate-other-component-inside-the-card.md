---
title: "Integrate other component inside the card"
component: "Card"
description: "This example demonstrates how to integrate other Essential JS 2 controls inside the Essential JS 2 Card control."
---

# Integrate other component inside the card

You can integrate any component inside the card element. Here ListView component is placed inside the card for showcasing the To-Do list.

{% tab template="card/card_with_list", sourceFiles="app/**/*.ts,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ListView } from '@syncfusion/ej2-lists';

@Component({
    selector: 'app-container',
    template: `
        <div style="margin: 50px;">
            <!--element which is going to render the Card-->
            <div tabindex="0" class="e-card" id="basic">
                <div class="e-card-title">To-Do List</div>
                <div class="e-card-separator"></div>
                <div class="e-card-content">
                    <div id='element'></div>
                </div>
            </div>
        </div>       `
})

export class AppComponent {
    @ViewChild('element') element;

ngAfterViewInit () {
//define the array of JSON
let todoList: { [key: string]: Object }[] = [
    {  todoList: 'Pay Bills' },
    {  todoList: 'Call Chris' },
    {  todoList: 'Meet Andrew' },
    {  todoList: 'Visit Manager' },
    {  todoList: 'Customer Meeting' },
];

//Initialize ListView component
let listviewInstance: ListView = new ListView({
    dataSource: todoList,
    //map the appropriate columns to fields property
    fields: { text: 'todoList' },
    showCheckBox: true,
});

//Render initialized ListView
listviewInstance.appendTo("#element");
}
}
```

{% endtab %}