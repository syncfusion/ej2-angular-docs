---
title: "Display a dialog with custom position"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Display a Dialog with custom position

By default, the dialog is displayed in the center of the target container. The dialog position can be set using the position property by providing custom X and Y coordinates.
The dialog can be positioned inside the target based on the given X and Y values.

{% tab template="dialog/dlg-position", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <div #container class='root-container'>
        <ejs-dialog id='firstDialog' #ejDialog header='Position-01' content='The dialog is positioned at {X: 160, Y: 14 } coordinates.' [target]='targetElement'
        width='360px' height='120px' [position]='position1'>
        </ejs-dialog>
        <ejs-dialog id='secondDialog' #ejDialog1 header='Position-02' content='The dialog is positioned at {X: 160, Y: 240} coordinates.' [target]='targetElement'
        width='360px' height='120px' [position]='position2'>
        </ejs-dialog>
      </div> `
})

export class AppComponent implements OnInit {
    @ViewChild('ejDialog') ejDialog: DialogComponent;
    @ViewChild('ejDialog1') ejDialog1: DialogComponent;
    // Create element reference for dialog target element.
    @ViewChild('container', { read: ElementRef }) container: ElementRef;
    // The Dialog shows within the target element.
    public targetElement: HTMLElement;

    //To get all element of the dialog component after component get initialized.
    ngOnInit() {
      this.initilaizeTarget();
    }
    // Set Dialog position
    public position1: object={ X: 160, Y: 14 };
    public position2: object={ X: 160, Y: 240 };

    // Initialize the Dialog component's target element.
    public initilaizeTarget: EmitType<object> = () => {
      this.targetElement = this.container.nativeElement.parentElement;
    }
}

```

{% endtab %}
