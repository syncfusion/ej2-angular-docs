---
title: "Load accordion with DataSource"
component: "Accordion"
description: "This example demonstrates how to bind any data object to accordion items in the Essential JS 2 Accordion control."
---

# Load Accordion with DataSource

You can bind any data object to Accordion items, by mapping it to [`header`](../../api/accordion/accordionItem#header)
and [`content`](../../api/accordion/accordionItem#content)&nbsp; property.

In the below demo, Data is fetched from an `OData` service using `DataManager`. The result data is formatted as a
JSON object with [`header`](../../api/accordion/accordionItem#header) and [`content`](../../api/accordion/accordionItem#content)
fields, which is set to [`items`](../../api/accordion#items) property of Accordion.

{% tab template="accordion/accordion", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { AccordionComponent } from '@syncfusion/ej2-angular-navigations';
import { DataManager, Query, ODataAdaptor, ReturnOption } from '@syncfusion/ej2-data';

const SERVICE_URI: string = 'https://js.syncfusion.com/ejServices/Wcf/Northwind.svc/Employees';

@Component({
    selector: 'app-container',
    template: `<ejs-accordion #element></ejs-accordion>`
})

export class AppComponent implements OnInit {
  @ViewChild('element') accordionObj: AccordionComponent;
  public itemsData: any = [];
  public mapping =  { header: 'FirstName', content: 'Notes' };

  public ngOnInit(): void {
    new DataManager({ url: SERVICE_URI, adaptor: new ODataAdaptor})
    .executeQuery(new Query().range(1, 4)).then((e: ReturnOption) => {
      let result: any = e.result;

      for(let i: number = 0; i < result.length; i++) {
        this.itemsData.push({ header: result[i][this.mapping.header], content: result[i][this.mapping.content] });
      }
      this.accordionObj.items = this.itemsData;
      this.accordionObj.refresh();
    });
  }
}

```

{% endtab %}
