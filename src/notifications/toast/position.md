---
title: "Angular Toast Positions"
component: "Toast"
description: "The Syncfusion Angular Toast component position section explains how to customize the toast position or update the toast predefined position."
---

# Positions

Toast position can be updated based on predefined positions or user customizable positions. Predefined position combinations are updated in [`X`](../../api/toast/toastPositionModel#x) and [`Y`](../../api/toast/toastPositionModel#y) position properties.

## Predefined

`X` Positions

* Left
* Center
* Right

`Y` Positions

* Top
* Bottom

> In the case of multiple Toast display, new Toast position will not update on dynamic change of property values, until the old Toast messages removed.
> Toast occupies full width when we set width as '100%', so X positions won't affect changes when '100%' width.

## Custom

Custom `X` and `Y` Position can be given as pixels/numbers/percentage. The number value is considered as pixels. based value top and left value updated in the toast.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <div id='sample_container'>
        <div id='container'>
          <div class='row' style="padding-top: 20px" id= "toast_pos_target">
            <div id="toast_pos"> </div>
            <div id="toast_pos_property">
                <table style="width: 100%">
                    <tr>
                        <td>
                            <div style='padding:25px 0 0 0;'>
                                <ejs-radiobutton (change)="positionChange($event)" label="Position" name="position" value="position" checked="true"></ejs-radiobutton>
                            </div>
                        </td>
                        <td>
                            <div style='padding:25px 0 0 0;'>
                                <ejs-radiobutton (change)="customePosition($event)" label="Custom" name="position" value="position"></ejs-radiobutton>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td id="dropdownChoose" colspan="2">
                            <div id="dropdown" style='padding-top:25px;'>
<ejs-dropdownlist #dropDown (change)="dropDownChange($event)"  [dataSource]='dropdownDB' index='4'>
            </ejs-dropdownlist>
                            </div>
                        </td>
                    </tr>
                    <tr>
                        <td colspan="2" id="customChoose" style="display: none">
                            <form id="formId" class="form-horizontal">
                                <div class='e-row'>
                                    <div class="e-float-input">
                                        <input class="e-input" id="xPos" name="Digits" value=50 digits="true" data-digits-message="Please enter digits only." required="">
                                        <span class="e-float-line"></span>
                                        <label class="e-float-text" for="Digits">X Position</label>
                                    </div>
                                </div>
                                <div class='e-row'>
                                    <div class="e-float-input">
                                        <input class="e-input" id="yPos" name="Digits" value=50 digits="true" data-digits-message="Please enter digits only." required="">
                                        <span class="e-float-line"></span>
                                        <label class="e-float-text" for="Digits">Y Position</label>
                                    </div>
                                </div>
                            </form>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            <div style='padding:25px 0 0 0;'>
                                <ejs-radiobutton (change)="targetChange($event)" label="Target" name="target" value="Bottom"></ejs-radiobutton>
                            </div>
                        </td>
                        <td>
                            <div style='padding:25px 0 0 0;'>
                                <ejs-radiobutton (change)="globalTargetChange($event)" label="Global" name="target" value="Bottom" checked="true"></ejs-radiobutton>
                            </div>
                        </td>
                    </tr>
                </table>
                <div id="toast_btn" style="padding-top: 25px">
                  <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
                </div>
            </div>
        </div>
        </div></div>

        <ejs-toast #element (created)="onCreate($event)"  [position] = 'position' >
              <ng-template #title>
                  <div>Matt sent you a friend request</div>
              </ng-template>
              <ng-template #content>
                  <div>Hey, wanna dress up as wizards and ride our hoverboards?</div>
              </ng-template>
            </ejs-toast>
        `
})

export class AppComponent {
    @ViewChild('element') toastObj;
    @ViewChild('dropDown') dropDownList;

    public position = { X: 'Right', Y: 'Bottom' };
    public dropdownDB = ['Top Left', 'Top Right', 'Top Center', 'Bottom Left', 'Bottom Right', 'Bottom Center' ];
    public customFlag = false;

    onCreate() {
      this.toastShow();
    }
    btnClick() {
    if (this.customFlag) {
        this.setcustomPosValue();
    }
    this.toastObj.hide('All');
    this.toastShow();
    }

    positionChange(e) {
      if (e.event.target.checked) {
        this.toastObj.hide('All');
        document.getElementById('dropdownChoose').style.display = 'table-cell';
        document.getElementById('customChoose').style.display = 'none';
        this.setToastPosValue(this.dropDownList.value.toString());
        this.customFlag = false;
        this.toastShow();
      }
    }

    customePosition(e) {
      if (e.event.target.checked) {
        this.toastObj.hide('All');
        document.getElementById('dropdownChoose').style.display = 'none';
        document.getElementById('customChoose').style.display = 'table-cell';
        this.setcustomPosValue();
        this.customFlag = true;
        this.toastShow();
      }
    }

    dropDownChange(e) {
    this.toastObj.hide('All');
    this.setToastPosValue(e.value);
    this.toastShow();
    }
    globalTargetChange(e) {
      if (e.event.target.checked) {
        this.toastObj.hide('All');
        this.toastObj.target = document.body;
        this.toastShow();
      }
    }

    targetChange(e) {
      if (e.event.target.checked) {
        this.toastObj.hide('All');
        this.toastObj.target = '#toast_pos_target';
        this.toastShow();
      }
    }

     setcustomPosValue(): void {
    this.toastObj.position.X = parseInt((<any>document.getElementById('xPos')).value, 10);
    this.toastObj.position.Y = parseInt((<any>document.getElementById('yPos')).value, 10);
     }

 setToastPosValue(value: string): void {
    value = value.toLowerCase().replace(' ', '');
    let toastObj = this.toastObj;
    switch (value) {
        case 'topleft':
            toastObj.position.X = 'Left'; toastObj.position.Y = 'Top'; break;
        case 'topright':
            toastObj.position.X = 'Right'; toastObj.position.Y = 'Top'; break;
        case 'topcenter':
            toastObj.position.X = 'Center'; toastObj.position.Y = 'Top'; break;
        case 'topfullwidth':
            toastObj.width = '100%'; toastObj.position.X = 'Center'; toastObj.position.Y = 'Top'; break;
        case 'bottomleft':
            toastObj.position.X = 'Left'; toastObj.position.Y = 'Bottom'; break;
        case 'bottomright':
            toastObj.position.X = 'Right'; toastObj.position.Y = 'Bottom'; break;
        case 'bottomcenter':
            toastObj.position.X = 'Center'; toastObj.position.Y = 'Bottom'; break;
        case 'bottomfullwidth':
            toastObj.width = '100%'; toastObj.position.X = 'Center'; toastObj.position.Y = 'Bottom'; break;
    }
}

    toastShow() {
            setTimeout(
        () => {
            this.toastObj.show();
        }, 700);
    }
}

```

{% endtab %}

## See Also

* [Render toast with different positions](./how-to/show-multiple-toasts-in-various-positions/)