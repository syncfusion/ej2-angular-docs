---
title: "To keep single pane open always"
component: "Accordion"
description: "This example demonstrates how to keep a single pane in an expanded state in the Essential JS 2 Accordion control."
---

# To keep single pane open always

By default, all Accordion panels are collapsible. You can customize the Accordion to keep one panel
as expanded state always. This is applicable for `Single` expand mode.

 {% tab template="accordion/accordion", sourceFiles="app/**/*.ts"    %}

```typescript
import { Component, ViewChild } from '@angular/core';
import {ExpandEventArgs, AccordionClickArgs} from '@syncfusion/ej2-navigations';

@Component({
    selector: 'app-container',
    template: `
    <ejs-accordion #element expandMode='Single' (expanding)="beforeExpand($event)" (clicked)="clicked($event)">
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
          <e-accordionitem>
            <ng-template #header>
              <div>JavaScript</div>
            </ng-template>
            <ng-template #content>
              <div>JavaScript (JS) is an interpreted computer programming language.It was originally implemented as part of web browsers
                so that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter
                the document content that was displayed.More recently, however, it has become common in both game development and
                the creation of desktop applications.</div>
            </ng-template>
          </e-accordionitem>
        </e-accordionitems>
    </ejs-accordion>
        `
})

export class AppComponent {
    @ViewChild('element') acrdnInstance: AccordionComponent;
    public clickEle: HTMLElement;
    public clicked(e: AccordionClickArgs) {
    this.clickEle = (e.originalEvent.target as Element).closest(
      '.e-acrdn-header'
    );
  }
  public beforeExpand(e: ExpandEventArgs): void {
    let expandCount: number = this.acrdnInstance.element.querySelectorAll(
      '.e-selected'
    ).length;
    let ele: Element = this.acrdnInstance.element.querySelectorAll(
      '.e-selected'
    )[0];
    if (ele) {
      ele = ele.firstChild as Element;
    }
    if (expandCount === 1 && ele === this.clickEle) {
      e.cancel = true;
    }
  }
}
```

{% endtab %}
