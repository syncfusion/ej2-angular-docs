---
title: "Customize the dialog appearance"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Customize the Dialog appearance

You can customize the dialog appearance by providing dialog template as string or HTML element to the [content](../../api/dialog/#content) property. In the following sample, dialog is customized as error window appearance.

{% tab template="dialog/dlg-appearance", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
    <div #container class='root-container'>
      <ejs-dialog id='dialog' #ejDialog [animationSettings]='animationSettings' header='File and Folder Rename' [target]='targetElement'
      width='400px' [showCloseIcon]='showCloseIcon' [buttons]='buttons'>
      <ng-template #content>
        <div class = 'dialog-content'>
          <div class='msg-wrapper  col-lg-12'>
              <span class ='e-icons close-icon col-lg-2'></span>
              <span  class ='error-msg col-lg-10'>Can not rename 'pictures' because a file or folder with that name already exists </span>
              </div>
              <div class ='error-detail col-lg-8'>
              <span>Specify a different name</span>
              </div>
          </div>
      </ng-template>
      </ejs-dialog> </div> `
})

export class AppComponent implements OnInit {
    @ViewChild('ejDialog') ejDialog: DialogComponent;
    // Create element reference for dialog target element.
    @ViewChild('container', { read: ElementRef }) container: ElementRef;
    // The Dialog shows within the target element.
    public targetElement: HTMLElement;

    //To get all element of the dialog component after component get initialized.
    ngOnInit() {
      this.initilaizeTarget();
    }

    // Initialize the Dialog component's target element.
    initilaizeTarget: EmitType<object> = () => {
      this.targetElement = this.container.nativeElement.parentElement;
    }

    //Animation options
    public animationSettings: Object = { effect: 'Zoom', duration: 400, delay: 0 };

    public showCloseIcon: boolean = true;
    // Hide the Dialog when click the footer button.
    public hideDialog: EmitType<object> = () => {
        this.ejDialog.hide();
    }
    // Enables the footer buttons
    public buttons: Object = [
        {
            'click': this.hideDialog.bind(this),
            // Accessing button component properties by buttonModel property
              buttonModel:{
              content:'Close',
              //Enables the primary button
              isPrimary: true
            }
        }
    ];
    // Sample level code to handle the button click action
    public onOpenDialog = function(event: any): void {
        // Call the show method to open the Dialog
        this.ejDialog.show();
    }
}

```

{% endtab %}
