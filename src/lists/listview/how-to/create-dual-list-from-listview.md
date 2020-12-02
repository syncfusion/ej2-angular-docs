# Create Dual List from ListView

The dual list contains two ListView. This allows you to move list items from one list to another using the client-side
events. This section explains how to integrate the ListView component to achieve dual list.

## Use cases

* Stock exchanges of two different countries
* Job applications (skill sets)

## Integration of Dual List

Here, two ListView components have been used to display the list items. An ej2-button is used to transfer data between
the ListView, and a textbox is used to achieve the UI of filtering support.

The dual list supports:

* Moving whole data from one list to another.
* Moving selected data from one list to another.
* Filtering the list by using a client-side typed character.

In the ListView component, sorting is enabled using the
[sortOrder](../../api/list-view#sortorder) property, and
the [select](../../api/list-view#select) event is triggered
while selecting an item. Here, the select event is triggered to enable and disable button states.

## Manipulating data

## Moving whole data from the first list to the second list(>>)

* Here, the whole data can be moved from the first ListView to the second by clicking the first button. When clicking the button,
the whole list items are sliced, and `concat` with the second ListView. This button is enabled only when the data source
of the first ListView is not empty.

## Moving whole data from the second list to the first list(<<)

* The functionality of the second button is the same as above, and data is transferred from the second list to the first
list. This button is enabled only when the data source of the second ListView is not empty.

## Moving selected item from one list to another list (>) and (<)

* The [Select](../../api/list-view#select) event is triggered
when selecting a list item in the ListView. The selected items can be transferred between two lists. These buttons will be
enabled when selecting an item in lists.

## Filtering method

* The filtering method is used to filter list items when typing a character in the text box. In this
method, the [`dataManager`](https://ej2.syncfusion.com/angular/documentation/data/getting-started) has been
used to fetch data from the data source and display in ListView.

## Sorting

* By using the dual list, list items can be sorted in the ListView component using the
[sortOrder](../../api/list-view#sortorder) property.
You can enable sorting in one ListView; in the same order, data can be transferred to another ListView.

{% tab template="listview/dual-list", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from "@angular/core";
import { enableRipple } from "@syncfusion/ej2-base";
import { DataManager, Query, ODataV4Adaptor } from "@syncfusion/ej2-data";
import { ListViewComponent } from "@syncfusion/ej2-angular-lists";
import { ButtonComponent } from "@syncfusion/ej2-angular-buttons"
enableRipple(true);

@Component({
    selector: 'my-app',
    template: `<div id="text1">
            <input #textbox class="e-input" type="text" id="firstInput" placeholder="Filter" title="Type in a name" (keyup)="onFirstKeyUp($event)" />
              </div>
            <ejs-listview #list1 id='list-1' [dataSource]='firstListData' [fields]='fields' [sortOrder]='Ascending'  (select)="onFirstListSelect()"></ejs-listview>
             <div id="btn">
             <button ejs-button #btn1 id="firstBtn" (click)="firstbtnclick()"> >> </button>
             <button ejs-button #btn2 id="secondBtn" [disabled]=true (click)="secondbtnclick()"> > </button>
             <button ejs-button #btn3 id="thirdBtn" [disabled]=true (click)="thirdbtnclick()"> < </button>
             <button ejs-button #btn4 id="fourthBtn" (click)="fourthbtnclick()"> << </button>
             </div>

            <div id="text2">
            <input #text class="e-input" type="text" id="secondInput" placeholder="Filter" title="Type in a name" (keyup)="onSecondKeyUp($event)" />
            </div>
            <ejs-listview #list2 id='list-2' [dataSource]='secondListData' [fields]='fields' [sortOrder]='Ascending' (select)="onSecondListSelect()"></ejs-listview>
        `,
})

export class AppComponent {
  public fields: Object;
  public firstListData:any; secondListData: any;
  constructor(){
   this.firstListData  = [
  { text: "Hennessey Venom", id: "list-01" },
  { text: "Bugatti Chiron", id: "list-02" },
  { text: "Bugatti Veyron Super Sport", id: "list-03" },
  { text: "SSC Ultimate Aero", id: "list-04" },
  { text: "Koenigsegg CCR", id: "list-05" },
  { text: "McLaren F1", id: "list-06" }
];

   this.secondListData = [
    { text: 'Aston Martin One- 77', id: 'list-07' },
    { text: 'Jaguar XJ220', id: 'list-08' },
    { text: 'McLaren P1', id: 'list-09' },
    { text: 'Ferrari LaFerrari', id: 'list-10' },
  ];

 this.fields = { text: "text", id: "id" };
  }
    @ViewChild('list1')firstListObj: ListViewComponent;
    @ViewChild('list2')secondListObj: ListViewComponent;
    @ViewChild('btn1')firstBtnObj: ButtonComponent;
    @ViewChild('btn2')secondBtnObj: ButtonComponent;
    @ViewChild('btn3')thirdBtnObj: ButtonComponent;
    @ViewChild('btn4')fourthBtnObj: ButtonComponent;
    @ViewChild('textbox')textboxEle: any;
    @ViewChild('text')textEle: any;
    ngAfterViewInit(){
        this.firstListData = this.firstListObj.dataSource.slice();
        this.secondListData = this.secondListObj.dataSource.slice();
    }
       //Here, all list items are moved to the second list on clicking move all button
    firstbtnclick() {
        this.secondListObj.dataSource = Array.prototype.concat.call(this.firstListObj.dataSource, this.secondListObj.dataSource);
        this.updateFirstListData();
        this.firstListObj.removeMultipleItems(this.firstListObj.liCollection);
        this.firstListData = this.firstListData.concat(this.firstListObj.dataSource);
        this.secondListData = this.secondListObj.dataSource.slice();
        this.firstBtnObj.disabled = true;
        this.onFirstKeyUp();
        this.setButtonState();
    }

    //Here, the selected list items are moved to the second list on clicking move button
  secondbtnclick() {
        let e = this.firstListObj.getSelectedItems();
        this.secondListObj.dataSource = Array.prototype.concat.call(this.secondListObj.dataSource, e.data);
        this.firstListObj.removeItem(e.item);
        this.firstListData = this.firstListObj.dataSource;
        this.secondListData = this.secondListObj.dataSource.slice();
        this.onFirstKeyUp();
        this.secondBtnObj.disabled = true;
        this.setButtonState();
    }

    //Here, the selected list items are moved to the first list on clicking move button
   thirdbtnclick () {
        let e = this.secondListObj.getSelectedItems();
        this.firstListObj.dataSource = Array.prototype.concat.call(this.firstListObj.dataSource, e.data);
        this.secondListObj.removeItem(e.item);
        this.secondListData = this.secondListObj.dataSource;
        this.firstListData = this.firstListObj.dataSource.slice();
        this.onSecondKeyUp();
        this.thirdBtnObj.disabled = true;
        this.setButtonState();

    }

    //Here, all list items are moved to the first list on clicking move all button
   fourthbtnclick() {
        this.firstListObj.dataSource = Array.prototype.concat.call(this.firstListObj.dataSource, this.secondListObj.dataSource);
        this.updateSecondListData();
        this.secondListObj.removeMultipleItems(this.secondListObj.liCollection);
        this.secondListData = this.secondListData.concat(this.secondListObj.dataSource);
        this.firstListData = this.firstListObj.dataSource.slice();
        this.onSecondKeyUp();
        this.setButtonState();

    }

    //Here, the ListView data source is updated to the first list
    updateFirstListData() {
        Array.prototype.forEach.call(this.firstListObj.liCollection, (list) => {
            this.firstListData.forEach((data, index) => {
                if (list.innerText.trim() === data.text) {
                    delete this.firstListData[index];
                }
            });
        });
        this.textboxEle.nativeElement.value= '';
        let ds = [];
        this.firstListData.forEach((data) => {
            ds.push(data);
        })
        this.firstListData = ds;

    }

    //Here, the ListView dataSource is updated for the second list
    updateSecondListData() {
        Array.prototype.forEach.call(this.secondListObj.liCollection, (list) => {
            this.secondListData.forEach((data, index) => {
                if (list.innerText.trim() === data.text) {
                    delete this.secondListData[index];
                }
            });

        });
        this.textEle.nativeElement.value = '';
        let ds = [];
        this.secondListData.forEach((data) => {
            ds.push(data);
        })
        this.secondListData = ds;

    }
    onFirstListSelect() {
        this.secondBtnObj.disabled = false;
    }
    onSecondListSelect() {
        this.thirdBtnObj.disabled = false;
    }

    //Here, filtering is handled using the dataManager for the first list
    onFirstKeyUp(e) {
        let value = this.textboxEle.nativeElement.value;
        let data = new DataManager(this.firstListData).executeLocal(new Query().where('text', 'startswith', value, true));
        if (!value) {
            this.firstListObj.dataSource = this.firstListData.slice();
        } else {
            this.firstListObj.dataSource = data;
        }
    }
    //Here, filtering is handled using the dataManager for the second list
     onSecondKeyUp(e) {
        let value =this.textEle.nativeElement.value;
        let data = new DataManager(this.secondListData).executeLocal(new Query().where('text', 'startswith', value, true));
        if (!value) {
            this.secondListObj.dataSource = this.secondListData.slice();
        } else {
            this.secondListObj.dataSource = data;
        }
    }

    //Here, the state of the button is changed
    setButtonState() {
        if (this.firstListObj.dataSource.length) {
            this.firstBtnObj.disabled = false;
        } else {
            this.firstBtnObj.disabled = true;
            this.secondBtnObj.disabled = true;
        }

        if (this.secondListObj.dataSource.length) {
            this.fourthBtnObj.disabled = false;
        } else {
            this.fourthBtnObj.disabled = true;
            this.thirdBtnObj.disabled = true;
        }

    }
}
```

{% endtab %}
