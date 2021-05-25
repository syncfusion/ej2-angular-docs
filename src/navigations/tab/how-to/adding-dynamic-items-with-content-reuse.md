---
title: "Tab How To sections"
component: "Tab"
description: "This example demonstrates how to add the Essential JS 2 Tabs control with angular component content reuse."
---

# Adding dynamic items with content reuse

You can add dynamic tabs with angular component content reuse using Angular **TemplateRef**.

Content reuse can be achieved by using the following steps:
1. Create a TemplateRef variable in your component(app.component.ts) file.
2. Access the TemplateRef using ViewChild on the `<ng-template>` element.
3. Provide separate TemplateRef declaration for each angular component
and pass content by dynamically adding tab. It will reuse the content of angular component.

Refer to the following sample.

{% tab template="tab/content-reuse", sourceFiles="app//*.ts,app//*.html,index.css"%}

```typescript


import { Component, ViewChild, OnInit, TemplateRef } from '@angular/core';
import { createElement } from '@syncfusion/ej2-base';
import { TabComponent, SelectEventArgs  } from '@syncfusion/ej2-angular-navigations';
import { enableRipple } from '@syncfusion/ej2-base';

enableRipple(true);

/**
 * Content reuse
 */

@Component({
  selector: 'my-app',
  templateUrl: 'app.component.html',
  styleUrls: ['app.component.css'],
})

export class AppComponent {
  @ViewChild('element') tabObj: TabComponent;
  @ViewChild('DatePickertemplateRef') public DatePickertemplate: TemplateRef<any>;
  @ViewChild('DropDowntemplateRef') public DropDowntemplate: TemplateRef<any>;

  public headerText: Object = [{ 'text': 'DatePicker' }, { 'text': 'Dropdown' }, { 'text': 'Reused Dropdown' }];

  public btnClicked(e: any): void {
    var newtabItem = [
      { header: { text: 'DynamicTabItem' }, content: this.DropDowntemplate }
    ];
    this.tabObj.addTab(newtabItem,1);
  }

  public btnClicked1(e: any): void {
    this.tabObj.removeTab(1);
  }

}



```

{% endtab %}