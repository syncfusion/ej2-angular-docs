---
title: "Open a dialog on popup item click"
component: "SplitButton"
description: "Angular SplitButton how to section, group popup items using list view component, dialog open on popup item click."
---

# Open a dialog on popup item click

This section explains about how to open a dialog on SplitButton popup item click. This can be achieved by
handling dialog open in [`select`](../../api/split-button#select) event of the SplitButton.

In the following example, Dialog will open while selecting `Update...` item:

{% tab template="split-button/dialog", sourceFiles="app/**/*.ts", isDefaultActive=true %}

 ```typescript
import { Component, ViewChild } from '@angular/core';
import { ItemModel, MenuEventArgs  } from '@syncfusion/ej2-angular-splitbuttons';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';

@Component({
    selector: 'app-root',
    template: `<!-- To render Dialog. -->
               <ejs-dialog #dialog [buttons]='alertDlgButtons' [visible]='false' content='Are you sure want to update?' width='250px' header='Software Update'>
               </ejs-dialog>
               <!-- To Render splitbutton. -->
               <ejs-splitbutton content="Help" [items]='items' (select)='select($event)'></ejs-splitbutton>`
})

export class AppComponent {
    @ViewChild('dialog')
    public alertDialog: DialogComponent;

    public items: ItemModel[] = [
    {
        text: 'Help'
    },
    {
        text: 'About'
    },
    {
        text: 'Update...'
    }];

    public alertDlgButtons: Object[] = [{
        buttonModel: {
            isPrimary: true,
            content: 'Ok',
        },
        click: function () {
            this.hide();
        }
    },
    {
        buttonModel: {
            isPrimary: true,
            content: 'Cancel',
        },
        click: function () {
            this.hide();
        }
    }];

    public select (args: MenuEventArgs) {
        if (args.item.text === 'Update...') {
            this.alertDialog.show();
        }
    }
}
```

{% endtab %}