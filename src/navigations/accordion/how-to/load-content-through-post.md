---
title: "Load content through Ajax"
component: "Accordion"
description: "This example demonstrates how to load the external content into the Essential JS 2 Accordion content through Ajax post."
---

# Load content through Ajax

Accordion supports to load external contents through `AJAX` library. Refer the below steps.

* Import the `Ajax` module from `ej2-base` and initialize with URL path.

* Get data from the Ajax `Success` event to initialize Accordion with retrieved external path data.

{% tab template="accordion/accordion-ajax" , sourceFiles="app/**/*.ts,ajax.html"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { Ajax } from '@syncfusion/ej2-base';
import { AccordionComponent} from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-container',
    template: `
    <div id="acrdnContnet1" style="display:none">
        <ul style="margin : 0px;padding:0px 16px; list-style-type: none">
          <li>Testing</li>
          <li>Development</li>
        </ul>
    </div>
    <div id="acrdnContnet2" style="display:none">
      <ul style="margin : 0px;padding:0px 16px; list-style-type: none">
        <li>Mobile</li>
        <li>Web</li>
      </ul>
    </div>
    <ejs-accordion #acrdnInstance>
      <e-accordionitems>
        <e-accordionitem header='Department' content = '#acrdnContnet1'></e-accordionitem>
        <e-accordionitem header='Platform' content = '#acrdnContnet2'></e-accordionitem>
        <e-accordionitem header='Employee Details'></e-accordionitem>
      </e-accordionitems>
    </ejs-accordion>
        `
})

export class AppComponent {
    @ViewChild('acrdnInstance') acrdnInstance: AccordionComponent;
    public contentData: string;

    ngOnInit() {
    let ajax: Ajax = new Ajax('./ajax.html', 'GET', true);
    ajax.send().then();
    ajax.onSuccess = (data: string): void => {
       this.acrdnInstance.items[2].content = data;
       this.acrdnInstance.refresh();
    };
    }
}}
```

{% endtab %}