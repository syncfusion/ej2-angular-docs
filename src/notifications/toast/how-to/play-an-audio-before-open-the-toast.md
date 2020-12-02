---
title: "Play an audio before open the Angular Toast"
component: "Toast"
description: "This example demonstrates how to play audio in the background while opening the Essential JS 2 Toaster control."
---

# Play an audio before the Toast shown

Here below sample demonstrates to playing audio background while opening toast. Here we have included audio play codes into beforeOpen event Function.

> If you want to stop the audio after displaying toast use [`open`](../../api/toast#open) event in Toast. please check the Toast Events [`api's`](../../api/toast#events) for further customization.

{% tab template="toast/toast", sourceFiles="app/**/*.ts,index.html,index.css"    %}

```typescript

import { Component, ViewChild } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id="toast_target"></div>
        <button ejs-button [isPrimary]="true" (click)="btnClick($event)">Show Toast</button>
        <ejs-toast #element  (beforeOpen)="onBeforeOpen($event)"  [position] = 'position' >
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


    onBeforeOpen(e) {
      let audio: HTMLAudioElement = new Audio('https://drive.google.com/uc?export=download&id=1M95VOpto1cQ4FQHzNBaLf0WFQglrtWi7');
     audio.play();
    }
    btnClick() {
      this.toastShow();
    }
    toastShow() {
          setTimeout(
        () => {
            this.element.show();
               }
        }, 0);
    ngAfterViewInit() {
    }
}
```

{% endtab %}
