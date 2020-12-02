# Filter list items in the ListView

The filtered data can be displayed in the ListView component depending upon on user inputs using the [`DataManager`](https://ej2.syncfusion.com/angular/documentation/data/getting-started). Refer to the following steps to render the ListView with filtered data.

* Render a textbox to get input for filtering data.

* Render ListView with [`dataSource`](../../api/list-view#datasource), and set the [`sortOrder`](../../api/list-view#sortorder) property.

* Bind the `keyup` event for textbox to perform filtering operation. To filter list data, pass the list data source to the `DataManager`, manipulate the data using the [`executeLocal`](https://ej2.syncfusion.com/documentation/api/data/dataManager/#executelocal) method, and then update filtered data as ListView dataSource.

{% tab template="listview/getting-started", sourceFiles="app/**/*.ts,index.css", isDefaultActive=true %}

```typescript

import { Component, ViewChild } from "@angular/core";
import { enableRipple } from "@syncfusion/ej2-base";
import { DataManager, Query, ODataV4Adaptor } from "@syncfusion/ej2-data";
enableRipple(true);

@Component({
    selector: 'my-app',
    template: `<div id="sample">
            <input #textbox class="e-input" type="text" id="textbox" placeholder="Filter" title="Type in a name" (keyup)=onkeyup($event) />
            <ejs-listview #list id='list' [dataSource]='listData' [fields]='fields' [sortOrder]='Ascending'></ejs-listview>
        </div>`,
        styles: [`
        #list {
  box-shadow: 0 1px 4px #ddd;
  border-bottom: 1px solid #ddd;
}
#sample {
  height: 220px;
  margin: 0 auto;
  display: table;
}
        `]
})

export class AppComponent {
    public listData: Object = [
  { text: "Hennessey Venom", id: "list-01" },
  { text: "Bugatti Chiron", id: "list-02" },
  { text: "Bugatti Veyron Super Sport", id: "list-03" },
  { text: "SSC Ultimate Aero", id: "list-04" },
  { text: "Koenigsegg CCR", id: "list-05" },
  { text: "McLaren F1", id: "list-06" }
];

 public fields: Object = { text: "text", id: "id" };
   @ViewChild('list')
   listObj: ListViewComponent;
   @ViewChild('textbox')textboxEle: any;
    onkeyup(event){
      let value = this.textboxEle.nativeElement.value;
      let data = new DataManager(this.listData).executeLocal(new Query().where("text", "startswith", value, true));
  if (!value) {
    this.listObj.dataSource = this.listData.slice();
  } else {
    this.listObj.dataSource = data;
  }
  this.listObj.dataBind();
    }
}

```

{% endtab %}

> In this demo, data has been filtered with starting character of the list items. You can also filter list items with ending character by passing the `endswith` in [where](https://ej2.syncfusion.com/documentation/api/data/query/#where) clause instead of `startswith`.
