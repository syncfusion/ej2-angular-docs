---
title: "Accordion Accessibility"
component: "Accordion"
description: "The Accordion control has accessibility support to access the features via keyboard, screen readers, or other assistive technology devices."
---

# Accessibility

The Accordion component has been designed keeping in mind the [WAI-ARIA](http://www.w3.org/WAI/PF/aria-practices/) specifications, by applying
 the prompt WAI-ARIA roles, states, and properties along with the keyboard support. Thus, making it usable
 for people who use assistive WAI-ARIA Accessibility supports that is achieved through the attributes like
 `aria-multiselectable`, `aria-disabled`, `aria-expanded`, `aria-selected`, and `aria-hidden`.
It helps to provides information about the elements in a document for assistive technology.
The component implements the keyboard navigation support by following the
  [WAI-ARIA practices](https://www.w3.org/TR/wai-aria-practices/) and tested in major screen readers.

## ARIA attributes

<!-- markdownlint-disable MD033 -->
| Property             | Functionality                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| role                 |<b>presentation:</b> <br/>   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;It indicates that the element is used to control presentation. This attribute is added to the Accordion element describing the actual role of the element.<br/> <b>heading:</b><br/> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;It identifies the element as a heading that serves as an Accordion header. This attribute is added to all the Accordion header elements describing the actual role of the element.<br/>  |
| aria-multiselectable | It indicates the expand mode in the Accordion. Default value of this attribute is true. If expand mode value is changed as ‘single’, the attribute value changes to `false`.                                                                                                                                                                                                                                                                                                                                                                                             |
| aria-disabled        | It indicates the disabled state of the Accordion and its items.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| aria-expanded        | It indicates the expand state of the Accordion Item. Default value of this attribute is `false`. If an item is expanded, the attribute value changes to ‘true’.                                                                                                                                                                                                                                                                                                                                                                                                            |
| aria-selected        | It indicates the Selection state of the Accordion Item. Default value of this attribute is `false`. If an item is expanded, the attribute value changes to ‘true’.                                                                                                                                                                                                                                                                                                                                                                                                         |
| aria-hidden          | It indicates the content visible state of the Accordion Item. Default value of this attribute is `true`. If an item content is visible, the attribute value changes to ‘false`.                                                                                                                                                                                                                                                                                                                                                                                           |
| aria-labelledby      | Attribute is set to content (panel) and it points to the corresponding Accordion header.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| aria-controls        | Attribute is set to the header and it points to the corresponding Accordion content.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| aria-level           | It defines the hierarchical level of an Accordion element with its inner level.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

## Keyboard interaction

Keyboard navigation is enabled by default. Possible keys are:

| Key           | Description                                                                         |
|---------------|-------------------------------------------------------------------------------------|
| <kbd>Space or Enter</kbd>    | When focus is on the Accordion header, click on the focused element makes the element to expand and collapse.                                                     |
| <kbd>Down Arrow</kbd>   | Focus the next Accordion header.                                                            |
| <kbd>Up Arrow</kbd>         | Focus the previous Accordion header. |
| <kbd>Home</kbd>           | Focus the first Accordion header.                                                                     |
| <kbd>End</kbd>   | Focus the last Accordion header.                                                |

{% tab template="accordion/accordion", isDefaultActive=true, sourceFiles="app/**/*.ts"  %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `
  <ejs-accordion>
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

}
```

{% endtab %}