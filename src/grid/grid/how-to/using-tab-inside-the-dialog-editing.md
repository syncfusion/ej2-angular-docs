---
title: "Using Tab Inside the Dialog Editing"
component: "Grid"
description: "Learn how to Using Tab Inside the Dialog Editing."
---

# Using Tab Inside the Dialog Editing

You can use [`Tab`](../../../tab/index.html) component inside dialog edit UI using dialog template feature. The dialog template feature can be enabled by defining  [`editSettings.mode`](../../../api/grid/editSettings/#mode) as `Dialog` and [`editSettingsTemplate`](../../../api/grid/editSettings/#template) as template variable to define the editors.

To include tab components in the Dialog, please ensure the following steps:

**Step 1**:

To render the Tab component, use the [`editSettingsTemplate`](../../../api/grid/editSettings/#template) of the Grid. Inside the content template of the tab items define
the input elements.

```html

    <ejs-tab #tab id="tab_wizard" showCloseButton=false (selecting)='selecting($event)'>
        <e-tabitems>
            <e-tabitem [header]="{ 'text': 'Details' }" >
            <ng-template #content>
            <div id="tab1">
        <div class="form-row">
            <div class="form-group col-md-6">
                <div class="e-float-input e-control-wrapper" [ngClass]="{'e-error': OrderID.invalid && (OrderID.dirty || OrderID.touched)}">
                    <input [(ngModel)]="data.OrderID" required id="OrderID" name="OrderID" type="text" [attr.disabled]="!data.isAdd ? '' : null" #OrderID="ngModel">
                    <span class="e-float-line"></span>
                    <label class="e-float-text e-label-top" for="OrderID"> Order ID</label>
                </div>
                <div id="OrderIDError" *ngIf='OrderID.invalid && (OrderID.dirty || OrderID.touched)'>
                    <label class="e-error" for="OrderID" id="OrderID-info" style="display: block;">*Order ID is required</label>
                </div>
            </div>
        </div>
        <div class="form-row">
            <div class="form-group col-md-6">
                <div class="e-float-input e-control-wrapper" [ngClass]="{'e-error': CustomerID.invalid && (CustomerID.dirty || CustomerID.touched)}">
                    <input [(ngModel)]="data.CustomerID" required id="CustomerID" name="CustomerID" type="text" #CustomerID="ngModel">
                    <span class="e-float-line"></span>
                    <label class="e-float-text e-label-top" for="CustomerID">Customer Name</label>
                </div>
                <div id="CustomerIDError" *ngIf='CustomerID.invalid && (CustomerID.dirty || CustomerID.touched)'>
                    <label class="e-error" for="CustomerID" id="CustomerID-info" style="display: block;">*Customer Name is required</label>
                </div>
            </div>
        </div>
        <button ejs-button type="button" cssClass="e-info e-btn" style="float: right" (click)="nextBtn($event)" >next</button>
    </div>
            </ng-template></e-tabitem>
            <e-tabitem [header]="{ 'text': 'Verify' }">
            <ng-template #content>
               <div id="tab2" style='display: none'>
        <div class="form-row" >
            <div class="form-group col-md-6">
                <ejs-dropdownlist id="ShipCountry" name="ShipCountry" [(ngModel)]="data.ShipCountry" [dataSource]='shipCountryDistinctData' [fields]="{text: 'ShipCountry', value: 'ShipCountry' }" placeholder="Ship Country" popupHeight='300px' floatLabelType='Always'></ejs-dropdownlist>
            </div>
        </div>
        <div class="form-row">
            <div class="form-group col-md-6">
                <ejs-checkbox #Verified name="Verified" id="Verified" label="Verified" [checked]="data.Verified" ></ejs-checkbox>
            </div>
        </div>
        <button ejs-button type="button" cssClass="e-info e-btn" style="float: right" (click)='submitBtn($event)'>submit</button>
    </div>
            </ng-template>
            </e-tabitem>
        </e-tabitems>
    </ejs-tab>

```

The following example, we have rendered tab control inside the edit dialog. The tab control has two tabs and once you fill the first tab and navigate to second one. The validation for first tab was done before navigate to second.

{% tab template="grid/tablikeedit", sourceFiles="app/app.component.ts,app/tablikeedit.html,app/app.module.ts,app/main.ts" %}

```typescript

import { Component, OnInit, ViewChild } from '@angular/core';
import { FormGroup } from '@angular/forms';
import { DataUtil } from '@syncfusion/ej2-data';
import { data } from './datasource';
import { EditSettingsModel, ToolbarItems, GridComponent, DialogEditEventArgs } from '@syncfusion/ej2-angular-grids';

@Component({
    selector: 'app-root',
    templateUrl: `./app/tablikeedit.html`
})
export class AppComponent implements OnInit {

    public data: Object[];
    public editSettings: EditSettingsModel;
    public toolbar: ToolbarItems[];
    public shipCountryDistinctData: Object;
    @ViewChild('grid')
    grid: GridComponent;
    @ViewChild('orderForm')
    orderForm: FormGroup
    @ViewChild('tab')
    tabObj: any;

    ngOnInit(): void {
        this.data = data;
        this.editSettings = { allowEditing: true, allowAdding: true, allowDeleting: true, mode: 'Dialog' };
        this.toolbar = ['Add', 'Edit', 'Delete'];
        this.shipCountryDistinctData = DataUtil.distinct(data, 'ShipCountry', true );
    }

    actionComplete(args: DialogEditEventArgs) {
        if ((args.requestType === 'beginEdit' || args.requestType === 'add')) {
            // Disable deafault valdation.
            args.form.ej2_instances[0].rules = {};
            // Set initail Focus
            if (args.requestType === 'beginEdit') {
                (args.form.elements.namedItem('CustomerID')as HTMLInputElement).focus();
            }
        }
    }

    nextBtn() {
        this.moveNext();
    }

    selecting(e) {
     if(e.isSwiped){
       e.cancel = true;
     }
     if(e.selectingIndex === 1) {
       e.cancel = !this.orderForm.valid;
     }
    }

    moveNext() {
        if (this.orderForm.valid)) {
            this.tabObj.select(1);
        }
    }
    submitBtn() {
        if (this.orderForm.valid) {
            this.grid.endEdit();
        }
    }
}

```

{% endtab %}