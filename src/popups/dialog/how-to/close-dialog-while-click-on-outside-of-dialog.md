---
title: "Close the Angular dialog while click on outside of dialog"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Close Dialog when click outside of its region

By default, dialog can be closed by pressing Esc key and clicking the close icon on the right of dialog header. It can also be closed by clicking outside of the dialog using hide method.

> Set the [closeOnEscape](../../api/dialog/#closeonescape) property value to false to prevent closing of the dialog when pressing Esc key.

In the following sample, dialog is closed when clicking outside the dialog area using [hide](../../api/dialog/#hide) method.

{% tab template="dialog/dlg-close", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
    <div #container class='root-container'>
      <ejs-dialog id='dialog' #ejDialog [animationSettings]='animationSettings' content='Are you sure you want to permanently delete all of these items?' header='Delete Multiple Items' [target]='targetElement'
      width='300px' [showCloseIcon]='showCloseIcon' [buttons]='buttons'>
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
    ngAfterViewInit(): void {
      document.onclick = (args: any) : void => {
            if(args.target.tagName === 'BODY') {
                this.ejDialog.hide();
            }
        }
    }

    // Initialize the Dialog component's target element.
    initilaizeTarget: EmitType<object> = () => {
      this.targetElement = document.body;
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
              content:'Yes',
              //Enables the primary button
              isPrimary: true
            }
        },
        {
            'click': this.hideDialog.bind(this),
            // Accessing button component properties by buttonModel property
              buttonModel:{
              content:'No',
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

In the following sample, the dialog is rendered based on the target container. It can also be closed by clicking outside of the dialog.

{% tab template="dialog/dialog-close", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewEncapsulation, ViewChild, ElementRef, AfterViewInit } from '@angular/core';
import { DialogComponent, AnimationSettingsModel } from '@syncfusion/ej2-angular-popups';
import { CheckBoxComponent, ButtonModel } from '@syncfusion/ej2-angular-buttons';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

import { OnInit } from '@angular/core';
import { EmitType } from '@syncfusion/ej2-base';
/**
 * Modal Dialog Component
 */
@Component({
    selector: 'app-root',
    templateUrl: 'app.component.html',
    styleUrls: ['app.component.css'],
    encapsulation: ViewEncapsulation.None
})

export class AppComponent {

   @ViewChild('ejDialog') ejDialog: DialogComponent;
    // Create element reference for dialog target element.
    @ViewChild('container', { read: ElementRef }) container: ElementRef;
    // The Dialog shows within the target element.
    public targetElement: HTMLElement;
    //To get all element of the dialog component after component get initialized.
    ngOnInit() {
      this.initilaizeTarget();
    }
    ngAfterViewInit(): void {
      document.onclick = (args: any) : void => {
            let currentTarget = args.target.closest('ejs-dialog, button');
            if(currentTarget === null) {
                this.ejDialog.hide();
            }
        }
    }

    // Initialize the Dialog component's target element.
    initilaizeTarget: EmitType<object> = () => {
      this.targetElement = document.getElementById("modalTarget");
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
              content:'Yes',
              //Enables the primary button
              isPrimary: true
            }
        },
        {
            'click': this.hideDialog.bind(this),
            // Accessing button component properties by buttonModel property
              buttonModel:{
              content:'No',
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