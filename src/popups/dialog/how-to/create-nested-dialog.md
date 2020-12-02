---
title: "Create Nested Dialog"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Create nested Dialog

A Dialog can be nested within another Dialog. The below sample contains parent and child Dialog (inner Dialog).

**Step 1**:

Create two div elements with id `#dialog` and `#innerDialog`.

**Step 2**:

Initialize the Dialog as mentioned in the below sample.

**Step 3**:

Set the inner Dialog target as `#dialog`.

{% tab template="dialog/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
    <div #container class='root-container'></div>
      <ejs-dialog id='dialog' #ejDialog header='Outer Dialog' height='300px' width='400px' showOnInit='true' showCloseIcon='true' [content]='content' [target]='targetElement' [animationSettings]='dialogAnimation' [closeOnEscape]='closeOnEscape'>
      <button class="e-control e-btn" id="innerButton" (click)="onOpenInnerDialog($event)" style='margin-left: 18px;'>Open InnerDialog</button>
      </ejs-dialog>
      <ejs-dialog id='innerDialog' #ejInnerDialog header='Inner Dialog' height='150px' width='250px' showOnInit='true' showCloseIcon='true' content='This is a Nested Dialog' target='#dialog' [animationSettings]='dialogAnimation' [closeOnEscape]='closeOnEscape'>
      </ejs-dialog>
        `
})

export class AppComponent implements OnInit {
    @ViewChild('ejDialog') ejDialog: DialogComponent;
    @ViewChild('ejInnerDialog') ejInnerDialog: DialogComponent;
   // Create element reference for dialog target element.
    @ViewChild('container', { read: ElementRef }) container: ElementRef;
    // The Dialog shows within the target element.
    public targetElement: HTMLElement;

    //To get all element of the dialog component after component get initialized.
    ngOnInit() {
      this.initilaizeTarget();
    }

    // Initialize the Dialog component target element.
    public initilaizeTarget: EmitType<object> = () => {
      this.targetElement = this.container.nativeElement.parentElement;
    }
    // Dialog animation
    public dialogAnimation: Object={effect: 'None'};
     // Disable the Esc key option to hide the Dialog
    public closeOnEscape: boolean =false;
    // Dialog header template content
    public header: string='<div title="Installation Complete" class="e-icon-settings e-icons" style="padding: 3px;">   Installation Complete</div>';
    // Dialog footer template content
    public footerTemplate: string='<span style="float: left;font-size: 14px;padding-left: 15px;color: rgba(0, 0, 0, 0.54);">Click the close button to Exit</span>';
    // Sample level code to handle the button click action
    public onOpenDialog = function(event: any): void {
        this.ejDialog.show();
    }
    public onOpenInnerDialog = function(event: any): void {
        this.ejInnerDialog.show();
    }
}

```

{% endtab %}
