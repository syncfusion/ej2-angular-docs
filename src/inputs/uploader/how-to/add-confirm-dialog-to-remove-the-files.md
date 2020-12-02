---
title: "Add confirm dialog to remove the files"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Add confirm dialog to remove the files

You can customize the uploader component using confirm dialog before removing the files.
Here, ej2 dialog is used as confirm dialog. Refer to the following example.

{% tab template="uploader/confirm-dialog", sourceFiles="app/**/*.ts,default.html,index.css" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { EmitType } from '@syncfusion/ej2-base';
import { UploaderComponent, SelectedEventArgs } from '@syncfusion/ej2-angular-inputs';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
@Component({
    selector: 'app-root',
    templateUrl: 'default.html',
    styleUrls: ['index.css']
})

export class AppComponent {
  @ViewChild('defaultupload') uploadObj: UploaderComponent;
  @ViewChild('dialog') dialog: DialogComponent;

   public path: Object = {
       saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
       removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove'
   };
   public removeFile: any = [];
   public content: string = 'Confirm to remove the file?';
   public width: string = '250px';
   public visible: boolean = false;
   public target: string = '#container';
   public buttons: Object = [{'click': this.onClick.bind(this), buttonModel: { content: 'OK', cssClass: 'e-flat', isPrimary: true}},
   {'click': () => {this.dialog.hide(); }, buttonModel: { content: 'Cancel', cssClass: 'e-flat'} }];
   public onremoving: EmitType<SelectedEventArgs> = (args: any) =>  {
    args.cancel = true;
    this.removeFile.push(args.filesData);
    this.dialog.show();
   };
   onClick() {
    this.dialog.hide();
    this.uploadObj.remove(this.removeFile, true);
    this.removeFile = [];
   }
}
```

{% endtab %}
