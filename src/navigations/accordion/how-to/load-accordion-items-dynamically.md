---
title: "Load accordion items dynamically"
component: "Accordion"
description: "This example demonstrates how to dynamically load or add an accordion item in the Essential JS 2 Accordion control."
---

# Load accordion items dynamically

Accordion items can be added dynamically by passing the item and index value with the [`addItem`](../../api/accordion#additem) method.

In the following demo, you can add the accordion content by expanding any accordion header content using
[`expanded`](../../api/accordion#expanded) event.

* Data is fetched from the data source.

* The data is formatted as a JSON object with [`header`](../../api/accordion/accordionItem#header)
and [`content`](../../api/accordion/accordionItem#content) fields.

* Here last index is calculated to append the new accordion at the end.

{% tab template="accordion/accordion-items-dynamically", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { AccordionComponent } from '@syncfusion/ej2-angular-navigations';
import { Accordion, ExpandEventArgs, AccordionClickArgs, AccordionItemModel } from '@syncfusion/ej2-navigations';
import { accordion } from './datasource.ts';

let dbFlag: number = 0;
let dynamciAcrdnCount: number = 2;
@Component({
    selector: 'app-container',
    template: `
            <ejs-accordion #element (expanded)="expanded($event)">
        <e-accordionitems>
          <e-accordionitem expanded='true'>
            <ng-template #header>
              <div>ASP.NET</div>
            </ng-template>
            <ng-template #content>
              <div>Microsoft ASP.NET is a set of technologies in the Microsoft .NET Framework for building Web applications and XML Web
                services. ASP.NET pages execute on the server and generate markup such as HTML, WML, or XML that is sent to a desktop
                or mobile browser. ASP.NET pages use a compiled,event-driven programming model that improves performance and enables
                the separation of application logic and user interface.</div>
            </ng-template>
          </e-accordionitem>
          <e-accordionitem>
            <ng-template #header>
              <div>ASP.NET MVC</div>
            </ng-template>
            <ng-template #content>
              <div>The Model-View-Controller (MVC) architectural pattern separates an application into three main components: the model,
                the view, and the controller. The ASP.NET MVC framework provides an alternative to the ASP.NET Web Forms pattern for
                creating Web applications. The ASP.NET MVC framework is a lightweight, highly testable presentation framework that
                (as with Web Forms-based applications) is integrated with existing ASP.NET features, such as master pages and membership-based
                authentication.
              </div>
            </ng-template>
          </e-accordionitem>
        </e-accordionitems>
    </ejs-accordion>
        `
})

export class AppComponent {
    @ViewChild('element') acrdnInstance: AccordionComponent;
    public expanded(e: ExpandEventArgs) {
         let Elementindex = document.getElementsByClassName("e-expand-state e-selected e-active")[0];
         if([].slice.call(e.element.parentElement.children).indexOf(e.element) == [].slice.call(e.element.parentElement.children).indexOf(Elementindex)) {
            let array: AccordionItemModel[] = accordion as AccordionItemModel[];
            for(let i: number = 0 ; i < dynamciAcrdnCount; i++)
            {
            if (dbFlag === array.length) {
                return; }
            this.acrdnInstance.addItem( array[dbFlag] , this.acrdnInstance.items.length );
            ++dbFlag;
            }
         }
    }
    ngAfterViewInit() {
    }
}

```

{% endtab %}
