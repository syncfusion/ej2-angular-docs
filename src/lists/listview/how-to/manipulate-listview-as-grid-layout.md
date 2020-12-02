# Manipulate ListView as Grid Layout

In Listview, list items can be rendered in grid layout with following data manipulations.

* Add Item

* Remove Item

* Sort Items

* Filter Items

## Grid Layout

In this section, we will discuss about rendering of list items in grid layout.

* Initialize and render ListView with dataSource which will render list items in list layout.

* Now, add the below CSS to list item. This will make list items to render in grid layout

```css

#element .e-list-item {
        height: 100px;
        width: 100px;
        float: left;
}

```

In the below sample, we have rendered List items in grid layout.

{% tab template="listview/grid-layout", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
          <ejs-listview id='element' [dataSource]='data'>
          <ng-template #template let-data="">
          <img id="listImage" src="./apple.png" alt="apple" />
          </ng-template>
          </ejs-listview>
        `,
  })

export class AppComponent {
  public data = [1, 2, 3, 4, 5, 6, 7, 8, 9];
}
```

{% endtab %}

## Data manipulation

In this section, we will discuss about ListView data manipulations.

### Add Item

We can add list item using [`addItem`](../../api/list-view#additem) API. This will accept array of data as argument.

```typescript

 this.$refs.listViewInstance.addItem([{text: 'Apricot', id: '32'}]);

```

In the below sample, you can add new fruit item by clicking add button which will open dialog box with fruit name and image URL text box. After entering the item details, click the add button. This will add your new fruit item.

### Remove item

We can remove list item using [`removeItem`](../../api/list-view#removeitem) API. This will accept fields with `id` or list item element as argument.

```typescript

 this.$refs.listViewInstance.removeItem({id: '32'});

```

In the below sample, you can remove fruit by hovering the fruit item which will show delete button and click that delete button to delete that fruit from your list.

### Sort Items

Listview can be sorted either in Ascending or Descending order. To enable sorting in your ListView, set [`sortOrder`](../../api/list-view#sortorder) as `Ascending` or `Descending`.

```typescript

<ejs-listview sortOrder='Ascending'></ejs-listview>

```

We can also set sorting after component initialization.

```typescript

this.listViewInstance.sortOrder = 'Ascending'

```

In the below sample, we have sorted fruits in `Ascending` order. To sort it in descending, click on sort order icon and vice versa.

### Filter Items

Listview data can be filtered with the help of [`dataManager`](https://ej2.syncfusion.com/angular/documentation/data/getting-started). After filtering the data, update ListView [`dataSource`](../../api/list-view#datasource) with filtered data.

```typescript

let value = this.textboxEle.nativeElement.value;  //input text box value
let filteredData = new DataManager(this.listdata).executeLocal(
        new Query().where("text", "startswith", value, true)
);

listViewInstance.dataSource = filteredData;

```

In the below sample, we can filter fruit items with the help of search text box. This will filter fruit items based on your input. Here we used `startswith` of input text to filter data in DataManager.

{% tab template="listview/grid-manipulation", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript

import { Component, ViewChild, ElementRef } from '@angular/core';
import { closest, enableRipple } from '@syncfusion/ej2-base';
import { DataManager, Query } from "@syncfusion/ej2-data";
enableRipple(true);

@Component({
    selector: 'my-app',
    template: `
          <div id="sample">
        <div class="headerContainer">
            <div class="e-input-group">
                <input id="search" #searchEle class="e-input" type="text" placeholder="Search fruits" (keyup)='onKeyUp($event)'/>
                <span class="e-input-group-icon e-input-search"></span>
            </div>
            <button ejs-button id="sort" class="e-control e-btn e-small e-round e-primary e-icon-btn" (click)='sortItems($event)' title="Sort fruits" data-ripple="true">
                <span class="e-btn-icon e-icons e-sort-icon-ascending"></span>
            </button>
            <button ejs-button id="add" class="e-control e-btn e-small e-round e-primary e-icon-btn" (click)='addItem($event)' title="Add fruit" data-ripple="true">
                <span class="e-btn-icon e-icons e-add-icon"></span>
            </button>
            <ejs-dialog id="dialog" #dialogObj width='300px' [visible]='false' header='Add Fruit' showCloseIcon='true' [buttons]='addButtons'>
            <ng-template #content let-data="">
            <div id="listDialog"><div class="input_name"><label for="name">Fruit Name: </label><input id="name" class="e-input" type="text" placeholder="Enter fruit name"/></div><div><label for="imgurl">Fruit Image: </label><input id="imgurl" class="e-input" type="text" placeholder="Enter image url"/></div></div>
            </ng-template>
            </ejs-dialog>
        </div>
            <ejs-listview id='element' #listview [dataSource]='fruitsdata' sortOrder='Ascending' (actionComplete)='wireEvents()'>
            <ng-template #template let-data="">
            <div class="fruits"><div class="first"><img id="listImage" src={{data.imgUrl}} alt="fruit" /><button ejs-button class="delete e-control e-btn e-small e-round e-delete-btn e-primary e-icon-btn" data-ripple="true"><span class="e-btn-icon e-icons delete-icon"></span></button></div><div class="fruitName">{{data.text}}</div></div>
            </ng-template>
            </ejs-listview>
    </div>
        `,
  })

export class AppComponent {
  @ViewChild('listview') listViewInstance: any;
  @ViewChild('dialogObj')dialogObj: any;
  @ViewChild('searchEle')searchEle: any;
  public  fruitsdata = [
    { text: 'Date', id: '1', imgUrl: './dates.jpg' },
    { text: 'Fig', id: '2', imgUrl: './fig.jpg' },
    { text: 'Apple', id: '3', imgUrl: './apple.png' },
    { text: 'Apricot', id: '4', imgUrl: './apricot.jpg' },
    { text: 'Grape', id: '5', imgUrl: './grape.jpg' },
    { text: 'Strawberry', id: '6', imgUrl: './strawberry.jpg' },
    { text: 'Pineapple', id: '7', imgUrl: './pineapple.jpg' },
    { text: 'Melon', id: '8', imgUrl: './melon.jpg' },
    { text: 'Lemon', id: '9', imgUrl: './lemon.jpg' },
    { text: 'Cherry', id: '10', imgUrl: './cherry.jpg' },
];
public addButtons= [{
        click: this.dlgButtonClick.bind(this), buttonModel: { content: 'Add', isPrimary: true }
    }];
 wireEvents() {
    Array.prototype.forEach.call(document.getElementsByClassName('e-delete-btn'), (ele) => {
        ele.addEventListener('click', this.onDeleteBtnClick.bind(this));
    });
    },
addItem() {
    (document.getElementById("name")).value = "";
    (document.getElementById("imgurl")).value = "";
    this.dialogObj.show();
},
sortItems() {
    let ele = document.getElementById("sort").firstElementChild;
    let des = ele.classList.contains('e-sort-icon-descending') ? true : false;
    if (des) {
        ele.classList.remove('e-sort-icon-descending');
        ele.classList.add('e-sort-icon-ascending');
        this.listViewInstance.sortOrder = 'Ascending';
    } else {
        ele.classList.remove('e-sort-icon-ascending');
        ele.classList.add('e-sort-icon-descending');
        this.listViewInstance.sortOrder = 'Descending'
    }
    this.listViewInstance.dataBind();
    this.wireEvents();
},
onKeyUp(e) {
    let value = this.searchEle.nativeElement.value;
    let data = new DataManager(this.fruitsdata).executeLocal(
        new Query().where("text", "startswith", value, true)
    );
    if (!value) {
        this.listViewInstance.dataSource = this.fruitsdata.slice();
    } else {
        this.listViewInstance.dataSource = data;
        this.listViewInstance.dataBind();
    }
},
onDeleteBtnClick(e) {
    e.stopPropagation();
    let li = closest(e.currentTarget, '.e-list-item');
    let data = this.listViewInstance.findItem(li);
    this.listViewInstance.removeItem(data);
    new DataManager(this.fruitsdata).remove('id', { id: data.id });
},
 dlgButtonClick() {
    let name = (document.getElementById("name")).value;
    let url = (document.getElementById("imgurl")).value;
    let id = Math.random() * 10000;
    this.listViewInstance.addItem([{ text: name, id: id, imgUrl: url }]);
    this.fruitsdata.push({ text: name, id: id, imgUrl: url });
    this.listViewInstance.element.querySelector('[data-uid="'+ id + '"]').getElementsByClassName('e-delete-btn')[0].addEventListener('click', this.onDeleteBtnClick.bind(this));
    this.dialogObj.hide();
}
}
```

{% endtab %}
