# Nested FileManager

FileManager can be rendered inside the other components like Tab, Dialog, and more.

* [Adding file manager inside the dialog](#adding-file-manager-inside-the-dialog)
* [Adding  file manager inside the tab](#adding-file-manager-inside-the-tab)

## Adding file manager inside the dialog

The following example shows the file manager component rendered inside the dialog. Click the browse button in the Uploader element to open the File Manager inside the Dialog control.

{% tab template="file-manager/file-dialog", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component , ViewChild, Inject} from '@angular/core';
import { UploaderComponent } from '@syncfusion/ej2-angular-inputs';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { FileManagerComponent, FileOpenEventArgs } from '@syncfusion/ej2-angular-filemanager';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('uploadObj')
    public uploadObj: UploaderComponent;
    @ViewChild('dialogObj')
    public dialogObj: DialogComponent;
    @ViewChild('filemanagerObj')
    public filemanagerObj: FileManagerComponent;
    public dialogHeader = 'Select a file';
    public animationSettings: Object = { effect: 'None' };
    public showCloseIcon = true;
    public target = '#target';
    public visible = false;
    public dialogWidth = '850px';
    public ajaxSettings: object;
    public contextMenuSettings: object;
    public toolbarSettings: object;
    public hostUrl = 'https://ej2-aspcore-service.azurewebsites.net/';
    public contextmenuItems: string[] = ['Open', '|', 'Cut', 'Copy', 'Delete', 'Rename', '|', 'Details'];

    public btnClick: EmitType<object> = () => {
        this.dialogObj.show();
        this.dialogOpen();
        this.filemanagerObj.path = '/';
        this.filemanagerObj.selectedItems = [];
        this.filemanagerObj.refresh();
    }

    // Uploader will be hidden, if Dialog is opened
    public dialogOpen: EmitType<object> = () => {
        document.getElementById('uploadFileManager').style.display = 'none';
    }
    // Uploader will be shown, if Dialog is closed
    public dialogClose: EmitType<object> = () => {
        document.getElementById('uploadFileManager').style.display = 'block';
    }

    // File Manager's fileOpen event function
    public onFileOpen(args: FileOpenEventArgs): void {
        let file = (args as any).fileDetails;
        if (file.isFile) {
            args.cancel = true;
            if (file.size <= 0 ) { file.size = 10000; }
            this.uploadObj.files = [{name: file.name, size: file.size, type: file.type }];
            this.dialogObj.hide();
        }
    }

    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        this.toolbarSettings = {
            items: ['NewFolder', 'Upload', 'Delete', 'Cut', 'Copy', 'Rename', 'SortBy', 'Refresh', 'Selection', 'View', 'Details']
        };
        this.contextMenuSettings = {
            file: this.contextmenuItems,
            folder: this.contextmenuItems
        };
        this.uploadObj.autoUpload = true;
    }

    public ngOnDestroy(): void {
        if (document.querySelector('.sb-demo-section').classList.contains('upload-dialog')) {
            document.querySelector('.sb-demo-section').classList.remove('upload-dialog');
        }
    }
}

```

{% endtab %}

## Adding file manager inside the tab

The following example demonstrate that the file manager component is placed inside the content area of tab element.

{% tab template="file-manager/file-tab", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';
import { FileManagerComponent } from '@syncfusion/ej2-angular-filemanager';
import { TabAllModule } from '@syncfusion/ej2-angular-navigations';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public headerText: Object = [{ text: 'Overview' }, { text: 'FileManager' }];
    public ajaxSettings: object;
    // Mapping Tab items showCloseButton property
    public enableClose: boolean = true;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
    };
}

```

{% endtab %}