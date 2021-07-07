# How to enable/disable toolbar item/items

The toolbar items can be enabled/disabled by specifying the items in [enableToolbarItems](../../api/file-manager/#enabletoolbaritems) or [disableToolbarItems](../../api/file-manager/#disabletoolbaritems) methods respectively.

The following example shows enabling and disabling toolbar items on button click.

{% tab template="file-manager/toolbar-items", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { FileManager } from '@syncfusion/ej2-filemanager';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    @ViewChild('fileManager')
    public fileManagerInstance: FileManager;
    public ajaxSettings: object;
    public height: number;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        this.height = "330px";
       };
    onCreated(args: any) {
        // Click event for enable button
        document.getElementById("enable").addEventListener('click', (event) => {
            // Enable new folder toolbar item
            this.fileManagerInstance.enableToolbarItems(["newfolder"]);
        });
        // Click event for disable button
        document.getElementById("disable").addEventListener('click', (event) => {
            // Disable new folder toolbar item
            this.fileManagerInstance.disableToolbarItems(["newfolder"]);
        });
    }
}

```

{% endtab %}
