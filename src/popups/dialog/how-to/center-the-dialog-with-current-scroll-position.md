---
title: "Center the dialog based on current scroll position"
component: "Dialog"
description: "This section explains how to center the dialog based on the current scroll position."
---

# Center the dialog based on the current scroll position

The dialog is always centered based on the target container. If the target is not specified, then the dialog will be rendered based on its body and centered in the position of the current viewpoint.

In the following sample, the model dialog is centered based on its current scroll position of the page.

{% tab template="dialog/center-the-dialog", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Modal Dialog</button>
    <div #container class='root-container'></div>
    <ejs-dialog id='dialog' #ejDialog isModal='true' (overlayClick)="onOverlayClick()"
    content='This is a modal dialog' [target]='targetElement' width='250px'> </ejs-dialog>`
})

export class AppComponent implements OnInit {
  @ViewChild('ejDialog') ejDialog: DialogComponent;
  // The Dialog shows within the target element.
  @ViewChild('container', { read: ElementRef }) container: ElementRef;
  // The Dialog shows within the target element.
  public targetElement: HTMLElement;

  // To get all element of the dialog component after component get initialized.
  ngOnInit() {
    this.initilaizeTarget();
  }

  // Initialize the Dialog component target element.
  public initilaizeTarget: EmitType<object> = () => {
    this.targetElement = document.body;
  }
  // Sample level code to handle the button click action
  public onOpenDialog = function(event: any): void {
      // Call the show method to open the Dialog
      this.ejDialog.show();
  };
  // Sample level code to hide the Dialog when click the Dialog overlay
  public onOverlayClick: EmitType<object> = () => {
      this.ejDialog.hide();
  }
}

```

{% endtab %}