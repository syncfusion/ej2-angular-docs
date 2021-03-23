---
title: "Create wizard using Accordion"
component: "Accordion"
description: "This online shopping example demonstrates how to create multiple components inside the Essential JS 2 Accordion control."
---

# Create wizard using Accordion

Accordion items can be disabled dynamically by passing the index and boolean value with the [`enableItem`](../../api/accordion#enableitem) method and also dynamically expand the item using [`expandItem`](../../api/accordion#expanditem) method.

The below Wizard sample is designed for Online Shopping model. In this, each Accordion item is integrated with required components to fill
the details and designed for getting user details and making payment at the end. Each field is provided with validation for all mandatory
option to enable/disable to next Accordion. In below sample, accordion items can be disabled dynamically with [`enableItem`](../../api/accordion#enableitem) method using [`created`](../../api/accordion#created) event.

{% tab template="accordion/accordion-disable", sourceFiles="app/**/*.ts,app/**/*.html,index.css" %}

```typescript

import { Component, ViewChild, OnInit } from '@angular/core';
import { enableRipple, isNullOrUndefined as isNOU } from '@syncfusion/ej2-base';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { DatePickerComponent } from '@syncfusion/ej2-calendars';
import { NumericTextBoxComponent } from '@syncfusion/ej2-angular-inputs';
import { AccordionComponent, AccordionItemsDirective, AccordionItemDirective } from '@syncfusion/ej2-angular-navigations';

enableRipple(true);

@Component({
  selector: 'app-container',
  templateUrl: 'app/app.component.html'
})

export class AppComponent implements OnInit {
  @ViewChild('alertDlg') alertDlg: DialogComponent;
  @ViewChild('accordion') accordion: AccordionComponent;
  @ViewChild('mobile') mobile: NumericTextBoxComponent;
  @ViewChild('cardNo') cardNo: NumericTextBoxComponent;
  @ViewChild('date') expiry: DatePickerComponent;
  @ViewChild('cvv') cvv: NumericTextBoxComponent;

  public dlgTarget: HTMLElement;
  public dlgButtons: Object[];
  public success: string = 'Your payment successfully processed';
  public email_alert: string = 'Enter valid email address';
  public mobile_alert: string = 'Mobile number length should be 10';
  public card_alert: string = 'Card number length should be 16';
  public cvv_alert: string = 'CVV number length should be 3';

  public ngOnInit(): void {
    this.dlgTarget = document.body;
    this.dlgButtons = [{
      buttonModel: { content: 'Ok', isPrimary: true },
        click: (() => {
          this.alertDlg.hide();
          if (this.accordion.expandedItems[0] === 2 && this.alertDlg.content === this.success) {
            this.accordion.enableItem(0, true);
            this.accordion.enableItem(1, false);
            this.accordion.enableItem(2, false);
            this.accordion.expandItem(true, 0);
          }
        })
      }];
  }

  public dlgCreated(): void {
    this.alertDlg.hide();
  }

  public acrdnCreated(): void {
   this.accordion.enableItem(1, false);
   this.accordion.enableItem(2, false);
  }

  public btnClick(e: any): void {
    switch (e.target.id) {
      case 'Continue_Btn':
        let email: string = document.getElementById('email');
        let password: string = document.getElementById('password');
        if(email.value !== '' && password.value !== '') {
          if(this.checkMail(email.value)) {
            email.value = password.value = '';
            this.accordion.enableItem(1, true);
            this.accordion.enableItem(0, false);
            this.accordion.expandItem(true, 1);
          }
          document.getElementById('err1').classList.remove('show');
        } else {
          document.getElementById('err1').classList.add('show');
        }
        break;
      case 'Continue_BtnAdr':
        let name: string = document.getElementById('name');
        let address: string = document.getElementById('address');
        if((name.value !== '') && (address.value !== '') && (!isNOU(this.mobile.value))) {
          if(this.checkMobile(this.mobile.value)) {
            this.accordion.enableItem(2, true);
            this.accordion.enableItem(1, false);
            this.accordion.expandItem(true, 2);
          }
          document.getElementById('err2').classList.remove('show');
        } else {
          document.getElementById('err2').classList.add('show');
        }
        break;
      case 'Back_Btn':
        this.accordion.enableItem(1, true);
        this.accordion.enableItem(2, false);
        this.accordion.expandItem(true, 1);
        break;
      case 'Save_Btn':
        let cardHolder: string =document.getElementById('cardHolder');
        if(!isNOU(this.cardNo.value) && (cardHolder.value !== '') && (!isNOU(this.expiry.value)) && !isNOU(this.cvv.value)) {
          if (this.checkCardNo(this.cardNo.value)) {
            if (this.checkCVV(this.cvv.value)) {
              this.alertDlg.content = this.success;
              this.alertDlg.show();
            }
          }
          document.getElementById('err3').classList.remove('show');
        } else {
          document.getElementById('err3').classList.add('show');
        }
        break;
    }
  }

  public checkMail(mail: string): void {
    if (/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(mail)) {
      return true;
    } else {
      this.alertDlg.content = this.email_alert;
      this.alertDlg.show();
      return false;
    }
  }

  public checkMobile(mobile: number): void {
    if (/^\d{10}$/.test(mobile)) {
      return true;
    } else {
      this.alertDlg.content = this.mobile_alert;
      this.alertDlg.show();
      return false;
    }
  }

  public checkCardNo(cardNo: number): void {
    if (/^\d{16}$/.test(cardNo)) {
      return true;
    } else {
      this.alertDlg.content = this.card_alert;
      this.alertDlg.show();
      return false;
    }
  }

  public checkCVV(cvv: number): void {
    if (/^\d{3}$/.test(cvv)) {
      return true;
    } else {
      this.alertDlg.content = this.cvv_alert;
      this.alertDlg.show();
      return false;
    }
  }
}

```

{% endtab %}