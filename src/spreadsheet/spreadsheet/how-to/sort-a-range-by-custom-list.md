---
title: "Sort a range by custom list"
component: "Spreadsheet"
description: "Learn how to sort a range of cells by custom list."
---

# Sort a range by custom list

You can also define the sorting of cell values based on your own customized personal list. In this article, custom list is achieved using `custom sort comparer`.

In the following demo, the `Trustworthiness` column is sorted based on the custom lists `Perfect`, `Sufficient`, and `Insufficient`.

{% tab template="spreadsheet/custom-sort", sourceFiles="app/**/*.ts", isDefaultActive=true , iframeHeight="450px" %}

```javascript
import { Component, OnInit,ViewChild } from '@angular/core';
import { tradeData } from './datasource';
import { DataManager, DataUtil } from '@syncfusion/ej2-data';
import { SpreadsheetComponent, CellModel } from '@syncfusion/ej2-angular-spreadsheet';

@Component({
    selector: 'app-container',
    template: "<ejs-spreadsheet #spreadsheet (dataBound)='dataBound()' (sortComplete)='sortComplete($event)'> <e-sheets> <e-sheet> <e-ranges> <e-range [dataSource]='tradeData'></e-range></e-ranges><e-columns><e-column [width]=100></e-column><e-column [width]=120></e-column><e-column [width]=96></e-column></e-columns></e-sheet></e-sheets></ejs-spreadsheet>"
})
export class AppComponent implements OnInit {

    public tradeData: object[];
    @ViewChild('spreadsheet') public spreadsheetObj: SpreadsheetComponent;
    ngOnInit(): void {
        this.tradeData = tradeData;
    }
    dataBound(){
        if (this.spreadsheetObj.activeSheetIndex === 0) {
            this.spreadsheetObj.sort({sortDescriptors: { field: 'F',  sortComparer: this.mySortComparer }, containsHeader: true}, 'A1:H20');
        }
    };
    sortComplete (args) {
        this.spreadsheetObj.selectRange(args.range);
        // code here.
    }


mySortComparer(x: CellModel, y: CellModel): number {
// custom sort comparer to sort based on the custom list.
   let customList: string[] = ['Perfect', 'Sufficient', 'Insufficient'];
    let comparer: Function = DataUtil.fnSort('Ascending');
    return comparer(x ? customList.indexOf(x.value) : x, y ? customList.indexOf(y.value) : y);
};

}

```

{% endtab %}

## See Also

* [Filtering](./filter)
* [Sorting](./sort)
* [Hyperlink](./link)
