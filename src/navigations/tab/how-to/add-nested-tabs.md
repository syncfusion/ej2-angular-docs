---
title: "Add nested Tabs"
component: "Tab"
description: "This example demonstrates how to create the Essential JS 2 Tab control inside another Essential JS 2 Tab control."
---

# Add nested Tabs

Tab supports to render the nested level of Tabs by using [`content`](../../api/tab/tabItemDirective#content) property.
You can add the nested Tab element inside the parent Tab [`content`](../../api/tab/tabItemDirective#content) property.
To render the nested Tab, initialize the component using the id of Tab from [`selected`](../../api/tab#selected) event handler.

{% tab template="tab/basic", sourceFiles="app/**/*.ts,index.css,datasource.ts"%}

```typescript

import { Component, OnInit } from '@angular/core';
import { isNullOrUndefined as isNOU } from '@syncfusion/ej2-base';
import { Tab, TabComponent, SelectEventArgs } from '@syncfusion/ej2-angular-navigations';
import { nested_tab_items, usa_items, france_items, australia_items } from '../datasource.ts';

/**
 * Add nested Tabs
 */

@Component({
    selector: 'app-container',
    template: `
        <ejs-tab id="element" #tab [items]='tabItems' (created)='handleCreatedEvent($event)' (selected)='handleSelectEvent($event)'>
        </ejs-tab>`
})
export class AppComponent implements OnInit {
    public tabItems: Object[];
    public usaItems: Object[];
    public franceItems: Object[];
    public australiaItems: Object[];

    public ngOnInit(): void {
        this.tabItems = nested_tab_items;
        this.usaItems = usa_items;
        this.franceItems = france_items;
        this.australiaItems = australia_items;
    }

    public handleCreatedEvent(): void {
      if (isNOU(document.querySelector('#usa_tab.e-tab'))) {
       let usa_obj: Tab = new Tab({
        items: this.usaItems
       });
       usa_obj.appendTo('#usa_tab');
    }
  }

    public handleSelectEvent(e: SelectEventArgs): void {
        if (e.selectedIndex === 1 && isNOU(document.querySelector('#france_tab.e-tab'))) {
            let france_obj: Tab = new Tab({
                items: this.franceItems
            });
            france_obj.appendTo('#france_tab');
        } else if (e.selectedIndex === 2 && isNOU(document.querySelector('#australia_tab.e-tab'))) {
            let australia_obj: Tab = new Tab({
                items: this.australiaItems
            });
            australia_obj.appendTo('#australia_tab');
        }
    }
}

```

{% endtab %}
