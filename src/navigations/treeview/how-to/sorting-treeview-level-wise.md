# Sort the tree nodes based on levels

You can sort the TreeView nodes based on their level. When using the `sortOrder` property, the whole TreeView is sorted. When you sort a particular level, you can use the following code sample. The following code sample demonstrates how to sort the parent node alone in TreeView.

{% tab template="tree-view/sort-tree", sourceFiles="app/**/*.ts,index.css"  %}

```typescript

import { Component, Inject, ViewChild } from '@angular/core';
import { TreeViewComponent, NodeExpandEventArgs } from '@syncfusion/ej2-angular-navigations';
import { DataManager, Query } from '@syncfusion/ej2-data';
/**
 * Treeview Disable check box of parent nodes sample
 */
@Component({
    selector: 'app-container',
    template: `<div id='treeparent'><ejs-treeview id='treeElement' #treevalidate [fields]='field'  (nodeExpanding)='onNodeExpand($event)' (created)='onCreate($event)'></ejs-treeview></div>`
})
export class AppComponent {

   // Data source for TreeView component
   public Countries: Object[] = [
    { id: 1, name: 'India', hasChild: true },
    { id: 2, pid: 1, name: 'Assam' },
    { id: 3, pid: 1, name: 'Bihar' },
    { id: 4, pid: 1, name: 'Tamil Nadu' },
    { id: 6, pid: 1, name: 'Punjab' },
    { id: 7, name: 'Brazil', hasChild: true },
    { id: 8, pid: 7, name: 'Paraná' },
    { id: 9, pid: 7, name: 'Ceará' },
    { id: 10, pid: 7, name: 'Acre' },
    { id: 11, name: 'France', hasChild: true },
    { id: 12, pid: 11, name: 'Pays de la Loire' },
    { id: 13, pid: 11, name: 'Aquitaine' },
    { id: 14, pid: 11, name: 'Brittany' },
    { id: 15, pid: 11, name: 'Lorraine' },
    { id: 16, name: 'Australia', hasChild: true },
    { id: 17, pid: 16, name: 'New South Wales' },
    { id: 18, pid: 16, name: 'Victoria' },
    { id: 19, pid: 16, name: 'South Australia' },
    { id: 20, pid: 16, name: 'Western Australia' },
    { id: 21, name: 'China', hasChild: true },
    { id: 22, pid: 21, name: 'Guangzhou' },
    { id: 23, pid: 21, name: 'Shanghai' },
    { id: 24, pid: 21, name: 'Beijing' },
    { id: 25, pid: 21, name: 'Shantou' }
   ]

    public field:Object ={  dataSource: this.Countries, id: 'id', text: 'name', parentID: 'pid', hasChildren: 'hasChild' };
    public newData;
    @ViewChild ('treevalidate') tree: TreeViewComponent;

    public onNodeExpand(args: NodeExpandEventArgs): void {
        if (args.isInteracted){
            let childData =  new DataManager(this.newData).executeLocal(new Query().where(this.tree.fields.parentID, 'equal', parseInt(args.nodeData.id), false));
            this.tree.addNodes(childData, args.node,null)
        }
    }

    public onCreate(){
        this.newData = this.tree.fields.dataSource;
        // Selects the first level nodes alone
        let resultData = new DataManager(this.newData).executeLocal(new Query().where(this.tree.fields.parentID, 'equal', undefined, false));
        let name = [];
        for (let i = 0; i < resultData.length; i++){
            name.push(resultData[i][this.tree.fields.text]);
        }
        name.sort();
        let arr = [];
        for (let j = 0; j < name.length; j++) {
            let sortedData = new DataManager(this.newData).executeLocal(new Query().where(this.tree.fields.text, 'equal', name[j], false));
            let childData =  new DataManager(this.newData).executeLocal(new Query().where(this.tree.fields.parentID, 'equal', parseInt(sortedData[0][this.tree.fields.id]), false));
            arr.push(sortedData[0]);
        }
        // Renders treeview with sorted Nodes
        this.changeDataSource(arr);
        this.tree.dataBind();
    }

    public changeDataSource(data){
        this.tree.fields = {
            dataSource: data, id: 'id', text: 'name', parentID: 'pid', hasChildren: 'hasChild'
        }
    }
}

```

{% endtab %}