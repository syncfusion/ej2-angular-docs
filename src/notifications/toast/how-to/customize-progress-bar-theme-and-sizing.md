---
title: "Customize the Angular Toast progress bar theme and sizing"
component: "Toast"
description: "This example demonstrates how to customize the progress bar theme and sizing in the Essential JS 2 Toaster control."
---

# Customize progress bar theme and sizing

In default, the Progress bar will appear based on the theme stylings and dimensions. You can customize progress bar stylings through custom CSS or Event functions.

Here below sample demonstrates customize the progress bar Stylings using [`beforeOpen`](../../api/toast#beforeopen) Event.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <div id='#sample_container '>
        <div id='container'>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
          <div class="row" style="padding-top: 20px">
          <div class="e-float-input">
            <input class="e-input" id="progressHeight" name="Digits" value="4" required>
            <span class="e-float-line"></span>
            <label class="e-float-text" for="Digits">Progress Bar Height</label>
            </div>
        </div>
         <div class="row" style="padding-top: 20px">
          <div class="col-xs-6 col-sm-6 col-lg-6 col-md-6">
            <label> Progress Bar Color </label>
          </div>
          <div class="col-xs-6 col-sm-6 col-lg-6 col-md-6">
            <ejs-dropdownlist #dropDown (change)="dropDownChange($event)" id='games' #sample1 [dataSource]='progressBarColor' index='0'>
            </ejs-dropdownlist>
           </div>
        </div>
        </div>
        </div>
        <ejs-toast #element showProgressBar=true  (created)="onCreate($event)" (beforeOpen)="onBeforeOpen($event)"  [position] = 'position' >
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
    @ViewChild('element') element;
    @ViewChild('dropDown') dropDownListObj;
    public position = { X: 'Right', Y: 'Bottom' };
    public progressBarColor = ['Red', 'Cyan', 'Blue', 'Yellow', 'Pink'];

    onBeforeOpen(e) {
  const progress = e.element.querySelector('.e-toast-progress');
  progress.style.height = (document.getElementById('progressHeight') as any).value + 'px';
  progress.style.backgroundColor =  this.dropDownListObj.value;
   }

   dropDownChange() {
    const progressEles: NodeList = this.element.element.querySelectorAll('.e-toast-progress');
    progressEles.forEach((ele: HTMLElement) => {
      ele.style.backgroundColor = this.dropDownListObj.value;
    });
   }

    onCreate() {
      this.element.show();
    }
    btnClick() {
      this.toastShow();
    }
    toastShow() {
          setTimeout(
        () => {
            this.element.show();
        }, 0);
    }
}

```

{% endtab %}
