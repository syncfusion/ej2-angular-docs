---
title: "How To"
component: "Sidebar"
description: "Miscellaneous aspects of customizing the sidebar"
---

# Initialize the Sidebar with TreeView

The following example demonstrates how to render TreeView component inside the Sidebar with dock state and how to achieve expand and collapse the functionalities simultaneously in the sidebar and Treeview.

On collapse, the LI elements of TreeView show icons only to represent the short sign of the hidden text content. On expand, hidden text content will be set to be visible.

{% tab template="sidebar/treeview", sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component, ViewChild} from '@angular/core';
import { SidebarComponent, TreeViewComponent } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('sidebarTreeviewInstance')
    public sidebarTreeviewInstance: SidebarComponent;
    @ViewChild('treeviewInstance')
    public treeviewInstance: TreeViewComponent;
    public width: string = '290px';
    public enableDock: boolean = true;
    public dockSize:string ="44px";
    public mediaQuery: string = ('(min-width: 600px)');
    public target: string = '.main-content';
  
    public data: Object[] = [
        {
            nodeId: '01', nodeText: 'Installation', iconCss: 'icon-microchip icon',
        },
        {
            nodeId: '02', nodeText: 'Deployment', iconCss: 'icon-thumbs-up-alt icon',
        },
        {
            nodeId: '03', nodeText: 'Quick Start', iconCss: 'icon-docs icon',
        },
        {
            nodeId: '04', nodeText: 'Components', iconCss: 'icon-th icon',
            nodeChild: [
                { nodeId: '04-01', nodeText: 'Calendar', iconCss: 'icon-circle-thin icon' },
                { nodeId: '04-02', nodeText: 'DatePicker', iconCss: 'icon-circle-thin icon' },
                { nodeId: '04-03', nodeText: 'DateTimePicker', iconCss: 'icon-circle-thin icon' },
                { nodeId: '04-04', nodeText: 'DateRangePicker', iconCss: 'icon-circle-thin icon' },
                { nodeId: '04-05', nodeText: 'TimePicker', iconCss: 'icon-circle-thin icon' },
                { nodeId: '04-06', nodeText: 'SideBar', iconCss: 'icon-circle-thin icon' }
            ]
        },
        {
            nodeId: '05', nodeText: 'API Reference', iconCss: 'icon-code icon',
            nodeChild: [
                { nodeId: '05-01', nodeText: 'Calendar', iconCss: 'icon-circle-thin icon' },
                { nodeId: '05-02', nodeText: 'DatePicker', iconCss: 'icon-circle-thin icon' },
                { nodeId: '05-03', nodeText: 'DateTimePicker', iconCss: 'icon-circle-thin icon' },
                { nodeId: '05-04', nodeText: 'DateRangePicker', iconCss: 'icon-circle-thin icon' },
                { nodeId: '05-05', nodeText: 'TimePicker', iconCss: 'icon-circle-thin icon' },
                { nodeId: '05-06', nodeText: 'SideBar', iconCss: 'icon-circle-thin icon' }
            ]
        },
        {
            nodeId: '06', nodeText: 'Browser Compatibility', iconCss: 'icon-chrome icon'
        },
        {
            nodeId: '07', nodeText: 'Upgrade Packages', iconCss: 'icon-up-hand icon'
        },
        {
            nodeId: '08', nodeText: 'Release Notes', iconCss: 'icon-bookmark-empty icon'
        },
        {
            nodeId: '09', nodeText: 'FAQ', iconCss: 'icon-help-circled icon'
        },
        {
            nodeId: '10', nodeText: 'License', iconCss: 'icon-doc-text icon'
        }
    ];
    public field:Object ={ dataSource: this.data, id: 'nodeId', text: 'nodeText', child: 'nodeChild', iconCss: 'iconCss' };

    public onCreated(args: any) {
         this.sidebarTreeviewInstance.element.style.visibility = '';
    }
    public onClose(args: any) {
        this.treeviewInstance.collapseAll();
    }
    openClick() {
        if(this.sidebarTreeviewInstance.isOpen)
        {
            this.sidebarTreeviewInstance.hide();
            this.treeviewInstance.collapseAll();
        }
        else {
            this.sidebarTreeviewInstance.show();
            this.treeviewInstance.expandAll();
        }  
    }
  };


```

{% endtab %}
