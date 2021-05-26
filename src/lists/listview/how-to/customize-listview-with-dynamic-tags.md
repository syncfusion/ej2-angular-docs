# Customize ListView with dynamic tags

You can customize the ListView items using the
[`template`](../../api/list-view#template) property. Here,
the dynamic tags are added and removed in the list item from another ListView. Refer to the following steps to achieve this.

* Initialize dynamic ListView with required property that holds the tags of parent ListView, and bind the
[`select`](../../api/list-view#select) event
(triggers when the list item is selected), in which you can get and add the selected item value as tags into parent
ListView. Refer to the following code sample.

```typescript

//Select the event that is is rendered inside dialog for ListView
addTag(e) {
    let listTag = document.createElement('span');
    listTag.className = 'advanced-option';
    let labelElem = document.createElement('span');
    labelElem.className = 'label';
    let deleteElem = document.createElement('span');
    deleteElem.className = 'delete';
    deleteElem.onclick = this.removeTag;
    labelElem.innerHTML = e.text;
    listTag.appendChild(labelElem);
    listTag.appendChild(deleteElem);
    let tag = document.createElement('span');
    tag.className = 'advanced-option-list';
    tag.appendChild(listTag);
    this.listviewInstance.element.querySelector('.e-active').appendChild(tag);
}

```

* Render the dialog component with empty content and append the created dynamic ListView object to the dialog on
[`created`](../../api/dialog#created) event.

* Bind the click event for button icon (+) to update the ListView data source with tags, and open the dialog with this
dynamic ListView. Refer to the following code sample.

```typescript

//Method to hide/show the dialog and update the ListView data source
renderDialog(id) {
    if (document.getElementsByClassName('e-popup-open').length != 0) {
        this.dialog.hide();
    }
    else {
        this.listObj.dataSource = this.datasource[id];
        this.listObj.dataBind();
        this.dialog.show();
    }

}

```

* Bind the click event with added dynamic tags to remove it. Refer to the following code sample.

```typescript

//Method to remove the list item
removeTag() {
    this.parentNode.parentNode.remove();
}

```

{% tab template="listview/dynamic-tag", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript

import { Component, ViewChild } from '@angular/core';
import{ListViewComponent} from "@syncfusion/ej2-angular-lists";
import{DialogComponent} from "@syncfusion/ej2-angular-popups";
@Component({
    selector: 'my-app',
    template: `<div id="sample">
    <ejs-listview #list id='templatelist' [dataSource]='data' [fields]='fields' width=350 >
    <ng-template  #template let-data="">
    <div><span class="templatetext">{{data.Name}} </span> <span class="designationstyle"><button ejs-button id="{{data.Id}}" class="e-but" iconCss='e-icons e-add-icon' cssClass='e-small e-round' (click)='onClick($event)'></button></span></div>
    </ng-template>
    </ejs-listview>
   <ejs-dialog id='dialog' #ejDialog width='200px' [animationSettings]='animation' [visible]='false' showCloseIcon='true' [position]='position'>
      <ng-template #content>
        <ejs-listview #List id="list" showHeader=true headerTitle='Favorite' width='200px' [dataSource]='datasource.Brooke' [fields]='fields' (select)='addTag($event)'></ejs-listview>
      </ng-template>
      </ejs-dialog>
    </div>`
})

export class AppComponent {
    @ViewChild('list') listviewInstance: ListViewComponent;
    @ViewChild('List') listObj: ListViewComponent;
    @ViewChild('ejDialog') dialog: DialogComponent;
    //define the array of string
public data: string[] =  [{ "Id": "Brooke", "Name": "Brooke" },
{ "Id": "Claire", "Name": "Claire" },
{ "Id": "Erik", "Name": "Erik" },
{ "Id": "Grace", "Name": "Grace" },
{ "Id": "Jacob", "Name": "Jacob" }];

public fields: Object = {text: "Name"};
public position: Object;
public animation: Object = {effect: 'None'};
public parentNode:HTMLElement;

public brookeTag : Object = [{ "id": "list11", "Name": "Discover Music" },
{ "id": "list12", "Name": "Sales and Events" },
{ "id": "list13", "Name": "Categories" },
{ "id": "list14", "Name": "MP3 Albums" },
{ "id": "list15", "Name": "More in Music" },
];

public claireTag : Object = [{ "id": "list21", "Name": "Songs" },
{ "id": "list22", "Name": "Bestselling Albums" },
{ "id": "list23", "Name": "New Releases" },
{ "id": "list24", "Name": "Bestselling Songs" },
];

public erikTag : Object = [{ "id": "list31", "Name": "Artwork" },
{ "id": "list32", "Name": "Abstract" },
{ "id": "list33", "Name": "Acrylic Mediums" },
{ "id": "list34", "Name": "Creative Acrylic" },
{ "id": "list35", "Name": "Canvas Art" }
];

public graceTag : Object = [{ "id": "list41", "Name": "Rock" },
{ "id": "list42", "Name": "Gospel" },
{ "id": "list43", "Name": "Latin Music" },
{ "id": "list44", "Name": "Jazz" },
];

public jacobTag: Object = [{ "id": "list51", "Name": "100 Albums" },
{ "id": "list52", "Name": "Hip-Hop and R&B Sale" },
{ "id": "list53", "Name": "CD Deals" }
];

public datasource: any = { "Brooke": this.brookeTag, "Claire": this.claireTag, "Erik": this.erikTag, "Grace": this.graceTag, "Jacob": this.jacobTag };

ngAfterViewChecked(){
setTimeout(()=>{
  this.position =  { X: document.querySelector('.e-add-icon').getBoundingClientRect().left + 50, Y: document.querySelector('.e-add-icon').getBoundingClientRect().top - 5 };
},1000);
}
onClick(e){
  this.renderDialog(e.currentTarget.id);
}
renderDialog(id) {
    if (document.getElementsByClassName('e-popup-open').length != 0) {
        this.dialog.hide();
    }
    else {
        this.listObj.dataSource = this.datasource[id];
        this.listObj.dataBind();
        this.dialog.show();
    }

}
addTag(e) {
    let listTag = document.createElement('span');
    listTag.className = 'advanced-option';
    let labelElem = document.createElement('span');
    labelElem.className = 'label';
    let deleteElem = document.createElement('span');
    deleteElem.className = 'delete';
    deleteElem.onclick = this.removeTag;
    labelElem.innerHTML = e.text;
    listTag.appendChild(labelElem);
    listTag.appendChild(deleteElem);
    let tag = document.createElement('span');
    tag.className = 'advanced-option-list';
    tag.appendChild(listTag);
    this.listviewInstance.element.querySelector('.e-active').appendChild(tag);
}
removeTag() {
    this.parentNode.remove();
}
}
```

{% endtab %}
