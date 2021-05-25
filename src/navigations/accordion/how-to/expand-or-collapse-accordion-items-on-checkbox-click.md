---
title: "Expand and collapse accordion items on checkbox click"
component: "Accordion"
description: "This section explains how to expand and collapse accordion items on clicking the checkbox."
---

# Expand and collapse accordion items on checkbox click

By default, accordion items expand or collapse by clicking the accordion item header or clicking expand/collapse icon in accordion header.

You can also expand or collapse the accordion items through external button click. In the following example, when you change the checkbox provided then the accordion items will expand/collapse accordingly. This requirement can be achieved with the help of accordion's [`click`](../../api/accordion#click), [`expanding`](../../api/accordion#expanding) events, [`expandItem`](../../api/accordion#expanditem) public method and checkbox's [`change`](../../api/check-box#change) event.

{% tab template="accordion/accordion-checkbox", sourceFiles="app/**/*.ts,app/**/*.html,index.css" %}

```typescript

import { Component, ViewEncapsulation, Inject, ViewChild } from "@angular/core";
import {
  ExpandEventArgs,
  Accordion,
  AccordionClickArgs
} from "@syncfusion/ej2-navigations";
import { closest } from "@syncfusion/ej2-base";
import { AccordionComponent } from "@syncfusion/ej2-angular-navigations";
import { CheckBoxComponent } from "@syncfusion/ej2-angular-buttons";

@Component({
  selector: "app-container",
  templateUrl: "app/app.component.html"
})
export class AppComponent {
  @ViewChild("element") acrdnInstance: AccordionComponent;
  @ViewChild("checkbox1") chk1Instance: CheckBoxComponent;
  @ViewChild("checkbox2") chk2Instance: CheckBoxComponent;
  @ViewChild("checkbox3") chk3Instance: CheckBoxComponent;
  public clickEventArgs: Event;
  public expanding(e: ExpandEventArgs) {
    if (this.clickEventArgs) {
      let header = closest(
        this.clickEventArgs.target as Element,
        ".e-acrdn-header"
      );
      let checkboxEle = closest(
        this.clickEventArgs.target as Element,
        ".e-checkbox-wrapper"
      );
      if (header && !checkboxEle) {
        e.cancel = true;
        return;
      }
    }
    let index = this.acrdnInstance.items.indexOf(e.item);
    if (index == 0 && !this.chk1Instance.checked) {
      e.cancel = true;
      return;
    }
    if (index == 1 && !this.chk2Instance.checked) {
      e.cancel = true;
      return;
    }
    if (index == 2 && !this.chk3Instance.checked) {
      e.cancel = true;
      return;
    }
  }
  public onClick(e) {
    this.clickEventArgs = e.originalEvent;
  }
  public changeHandler1() {
    this.clickEventArgs = null;
    this.acrdnInstance.expandItem(true, 0);
  }
  public changeHandler2() {
    this.clickEventArgs = null;
    this.acrdnInstance.expandItem(true, 1);
  }
  public changeHandler3() {
    this.clickEventArgs = null;
    this.acrdnInstance.expandItem(true, 2);
  }
}
```

{% endtab %}
