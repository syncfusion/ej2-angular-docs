# Open a dialog on ContextMenu item click

This section explains about how to open a dialog on ContextMenu item click. This can be achieved by
handling dialog open in `select` event of the ContextMenu.

In the following sample, Dialog will open while clicking `Save As...` item:

{% tab template="context-menu/dialog", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { MenuItemModel, MenuEventArgs } from '@syncfusion/ej2-navigations';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';

@Component({
  selector: 'app-root',
  template: `<div id="target">Right click / Touch hold to open the ContextMenu</div>
  <ejs-dialog #dialog [buttons]='alertDlgButtons' [visible]='visible' content='This file can be saved as PDF' width='200px' height='110px' [position]='position'>
  </ejs-dialog>
  <ejs-contextmenu target="#target" [items]="data" (select)="itemSelect($event)"></ejs-contextmenu>`
})

export class AppComponent {
  @ViewChild('dialog')
  public alertDialog: DialogComponent;

  name = 'Angular';
  data= [
  {
    text: 'Back'
  },
  {
    text: 'Forward'
  },
  {
    text: 'Reload'
  },
  {
    separator: true
  },
  {
    text: 'Save As...'
  },
  {
    text: 'Print'
  },
  {
    text: 'Cast'
  }
  ];

  public visible: Boolean = false;

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

  public itemSelect(args: MenuEventArgs): void {
    if (args.item.text === "Save As...") {
      this.alertDialog.show();
    }
  }
}

```

{% endtab %}
