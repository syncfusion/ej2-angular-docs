# How to add custom menu item in context menu

The context menu can be customized using the [contextMenuSettings](../../api/file-manager/#contextmenusettings), [menuOpen](../../api/file-manager/#menuopen), and [menuClick](../../api/file-manager/#menuclick) events.

The following example shows adding a custom item in the context menu.

The [contextMenuSettings](../../api/file-manager/#contextmenusettings) is used to add new menu item. The [menuOpen](../../api/file-manager/#menuopen) event is used to add the icon to the new menu item. The [menuClick](../../api/file-manager/#menuclick) event is used to add an event handler to the new menu item.

{% tab template="file-manager/contextmenu", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html" %}

```typescript

import { Component } from '@angular/core';
import { MenuOpenEventArgs, MenuClickEventArgs } from '@syncfusion/ej2-filemanager';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public contextMenuSettings: object;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        this.contextMenuSettings = {
            file: ['Custom', 'Open', '|', 'Delete', 'Rename', '|', 'Details'],
            folder: ['Custom', 'Open', '|', 'Delete', 'Rename', '|', 'Details','Custom'],
            layout: ['Custom', 'SortBy', 'View', 'Refresh', '|', 'NewFolder', 'Upload', '|', 'Details', '|', 'SelectAll'],
            visible: true
        };
    }
menuOpen(args: MenuOpenEventArgs) {
   for(var i=0;i<args.items.length;i++) {
        if (args.items[i].text === 'Custom') {
            args.items[i].iconCss= 'e-icons e-fe-tick';
        }
    }
}

// event for custom menu item
menuClick(args: MenuClickEventArgs) {
    if (args.item.text === 'Custom') {
        alert('You have clicked custom menu item')
    }
}
}

```

{% endtab %}
