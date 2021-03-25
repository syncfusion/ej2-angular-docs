---
title: "Angular Toast Configuring Options"
component: "Toast"
description: "The Syncfusion Angular Toast component configuration section explains how to customize the appearance of the Toast control using built-in APIs."
---

# Configuring options

This section explains on customizing the Toast appearance using built-in APIs.

## Title and content template

Toast can be created with the notification message. The message contains [`title`](../../api/toast#title) and [`content`](../../api/toast#content) of the Toasts. Title and contents are adaptable in any resolution.

> Title or Content property can be given as HTML element/element ID as a string that can be displayed as a Toast.

{% tab template="toast/toast", isDefaultActive=true, sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript
import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        <ejs-toast #element (created)="onCreate($event)" [position] = 'position' >
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
    public position = { X: 'Right' };

    onCreate() {
      this.toastShow();
    }
    btnClick() {
      this.toastShow();
    }
    toastShow() {
          setTimeout(
        () => {
            this.element.show();
        }, 700);
    }
}
```

{% endtab %}

## Specifying custom target

By default toast can be rendered in the document body, we can change the target position for toast rendering using [`target`](../../api/toast#target) property. Based on the target [`position`](../../api/toast#position) will update.

## Close Button

In default [`showCloseButton`](../../api/toast#showclosebutton) is not enabled. We can enable it by setting true value. Before expiring toast we can use to close or destroy toasts manually.

## Progress bar

In default [`showProgressBar`](../../api/toast#showprogressbar) is not enabled. If we enabled it can visually indicate when will the toast gets expired. Based on the `timeOut` property Progress bar will appear.

### Progress bar direction

By default, the [progressDirection](../../api/toast/#progressDirection) is set to "Rtl" and it will appear from right to left direction. You can change the progressDirection to "Ltr" to make it appear from left to right direction.

## Newest on top

In default, newly created toasts will append next with existing toast. We can change the Sequence like inserting before the toast, by enabling the [`newestOnTop`](../../api/toast#newestontop).

Here below sample demonstrates the combination of `target`, `showCloseButton`, `showProgressBar` and `newestOnTop` properties in toast.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        <ejs-toast #element (created)="onCreate($event)" showCloseButton=true newestOnTop=true showProgressBar=true progressDirection="Ltr" target='#toast_target' [position] = 'position' >
            <ng-template #title>
                <div>File Downloading</div>
            </ng-template>
            <ng-template #content>
                <div class="progress"><span style="width: 80%"></span></div>
            </ng-template>
        </ejs-toast>`
})

export class AppComponent {
    @ViewChild('element') element;
    public position = { X: 'Center' };

    onCreate() {
      this.element.show();
    }
    btnClick() {
      this.element.show();
    }
}
```

{% endtab %}

## Width and height

we can set toast dimensions through [`width`](../../api/toast#width) and [`height`](../../api/toast#height) property. This will individually set all toasts, we can create different custom dimension toasts.

In default toast can be rendered with '300px' width with 'auto' height

   > In mobile device toast default width gets '100%' width of the page.
   > When we sets toast width as '100%' toast will occupies full width and displayed top or bottom based on position `Y` property.

Both width and height property allows setting pixels/numbers/percentage. The number value is considered as pixels.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <div id=sample_container>
         <div id='container'>
            <div class='row' style="padding-top: 20px;margin:0" id= "toast_pos_target">
              <table>
                <tr>
                  <td>
                      <div style='padding:25px 0 0 0;'>
                          <ejs-radiobutton (change)="topChange($event)" label="Top" name="position" value="Top"></ejs-radiobutton>
                      </div>
                  </td>
                  <td>
                      <div style='padding:25px 0 0 0;'>
                         <ejs-radiobutton (change)="bottomChange($event)" label="Bottom" name="position" value="Bottom" checked="true"></ejs-radiobutton>
                      </div>
                  </td>
                </tr>
                <tr>
                   <td>
                     <div style='padding:25px 0 0 0;'>
                         <ejs-checkbox #checkbox label="100% Width" (change)="checkBoxChange($event)"></ejs-checkbox>
                      </div>
                   </td>
                </tr>
              </table>
            </div></div>
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
    @ViewChild('element') toast;
    public position = { X: 'Center', Y: 'Bottom' };

    onCreate() {
      this.toastShow();
    }
    btnClick() {
      this.toastShow();
    }
    toastShow() {
          setTimeout(
        () => {
            this.toast.show();
        }, 700);
    }

    bottomChange(e) {
      let toast = this.toast;
        if (e.event.target.checked) {
      toast.position.Y = "Bottom";
      toast.hide('All');
      this.toastShow();
    }
    }

    topChange(e) {
      let toast = this.toast;
      if (e.event.target.checked) {
      toast.position.Y = "Top";
      toast.hide('All');
      this.toastShow();
    }
    }

    checkBoxChange(e) {
      let toast = this.toast;
        if (e.checked) {
            toast.hide('All');
            toast.width = "100%";
            toast.title = "";
            toast.content = "<div class='e-custom'>Take a look at our next generation <b>Javascript</b> <a href='https://ej2.syncfusion.com/home/index.html' target='_blank'>LEARN MORE</a></div>";
            this.toastShow();
        } else {
            toast.hide('All');
            toast.width = 300;
            toast.title = 'Matt sent you a friend request',
            toast.content = 'Hey, wanna dress up as wizards and ride our hoverboards?',
            this.toastShow();
        }
    }
}
```

{% endtab %}

## See Also

* [Prevent duplicate toasts](./how-to/prevent-duplicate-toast-display/)
* [Customize the progress bar](./how-to/customize-progress-bar-theme-and-sizing/)