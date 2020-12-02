---
title: "Use Wizard like Dialog Editing"
component: "Grid"
description: "Learn how to Use Wizard like Dialog Editing."
---

# Use Wizard like Dialog Editing

Wizard helps you create intuitive step-by-step forms to fill. You can achieve the wizard like editing by using the dialog template feature. It support your own editing template by defining [`editSettings.mode`](../../api/grid/editSettings/#mode) as **Dialog** and [`editSettingsTemplate`](../../api/grid/editSettings/#template) as template variable to define the editors.

The following example demonstrate the wizard like editing in the grid with the unobtrusive Validation.

{% tab template="grid/wizardtemplate", sourceFiles="app/app.component.ts,app/wizardtemplate.html,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { FormGroup } from '@angular/forms';
import { data } from './datasource';
import { DataUtil } from '@syncfusion/ej2-data';
import { EditSettingsModel, ToolbarItems, GridComponent, DialogEditEventArgs } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    templateUrl: `app/wizardtemplate.html`
})
export class AppComponent implements OnInit {

    public data: object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public shipCountryDistinctData: object;
    public next = 'Next';
    public currentTab = 0;
    public hidden = true;
    @ViewChild('grid') grid: GridComponent;
    @ViewChild('orderForm') orderForm: FormGroup;

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
        this.toolbar = ['Add', 'Edit', 'Delete'];
        this.shipCountryDistinctData = DataUtil.distinct(data, 'ShipCountry', true);
    }

    actionComplete(args: DialogEditEventArgs) {
        if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            args.form.ej2_instances[0].rules = {}; // Disable deafault valdation.
            // Set initail Focus
            if (args.requestType === 'beginEdit') {
                (args.form.elements.namedItem('CustomerID') as HTMLInputElement).focus();
            }
            this.currentTab = 0;
            this.hidden = true;
            this.next = 'Next';
        }
    }

    nextBtn(args) {
        if (this.orderForm.valid) {
            if (this.next !== 'SUBMIT') {
                this.currentTab++;
                this.nextpre(this.currentTab);
            } else {
                this.grid.endEdit();
            }
        }
    }

    previousBtn(args) {
        if (this.orderForm.valid) {
            this.currentTab--;
            this.nextpre(this.currentTab);
        }
    }

    nextpre(current) {
        if (current) {
            this.hidden = false;
            this.next = 'SUBMIT';
        } else {
            this.hidden = true;
            this.next = 'NEXT';
        }
    }
}

```

{% endtab %}
