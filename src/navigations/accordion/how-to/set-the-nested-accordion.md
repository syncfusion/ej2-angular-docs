---
title: "Set the nested accordion"
component: "Accordion"
description: "This example demonstrates how to create an Essential JS 2 Accordion control inside another Essential JS 2 Accordion control."
---

# Set the nested Accordion

Accordion supports to render `nested` level of Accordion by using content property. You can give nested Accordion
content inside the parent Accordion content property by using `id` of nested element. The nested Accordion can be
rendered with the use of provided events, such as [`clicked`](../../api/accordion#clicked) and [`expanding`](../../api/accordion#expanding).

{% tab template="accordion/accordion", sourceFiles="app/**/*.ts"   %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { AccordionComponent } from '@syncfusion/ej2-angular-navigations';
import { ExpandEventArgs, Accordion, AccordionClickArgs} from '@syncfusion/ej2-navigations';

@Component({
    selector: 'app-container',
    template: `
     <ejs-accordion #element (expanding)="expanding($event)">
        <e-accordionitems>
          <e-accordionitem expanded='true'>
            <ng-template #header>
              <div>Video</div>
            </ng-template>
            <ng-template #content>
              <div id="nested_video"></div>
            </ng-template>
          </e-accordionitem>
          <e-accordionitem>
            <ng-template #header>
              <div>Music</div>
            </ng-template>
            <ng-template #content>
             <div id="nested_music"></div>
            </ng-template>
          </e-accordionitem>
          <e-accordionitem>
            <ng-template #header>
              <div>Images</div>
            </ng-template>
            <ng-template #content>
             <div id="nested_images"></div>
            </ng-template>
          </e-accordionitem>
        </e-accordionitems>
    </ejs-accordion>
        `
})

export class AppComponent {
    @ViewChild('element') acrdnInstance: AccordionComponent;
    public clicked(e: AccordionClickArgs) {
     let ele: HTMLElement = e.originalEvent.target;
     if (ele.querySelectorAll('.e-accordion').length > 0) {
      return;
     }
     let nestAcrdn_musNew: Accordion = new Accordion({
     items: [
      { header: 'New Track1' },
      { header: 'New Track2' }
     ]
    }, '#nested_musicNew');
    }
    public expanding(e: ExpandEventArgs) {
    if (e.isExpanded && [].indexOf.call(this.acrdnInstance.items, e.item) === 0) {
      if (e.element.querySelectorAll('.e-accordion').length > 0) {
        return;
      }
    let nestAcrdn_vid: Accordion = new Accordion({
    items: [
      { header: 'Video Track1' },
      { header: 'Video Track2' }
    ]
    }, '#nested_video');
    } else if (e.isExpanded && [].indexOf.call(this.acrdnInstance.items, e.item) === 1) {
    if (e.element.querySelectorAll('.e-accordion').length > 0) {
      return;
    }
    let nestAcrdn_mus:Accordion = new Accordion({
      clicked: this.clicked,
      items: [
        { header: 'Music Track1' },
        { header: 'Music Track2' },
        { header: 'Music New', content: '<div id="nested_musicNew"></div>' }
      ]
    }, '#nested_music');
    } else if (e.isExpanded && [].indexOf.call(this.acrdnInstance.items, e.item) === 2) {
    if (e.element.querySelectorAll('.e-accordion').length > 0) {
      return;
    }
    let nestAcrdn_img: Accordion = new Accordion({
      items: [
        { header: 'Track1' },
        { header: 'Track2' },
      ]
    }, '#nested_images');
    }
    }
    ngAfterViewInit() {
    }
}
```

{% endtab %}