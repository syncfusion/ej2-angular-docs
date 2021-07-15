---
title: "Achieve invisible upload"
component: "Uploader"
description: "Covers customizable features of the file upload control such as a preview image, invisible upload, progress bar, sort the file list and more."
---

# Achieve invisible upload

You can achieve the invisible upload feature by using selected event in uploader component.
Refer to the following example.

{% tab template="uploader/invisible",  sourceFiles="app/**/*.ts,default.html,index.css" %}

```typescript
import { Component } from '@angular/core';
import { createElement } from '@syncfusion/ej2-base';
import { SelectedEventArgs } from '@syncfusion/ej2-angular-inputs';

/**
 * Default Uploader Default Component
 */
@Component({
    selector: 'app-root',
    templateUrl: 'default.html',
    styleUrls: ['index.css']
})
export class AppComponent {

    public path: Object = {
        saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
        removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove'
    };
  public allowExtensions: string = '.png, .jpg, .jpeg';
  public onSelected(args: SelectedEventArgs):void {
    for(let i = 0; i< args.filesData.length ; i++){
        let liparentDiv = createElement('div',  { className: 'image-list'});
        let liImage = createElement('img',  { className: 'image'});
        liparentDiv.appendChild(liImage);
        this.readURL(liImage, args.filesData[i]);
        document.getElementById('preview').appendChild(liparentDiv);
    }
    args.cancel=true;
}

public readURL(liImage: HTMLElement, file: any):void {
    let imgPreview: HTMLImageElement = liImage as HTMLImageElement;
    let imageFile: File = file.rawFile;
    let reader: FileReader = new FileReader();
    reader.addEventListener( 'load', () => {
        imgPreview.src = reader.result;
    }, false);
    if (imageFile) {
        reader.readAsDataURL(imageFile);
    }
};
}
```

{% endtab %}

> You can also explore [Angular File Upload](https://www.syncfusion.com/angular-ui-components/angular-file-upload) feature tour page for its groundbreaking features. You can also explore our [Angular File Upload example](https://ej2.syncfusion.com/angular/demos/#/material/uploader/default) to understand how to browse the files which you want to upload to the server.
