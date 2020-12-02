---
title: "Angular Toast Time out"
component: "Toast"
description: "This section explains how to set time-out value for the Toast component, which is used to display toast till the time-out reaches without user interaction."
---

# Timeout

Toast can be expired based on [`timeOut`](../../api/toast#timeout) property, toast will live till the timeOut reaches without user interaction, a timeOut value was considered as the millisecond.

* `timeOut` delay can be visually represented through [`Progress Bar`](./config#progress-bar).

* [`extendedTimeOut`](../../api/toast#extendedtimeout) property can make how long the toast will display after a user hovers over it.

> You can terminate the process by using  `showCloseButton` property for destroying toast at any time.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <div id='sample_container'>
         <div id='container'>
            <div class="e-float-input">
               <input class="e-input" id="toast_input_index" required="" value="5000">
               <span class="e-float-line"></span>
               <label class="e-float-text">Enter timeOut</label>
            </div>
        </div>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        </div>
        <ejs-toast #element (created)="onCreate($event)" [position] = 'position' >
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
    public position = { X: 'Right', Y: 'Bottom' };

    onCreate() {
      this.element.show();
    }
    btnClick() {
      const value = parseInt((document.getElementById('toast_input_index') as HTMLInputElement).value, 10);
      this.element.show({timeOut: value});
    }
}

```

{% endtab %}

## Static toast

We can prevent auto hiding in a toast as visible like static. For this, we need to set zero (`0`) value in timeOut Property.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <div id='sample_container'>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        </div>
        <ejs-toast #element (created)="onCreate($event)" showCloseButton=true timeOut = 0  [position] = 'position' >
                  <ng-template #title>
                  <div>Matt sent you a friend request</div>
              </ng-template>
              <ng-template #content>
                  <div>Hey, wanna dress up as wizards and ride our hoverboards?</div>
              </ng-template>
     </ejs-toast>`
})

export class AppComponent {
  @ViewChild('element') element;
  public position = { X: 'Right', Y: 'Top' };

  onCreate() {
    this.element.show();
  }
  btnClick() {
    this.element.show();
  }
}

```

{% endtab %}

## See Also

* [Hide the toast on click](./how-to/close-the-toast-with-click-tap/)