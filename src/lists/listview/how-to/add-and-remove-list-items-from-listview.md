# Add and remove list items from ListView

You can add or remove list items from the ListView component using the
[`addItem`](../../api/list-view#additem#additem) and
[`removeItem`](../../api/list-view#removeitem) methods.
Refer to the following steps to add or remove a list item.

* Render the ListView with data source, and use the
[template](../../api/list-view#template) property to append the delete icon
for each list item. Also, bind the click event for the delete icon using the
[actionComplete](../../api/list-view#actioncomplete) handler.

* Render the Add Item button, and bind the click event. On the click event handler, pass data with random id to
the [`addItem`](../../api/list-view#additem) method to add a
new list item on clicking the Add Item button.

* Bind the click handler to the delete icon created in step 1. Within the click event, remove the list item by passing the
delete icon list item to
[`removeItem`](../../api/list-view#removeitem) method.

{% tab template="listview/addItem", sourceFiles="app/**/*.ts" isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<ejs-listview #list id='sample-list' [dataSource]='data' [fields]='fields' (actionComplete)='onComplete()'>
    <ng-template  #template let-data="">
    <div class='text-content'> {{data.text}} <span class = 'delete-icon'></span> </div>
    </ng-template>
    </ejs-listview>
    <button ejs-button id="btn" (click)="addItem()">Add Item</button>`,
})

export class AppComponent {
   @ViewChild('list')
   listviewInstance: ListViewComponent;
    //define the array of string
    public data: object[] =  [{ text: "Hennessey Venom", id: "1", icon: "delete-icon" },
  { text: "Bugatti Chiron", id: "2", icon: "delete-icon" },
  { text: "Bugatti Veyron Super Sport", id: "3", icon: "delete-icon" },
  { text: "Aston Martin One- 77", id: "4", icon: "delete-icon" },
  { text: "Jaguar XJ220", id: "list-5", icon: "delete-icon" },
  { text: "McLaren P1", id: "6", icon: "delete-icon" }];

public fields: Object = {text: "text", iconCss: "icon" };
deleteItem(args) {
  args.stopPropagation();
  let liItem = args.target.parentElement.parentElement;
  this.listviewInstance.removeItem(liItem);
  this.onComplete();
}
  onComplete() {
  let iconEle = document.getElementsByClassName("delete-icon");
  //Event handler to bind the click event for delete icon
  Array.from(iconEle).forEach((element) => {
    element.addEventListener("click", this.deleteItem.bind(this));
  });
}

addItem(){
  let data = {
    text: "Koenigsegg - " + (Math.random() * 1000).toFixed(0),
    id: (Math.random() * 1000).toFixed(0).toString(),
    icon: "delete-icon"
  };
  this.listviewInstance.addItem([data]);
}
}

```

{% endtab %}
