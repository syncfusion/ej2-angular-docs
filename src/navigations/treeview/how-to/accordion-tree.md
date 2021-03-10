# Customize the TreeView into accordion

Accordion is an interface where a list of items can be collapsed or expanded, but only one list can be collapsed or expanded at a time. You can customize the TreeView to make it behave as an accordion. Refer to the following code sample to create an accordion tree.

{% tab template="tree-view/accordion-tree", sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component, Inject, ViewChild } from '@angular/core';
import { TreeViewComponent, NodeSelectEventArgs } from '@syncfusion/ej2-angular-navigations';
/**
 * TreeView Accordion sample
 */
@Component({
    selector: 'app-container',
    template: `<div id='treeparent'><ejs-treeview id='treeElement' #treevalidate [fields]='field'  (nodeSelected)='nodeSelect($event)' [cssClass]='cssClass'></ejs-treeview></div>`
})
export class AppComponent {

   // Data source for TreeView component
   public continents: Object[] = [
       {
        code: "AF", name: "Africa", countries: [
            { code: "NGA", name: "Nigeria" },
            { code: "EGY", name: "Egypt" },
            { code: "ZAF", name: "South Africa" }
        ]
    },
    {
        code: "AS", name: "Asia", countries: [
            { code: "CHN", name: "China" },
            { code: "IND", name: "India", selected: true },
            { code: "JPN", name: "Japan" }
        ]
    },
    {
        code: "EU", name: "Europe", countries: [
            { code: "DNK", name: "Denmark" },
            { code: "FIN", name: "Finland" },
            { code: "AUT", name: "Austria",
             }
        ]
    },
    {
        code: "NA", name: "North America", countries: [
            { code: "USA", name: "United States of America" },
            { code: "CUB", name: "Cuba" },
            { code: "MEX", name: "Mexico" }
        ]
    },
    {
        code: "OC", name: "Oceania", countries: [
            { code: "AUS", name: "Australia" },
            { code: "NZL", name: "New Zealand" },
            { code: "WSM", name: "Samoa" }
        ]
    }
    ];
    public field:Object ={ dataSource: this.continents,  id: "code", text: "name", child: "countries" };
    public cssClass="accordiontree";

    @ViewChild ('treevalidate') tree: TreeViewComponent;

    public nodeSelect(args: NodeSelectEventArgs): void {
      if (args.node.classList.contains('e-level-1')) {
        this.tree.collapseAll();
        this.tree.expandAll([args.node]);
        this.tree.expandOn = 'none'
      }
    }
}

```

{% endtab %}