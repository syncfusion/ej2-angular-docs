---
title: "Templates"
component: "QueryBuilder"
description: "Documentation on templates in the Essential JS 2 QueryBuilder control."
---

# Templates

Templates allows users to define customized header and own user interface for columns.

## Header Template

Header Template allows to define your own user interface for Header, which includes creating or deleting rules and groups and to customize the AND/OR condition and NOT condition options. To implement header template you can create the user interface using `ngTemplate` and  assign the values when requestType is header-template-create in `actionBegin` event.

The `#headerTemplate` template variable identifies the NgTemplate content as the header.

In the following sample dropdown, splitbutton and button are used as the custom components in the header.

{% tab template="query-builder/header-template", sourceFiles="app/app.component.ts,app/template-driven.html,app/app.module.ts,app/main.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { QueryBuilderComponent } from '@syncfusion/ej2-angular-querybuilder';
import { ActionEventArgs, RuleModel } from '@syncfusion/ej2-querybuilder';
import { ItemModel, MenuEventArgs } from '@syncfusion/ej2-splitbuttons';
import { closest } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  templateUrl: `app/template-driven.html`
})

export class AppComponent implements OnInit {
  @ViewChild('querybuilder') qryBldrObj: QueryBuilderComponent;
  public ds: { [key: string]: Object}[] = [{'key': 'AND', 'value': 'and'},{'key': 'OR', 'value': 'or'}];
  public ddbitems: ItemModel[];
  public importRules: RuleModel;
  public actionArgs: ActionEventArgs;
  public deleteGroupBtn: Element;
  public fields: Object;
  ngOnInit(): void {
    this.importRules = {
      'condition': 'and', 'not': true,
      'rules': [{
        'label': 'Age',
        'field': 'Age',
        'type': 'number',
        'operator': 'equal',
        'value': 34
      },
      {
        'label': 'LastName',
        'field': 'LastName',
        'type': 'string',
        'operator': 'equal',
        'value': 'vinit'
      },
      {
        'condition': 'or'
        'rules': [{
          'label': 'Age',
          'field': 'Age',
          'type': 'number',
          'operator': 'equal',
          'value': 34
        }]
      }]
    };
     this.ddbitems = [
      {
        text: 'AddGroup',
        iconCss: 'e-icons e-add-icon e-addgroup'
      },
      {
        text: 'AddCondition',
        iconCss: 'e-icons e-add-icon e-addrule'
      }];
      this.fields = { text: 'key', value: 'value' };
  }
  
  onChange(e: any): void {
    this.qryBldrObj.notifyChange(e.checked,e.event.target, 'not');
  }

  conditionChange(e: any): void {
    this.qryBldrObj.notifyChange(e.value, e.element, 'condition');
  }

  onSelect(event: MenuEventArgs): void {
    let addbtn: Element = closest(event.element,'.e-dropdown-popup'); let ddbId: string = addbtn.id;
    let ddb: string[]= ddbId.split('_');
    if (event.item.text === 'AddGroup') {
      this.qryBldrObj.addGroups([{condition: 'or', 'rules': [{}], not: false}], ddb[1]);
    } else if (event.item.text === 'AddCondition') {
     this.qryBldrObj.addRules([{}], ddb[1]);
    }
  }
  
  onClick(e: any): void {
    this.qryBldrObj.deleteGroup(closest(e.target.offsetParent, '.e-group-container'));
  }
}

```

{% endtab %}

## Column Template

Template allows you to define your own input widgets for columns. To implement [`template`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/columnsModel/#template), you can define the following functions

* `create`: Creates the custom component.
* `write`: Wire events for the custom component.
* `Destroy`:  Destroy the custom component.

In the following sample, dropdown is used as the custom component in the PaymentMode column.

{% tab template="query-builder/filtering", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { RuleModel, QueryBuilderComponent, ColumnsModel, TemplateColumn } from '@syncfusion/ej2-angular-querybuilder';
import { expenseData } from './datasource';
import { DropDownList, MultiSelect } from '@syncfusion/ej2-dropdowns';
import { getComponent, createElement } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<!-- To render Query Builder. -->
               <ejs-querybuilder #querybuilder width="70%" [dataSource]="data" [rule]="importRules" [columns]="filter">
              </ejs-querybuilder>`
})

export class AppComponent implements OnInit {

    public data: Object[];
    public importRules: RuleModel;
     @ViewChild('querybuilder')
    public qryBldrObj: QueryBuilderComponent;
    public filter: ColumnsModel[];
    public paymentTemplate: TemplateColumn;
    public inOperators: string[] = ['in', 'notin'];
    ngOnInit(): void {
        this.data = expenseData;
        this.paymentTemplate = {
        create: () => {
            return createElement('input', { attrs: { 'type': 'text' } });
        },
        destroy: (args: { elementId: string }) => {
            let multiSelect: MultiSelect = (getComponent(document.getElementById(args.elementId), 'multiselect') as MultiSelect);
            if (multiSelect) {
                multiSelect.destroy();
            }
            let dropdown: DropDownList = (getComponent(document.getElementById(args.elementId), 'dropdownlist') as DropDownList);
            if (dropdown) {
                dropdown.destroy();
            }
        },
        write: (args: { elements: Element, values: string[] | string, operator: string }) => {
            let ds: string[] = ['Cash', 'Debit Card', 'Credit Card', 'Net Banking', 'Wallet'];
            if (this.inOperators.indexOf(args.operator) > -1) {
                let multiSelectObj: MultiSelect = new MultiSelect({
                    dataSource: ds,
                    value: args.values as string[],
                    mode: 'CheckBox',
                    placeholder: 'Select Transaction',
                    change: (e: any) => {
                        this.qryBldrObj.notifyChange(e.value, e.element);
                    }
                });
                multiSelectObj.appendTo('#' + args.elements.id);
            } else {
                let dropDownObj: DropDownList = new DropDownList({
                    dataSource: ds,
                    value: args.values as string,
                    change: (e: any) => {
                        this.qryBldrObj.notifyChange(e.itemData.value, e.element);
                    }
                });
                dropDownObj.appendTo('#' + args.elements.id);
            }
        }
    };
         this.filter = [
        { field: 'Category', label: 'Category', type: 'string' },
        { field: 'PaymentMode', label: 'Payment Mode', type: 'string', template: this.paymentTemplate },
        { field: 'TransactionType', label: 'Transaction Type', type: 'string' },
        { field: 'Description', label: 'Description', type: 'string' },
        { field: 'Date', label: 'Date', type: 'date' },
        { field: 'Amount', label: 'Amount', type: 'number'}
    ];
        this.importRules = {
        'condition': 'and',
        'rules': [{
                'label': 'Payment Mode',
                'field': 'PaymentMode',
                'type': 'string',
                'operator': 'equal',
                'value': 'Cash'
            }]
        };
    }

}

```

{% endtab %}

### Using Template

The value template for a particular column can be specified using the content of the NgTemplate. The `#template` template variable identifies the NgTemplate content as the corresponding column.

{% tab template="query-builder/template", sourceFiles="app/app.component.ts,app/template-driven.html,app/app.module.ts,app/main.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { QueryBuilderComponent } from '@syncfusion/ej2-angular-querybuilder';
import { RuleModel } from '@syncfusion/ej2-querybuilder';
@Component({
    selector: 'app-root',
    templateUrl: `app/template-driven.html`
})

export class AppComponent implements OnInit {
@ViewChild('querybuilder') qryBldrObj: QueryBuilderComponent;
  public paymentDataSource: string[] = ['Cash', 'Debit Card', 'Credit Card', 'Net Banking'];
  public importRules: RuleModel;
  public customOperators: any;
  ngOnInit(): void {
    this.importRules = {
      'condition': 'and',
      'rules': [{
        'label': 'Transaction Type',
        'field': 'TransactionType',
        'type': 'string',
        'operator': 'equal',
        'value': 'Expense'
      },
      {
        'label': 'Payment Mode',
        'field': 'PaymentMode',
        'type': 'string',
        'operator': 'equal',
        'value': 'Cash'
      }]
    };
    this.customOperators = [
      {value: 'equal', key: 'Equal'},
      {value: 'notequal', key: 'Not Equal'}
    ];
  }
  
  transactionChange(e: any, ruleID: string): void {
    let elem: HTMLElement = document.getElementById(ruleID).querySelector('.e-rule-value');
    this.qryBldrObj.notifyChange(e.checked === true ? 'Expense' : 'Income', elem, 'value');
  }

  paymentChange(e: any, ruleID: string): void {
    let elem: HTMLElement = document.getElementById(ruleID).querySelector('.e-rule-value');
    this.qryBldrObj.notifyChange(e.value as string, elem, 'value');
  }
}

```

{% endtab %}

## Rule Template

Rule Template allows to define your own user interface for columns. To implement [`ruleTemplate`](https://ej2.syncfusion.com/angular/documentation/api/query-builder/columnsModel/#ruleTemplate) you can create the user interface using `ngTemplate` and assign the values through `actionBegin` event.

The `#ruleTemplate` template variable identifies the NgTemplate content as the corresponding column.

In the following sample, dropdown and slider are used as the custom component and applied `greaterthanorequal` operator to `Age` column.

{% tab template="query-builder/rule-template", sourceFiles="app/app.component.ts,app/template-driven.html,app/app.module.ts,app/main.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild, OnInit } from '@angular/core';
import { QueryBuilderComponent } from '@syncfusion/ej2-angular-querybuilder';
import { ActionEventArgs, RuleModel } from '@syncfusion/ej2-querybuilder';
import { compile } from '@syncfusion/ej2-base';
import { DataManager, Predicate, Query } from '@syncfusion/ej2-data';
import { employeeData } from './datasource';

@Component({
    selector: 'app-root',
    templateUrl: `app/template-driven.html`
})

export class AppComponent implements OnInit {
@ViewChild('querybuilder') qryBldrObj: QueryBuilderComponent;
  public importRules: RuleModel;
  public rangeticks: Object;

  ngOnInit(): void {
    this.importRules = {
      'condition': 'and',
      'rules': [{
        'label': 'Age',
        'field': 'Age',
        'type': 'number',
        'operator': 'greaterthanorequal',
        'value': 32
      }]
    };
    this.rangeticks = { placement: 'Before', largeStep: 5, smallStep: 1, showSmallTicks: true };
  }

  actionBegin(args: ActionEventArgs): void {
    if (args.requestType === 'template-initialize') {
      args.rule.operator = 'greaterthanorequal';
      if (args.rule.value === '') {
        args.rule.value = 30;
      }
    }
  }
  
  fieldChange(e: any): void {
      this.qryBldrObj.notifyChange(e.value, e.element, 'field');
  };

  valueChange(e: any, ruleID: string): void {
    let elem: HTMLElement = document.getElementById(ruleID);
    this.qryBldrObj.notifyChange(e.value as Date, elem, 'value');
    this.refreshTable(this.qryBldrObj.getRule(elem), ruleID);
  }

  viewDetails(ruleID: string): void {
    let ruleElem: HTMLElement = document.getElementById(ruleID);
    let element: HTMLElement = document.getElementById(ruleID + '_section');
    if (element.className.indexOf('e-hide') > -1) {
      this.refreshTable(this.qryBldrObj.getRule(ruleElem), ruleID);
      element.className = element.className.replace('e-hide', '');
      document.getElementById(ruleID + '_option').querySelector('.e-content').textContent = 'Hide Details';
    } else {
      element.className += ' e-hide';
      document.getElementById(ruleID + '_option').querySelector('.e-content').textContent = 'View Details';
    }
  }

  refreshTable(rule: RuleModel, ruleID: string): void {
    let template: string = '<tr><td>${EmployeeID}</td><td>${FirstName}</td><td>${Age}</td></tr>';
    let compiledFunction: any = compile(template);
    let dataManagerQuery: Query = this.qryBldrObj.getDataManagerQuery({condition: 'and', rules: [rule]});
    let dataManager: DataManager = new DataManager(employeeData);
    dataManager.defaultQuery = dataManagerQuery;
    let result: object[] = dataManager.executeLocal();
    let table: HTMLElement = document.getElementById(ruleID + '_datatable') as HTMLElement;
    if (table) {
      if (result.length) {
        table.style.display = 'block';
      } else {
        table.style.display = 'none';
      }
      table.querySelector('tbody').innerHTML = '';
      result.forEach((data) => {
          table.querySelector('tbody').appendChild(compiledFunction(data)[0].querySelector('tr'));
      });
    }
  }
}

```

{% endtab %}
