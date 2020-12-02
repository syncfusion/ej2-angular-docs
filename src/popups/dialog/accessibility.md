---
title: "Accessibility"
component: "Dialog"
description: "Describes the accessibility standard of the modal dialog box component such as WAI-ARIA attributes, keyboard interaction, and theming."
---

# Accessibility

The Dialog characterized with complete ARIA Accessibility support which helps to accessible
by on-screen readers and other assistive technology devices. This component designed with the
reference of the guidelines document given in [WAI ARAI Accessibility Practices](https://www.w3.org/TR/wai-aria-practices-1.1/#dialog_modal).

The Dialog component uses the `Dialog` role and following ARIA properties to its element based on its state.

| **Property** | **Functionalities** |
| --- | --- |
| aria-describedby | It indicates the Dialog content description is notified to the user through assistive technologies. |
| aria-labelledby | The Dialog title is notified to the user through assistive technologies. |
| aria-modal | For modal dialog it's value is true and non-modal dialog its value is false |
| aria-grabbed | Enable the draggable Dialog and starts dragging it is value is true and stopping the drag its value is false |

## Keyboard interaction

Keyboard interaction of Dialog component has designed based on
[WAI-ARIA Practices](https://www.w3.org/TR/wai-aria-practices-1.1/#dialog_modal) described for Dialog.
User can use the following shortcut keys to interact with the Dialog.

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td>
<b>Keyboard shortcuts</b></td><td>
<b>Actions</b></td></tr>
<tr>
<td>
<kbd>Esc</kbd></td><td>
Closes the Dialog. This functionality can be controlled by using
[closeOnEscape](../api/dialog/#closeonescape) </td></tr>
<tr>
<td>
<kbd>Enter</kbd></td><td>
When the Dialog button or any input (except text area) is in focus state, when
pressing the Enter key, the click event associated with the primary button or button will
trigger. Enter key is not working when the Dialog content contains any text area with
initial focus</td></tr>
<tr>
<td>
<kbd>Ctrl + Enter</kbd></td><td>
When the Dialog content contains text area and it is in focus state, and press the Ctrl + Enter
key to call the click event
function associated with primary button</td></tr>
<tr>
<td>
<kbd>Tab</kbd></td><td>
Focus will be changed within the Dialog elements</td></tr>
<tr>
<td>
<kbd>Shift + Tab</kbd></td><td>
The Focus will be changed previous focusable element within the Dialog elements. When focusing a
first focusable element in the Dialog, then press the shift + tab key, it will change the focus
to last focusable element</td></tr>
</table>

{% tab template="dialog/keyboard", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
    <div #container class='root-container'></div>
      <ejs-dialog id='dialog' #ejDialog header='Feedback' [target]='targetElement'
      width='400px' [buttons]='buttons' showCloseIcon='true' height='300px'>
      <ng-template #content>
            <form>
                <div class='form-group'><label for='email'>Email:</label>
                    <input type='email' class='form-control' id='email'>
                </div>
                <div class='form-group'></div>
                <div class='form-group'>
                    <label for='comment'>Comments:</label>
                    <textarea style='resize: none;' class='form-control' rows='5' id='comment'></textarea>
                </div>
            </form>
      </ng-template>
      </ejs-dialog>
        `
})

export class AppComponent implements OnInit {
    @ViewChild('ejDialog') ejDialog: DialogComponent;
    // Create element reference for dialog target element.
    @ViewChild('container', { read: ElementRef }) container: ElementRef;

    public targetElement: HTMLElement;

    //To get all element of the dialog component after component get initialized.
    ngOnInit() {
      this.initilaizeTarget();
    }

    // Initialize the Dialog component target element.
    public initilaizeTarget: EmitType<object> = () => {
      this.targetElement = this.container.nativeElement.parentElement;
    }
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
              content:'Submit',
              isPrimary:true
            }
        }
    ];
    // Sample level code to handle the button click action
    public onOpenDialog = function (event: any): void {
        // Call the show method to open the Dialog
        this.ejDialog.show();
    }
}

```

{% endtab %}

## See Also

* [Show dialog with full-screen](./how-to/show-dialog-with-full-screen)
