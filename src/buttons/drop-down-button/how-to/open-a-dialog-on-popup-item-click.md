---
title: "Open a dialog on popup item click"
component: "DropDownButton"
description: "Angular DropDownButton how to section, hide drop down arrow, group popup items using list view component, dialog open on popup item click."
---

# Open a dialog on popup item click

This section explains about how to open a dialog on DropdownButton popup item click.
This can be achieved by handling dialog open in
[`select`](../../api/drop-down-button#select) event of the DropdownButton.

In the following example, Dialog will open while selecting `Other Folder...` item.

{% tab template="drop-down-button/dialog", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ItemModel, MenuEventArgs, DropDownButtonComponent  } from '@syncfusion/ej2-angular-splitbuttons';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';

@Component({
    selector: 'app-root',
    template: `<!-- To render Dialog. -->
               <ejs-dialog #dialog [buttons]='alertDlgButtons' [visible]='false' content='Move Items To "Web Team"' width='250px' [position]='position'>
                </ejs-dialog>
                <!-- To render DropDownButton. -->
               <button ejs-dropdownbutton #dropdownbutton [items]='items' content='Move' iconCss='ddb-icons e-folder' cssClass='e-vertical' iconPosition='Top' (select)='select($event)'></button>`
})

export class AppComponent {
  @ViewChild('dialog')
  public alertDialog: DialogComponent;
  @ViewChild('dropdownbutton')
  public dropdownbutton: DropDownButtonComponent;

  public position: any = {X: 100, Y: 100};

  public alertDlgButtons: Object[] = [{
    buttonModel: {
        isPrimary: true,
        content: 'Submit',
        cssClass: 'e-flat',
    },
    click: function () {
        this.hide();
    }
  }];
   // Initialize action items.
   public items: ItemModel[] = [
    {
        text: 'Archive'
    },
    {
        text: 'Inbox'
    },
    {
        text: 'HR Portal'
    },
    {
        separator: true
    },
    {
        text: 'Other Folder...'
    },
    {
        text: 'Copy to Folder'
    }];
    // To open dialog on selecting `Other Folder...` item.
    public select (args: MenuEventArgs) {
       if (args.item.text === 'Other Folder...') {
        this.alertDialog.show();
      }
    }

}

```

{% endtab %}