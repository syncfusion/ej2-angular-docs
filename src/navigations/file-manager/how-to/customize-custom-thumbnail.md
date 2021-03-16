# How to add custom thumbnail in file manager

The default appearance of the file manager can customize with your own icon by using [showThumbnail](../../api/file-manager/#showthumbnail) property.

The following example demonstrate how to add a custom icon in largeicons view.

{% tab template="file-manager/custom-thumbnail", isDefaultActive = "true",sourceFiles="app/**/*.ts,app/app.component.html,app/app.component.css" %}

```typescript

import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['app/app.component.css'],
    templateUrl: 'app/app.component.html'
})
export class AppComponent {
    public ajaxSettings: object;
    public showThumbnail: boolean;
    public hostUrl: string = 'https://ej2-aspcore-service.azurewebsites.net/';
    public ngOnInit(): void {
        this.ajaxSettings = {
            url: this.hostUrl + 'api/FileManager/FileOperations',
            getImageUrl: this.hostUrl + 'api/FileManager/GetImage',
            uploadUrl: this.hostUrl + 'api/FileManager/Upload',
            downloadUrl: this.hostUrl + 'api/FileManager/Download'
        };
        this.showThumbnail = false;
       }
}

```

{% endtab %}