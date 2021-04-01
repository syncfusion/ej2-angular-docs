---
title: "Model Binding"
component: "QueryBuilder"
description: "Documentation on Model binding in the Essential JS 2 QueryBuilder control."
---

# Model Binding

Model binding allows to bind properties for the components used in field, operator, and value columns. To implement model binding, assign fieldModel, operatorModel, and valueModel properties in QueryBuilder.

{% tab template="query-builder/model-binding", sourceFiles="app/app.component.ts,app/template-driven.html,app/app.module.ts,app/main.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { QueryBuilderComponent } from '@syncfusion/ej2-angular-querybuilder';
import {  RuleModel } from '@syncfusion/ej2-querybuilder';

@Component({
  selector: 'app-root',
  templateUrl: `app/template-driven.html`
})
export class AppComponent implements OnInit {
  @ViewChild('querybuilder') qryBldrObj: QueryBuilderComponent;
  public importRules: RuleModel;
  ngOnInit(): void {
    this.importRules = {
      'condition': 'and',
      'rules': [{
        'label': 'Employee ID',
        'field': 'EmployeeID',
        'type': 'number',
        'operator': 'equal',
        'value': 1001
    }]
    };
  }
}

```

{% endtab %}