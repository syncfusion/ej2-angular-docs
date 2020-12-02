# How to add custom button in toolbar

The toolbar items can be customized using the [toolbarSettings](../../api/file-manager/#toolbarsettings) API and [toolbarClick](../../api/file-manager/#toolbarclick) events.

The following example shows adding a custom item in the toolbar.

The new toolbar button is added using [toolbarSettings](../../api/file-manager/#toolbarsettings). The [toolbarClick](../../api/file-manager/#toolbarclick) event is used to add an event handler to the new toolbar button.

{% tab template="file-manager/toolbar", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarClickEventArgs , ToolbarCreateEventArgs} from '@syncfusion/ej2-filemanager';
import {FileManagerComponent} from '@syncfusion/ej2-angular-filemanager';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('fileManager')
    public fileManagerInstance: FileManagerComponent;
    public ajaxSettings: object;
    public toolbarSettings: object;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        this.toolbarSettings = {items: ['NewFolder', 'Custom', 'Upload', 'Delete', 'Download', 'Rename', 'SortBy', 'Refresh', 'Selection', 'View', 'Details']}
       };
    toolbarClick(args: ToolbarClickEventArgs) {
        if (args.item.text === 'Custom') {
            alert('You have clicked custom toolbar item')
        }
    }
    toolbarCreate(args: ToolbarCreateEventArgs) {
        for(var i=0;i<args.items.length;i++) {
            if(args.items[i].id === this.fileManagerInstance.element.id +'_tb_custom') {
                args.items[i].prefixIcon= 'e-icons e-fe-tick';
            }
        }
    }
}

```

{% endtab %}