---
title: "Bind the event to the buttons in footer"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Bind events to footer buttons

You can bind the actions to the buttons inside the footer using the buttons property. In the following example,dialog will be closed when you click on the buttons.

{% tab template="dialog/button-actions", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<div class="control-section">
 <button class='e-btn' id='dlgbtn' #ButtonInstance (click)="BtnClick()">Open</button>
    <!-- Render Button to open the Dialog -->
    <ejs-dialog #Dialog [buttons]='dlgButtons' [header]='header' [animationSettings]='animationSettings' [content]='content' [showCloseIcon]='showCloseIcon' [target]='target' [width]='width' (open)="dialogOpen()"
        (close)="dialogClose()">
    </ejs-dialog>
</div>`
})

export class AppComponent implements OnInit {
    @ViewChild('Dialog')
    public Dialog: DialogComponent;
    BtnClick() {
        this.Dialog.show();
    }
    public header: string = 'Delete Multiple Items';
    public content: string = 'Are you sure you want to permanently delete these items ?'
    public showCloseIcon: Boolean = true;
    public width: string = '50%';
    public animationSettings: Object = { effect: 'None' };
    public hide: any;
    ngAfterViewInit():void{
      document.getElementById('dlgbtn').focus();
    }

    // On Dialog close, 'Open' Button will be shown
    dialogClose() {
        document.getElementById('dlgbtn').style.display = '';
    }
    // On Dialog open, 'Open' Button will be hidden
    dialogOpen() {
        document.getElementById('dlgbtn').style.display = 'none';
    }

    public dlgButtons: Object[] = [{ click: this.dlgBtnClick.bind(this), buttonModel: { content: 'Yes', isPrimary:'true' } }, { click: this.dlgBtnClick.bind(this), buttonModel: { content: 'No' } }];
    dlgBtnClick() {
       this.Dialog.hide();
    }
    public target: string = '.control-section';
}

```

{% endtab %}

To access the current component within the button actions, add **bind(this)** along with function name in action binding.