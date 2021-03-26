---
title: "Immutable"
component: "TreeGrid"
description: "Learn how to use immutable data in the Essential JS 2 Tree Grid control. Also learn about the limitations of this feature."
---

# Immutable Mode

The immutable mode optimizes the Tree Grid re-rendering performance by using the object reference and [`deep compare`](https://dmitripavlutin.com/how-to-compare-objects-in-javascript/#4-deep-equality) concept. When performing the Tree Grid actions, it will only re-render the modified or newly added rows and prevent the re-rendering of the unchanged rows.

To enable this feature, you have to set the [`enableImmutableMode`](../api/treegrid#enableimmutablemode) property as **true**.

>* This feature uses the primary key value for data comparison. So, you need to provide the [`isPrimaryKey`](../api/treegrid/column/#isprimarykey) column.

{% tab template="treegrid/immutable", sourceFiles="app/app.component.ts,app/app.template.html,app/app.module.ts,app/main.ts" %}

```typescript
import { Component, ViewChild } from "@angular/core";
import { ButtonComponent } from "@syncfusion/ej2-angular-buttons";
import { sampleData2, dataSource1, sampleData } from "./datasource";

@Component({
    selector: 'app-container',
    templateUrl: 'app/app.template.html'
})
export class AppComponent implements OnInit {
  public data: Object[] = [];
  public pageSettings: Object = { pageSize: 50 };
  public editSettings: Object = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Cell' };
  public selectionOptions: Object = { type: 'Multiple' };
  public immutableStart: number;
  public normalStart: number;
  @ViewChild("immutable")
  public immutableGrid: GridComponent;
  @ViewChild("normal")
  public normalGrid: GridComponent;
  @ViewChild("addtop")
  public addtop: ButtonComponent;
  @ViewChild("addbottom")
  public addbottom: ButtonComponent;
  @ViewChild("delete")
  public delete: ButtonComponent;
  @ViewChild("reverse")
  public reverse: ButtonComponent;
  @ViewChild("paging")
  public paging: ButtonComponent;
  public immutableInit: boolean = true;
  public init: boolean = true;

  ngOnInit(): void {
    dataSource1();
    this.data = sampleData2;
  }

  immutableBeforeDataBound(): void {
    this.immutableStart = new Date().getTime();
  }

  immutableDataBound(): void {
    let val: number | string = this.immutableInit ? '' : new Date().getTime() - this.immutableStart;
    document.getElementById("immutableDelete").innerHTML =
      "Immutable rendering Time: " + "<b>" + val + "</b>" + "<b>ms</b>";
    this.immutableStart = 0; this.immutableInit = false;
  }

  normalBeforeDataBound(): void {
    this.normalStart = new Date().getTime();
  }

  normalDataBound(): void {
    let val: number = this.init ? '' : new Date().getTime() - this.normalStart;
    document.getElementById("normalDelete").innerHTML =
      "Normal rendering Time: " + "<b>" + val + "</b>" + "<b>ms</b>";
    this.normalStart = 0; this.init = false;
  }

  addTopEvent(): void {
    this.normalGrid.addRecord(sampleData[0], 0, "Top");
    this.immutableGrid.addRecord(sampleData[0], 0, "Top");
  }

  addBottomEvent(): void {
    this.normalGrid.addRecord(sampleData[0], 0, "Bottom");
    this.immutableGrid.addRecord(sampleData[0], 0, "Bottom");
  }

  deleteEvent(): void {
    this.normalGrid.selectRows([0, 2, 4]);
    this.immutableGrid.selectRows([0, 2, 4]);
    this.normalGrid.deleteRecord();
    this.immutableGrid.deleteRecord();
  }

  sortEvent(): void {
    let aData: object[] = (this.immutableGrid.dataSource as object[]).reverse();
    this.normalGrid.setProperties({ dataSource: aData });
    this.immutableGrid.setProperties({ dataSource: aData });
  }

  pageEvent(): void {
    let page: number = this.normalGrid.pageSettings.currentPage + 1;
    this.normalGrid.goToPage(page);
    this.immutableGrid.goToPage(page);
  }
}

```

{% endtab %}

## Limitations

The following features are not supported in the immutable mode:

* Frozen rows and columns
* Row Template
* Detail Template
* Column reorder
* Virtualization
