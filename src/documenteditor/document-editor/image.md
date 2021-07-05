---
title: "Images"
component: "DocumentEditor"
description: "Learn the supported image types in JavaScript document editor and how to insert, resize, format images."
---

# Images

Document editor supports common raster format images like PNG, BMP, JPEG, and GIF. You can insert an image file or online image in the document using the `insertImage()` method. Refer to the following sample code.

{% tab template="document-editor/link",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, EditorService, SelectionService, SfdtExportService, EditorHistoryService, ImageResizerService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="width:100%;height:330px">
    <input id="insertImageButton" #insert_Image_Button style="position:fixed; left:-100em" type="file" (change)="onInsertImage($event)" accept=".jpeg,.jpg,.png,.gif,.bmp">
    <button ejs-button (click)="insertImageButtonClick()" >Insert Image</button>
    <ejs-documenteditor #document_editor  id="container" style="width:100%;height:100%;display:block"  [enableSfdtExport]=true [enableWordExport]=true [enableSelection]=true [enableEditor]=true [isReadOnly]=false [enableImageResizer]=true> </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [EditorService, SelectionService, SfdtExportService, ImageResizerService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public insertImageButtonClick() :void {
    let pictureUpload: HTMLInputElement = document.getElementById("insertImageButton") as HTMLInputElement;
    pictureUpload.value = '';
    pictureUpload.click();
 }

 public onInsertImage(args: any): void {
    let documentEditor: DocumentEditorComponent =  this.documentEditor;
    if (navigator.userAgent.match('Chrome') || navigator.userAgent.match('Firefox') || navigator.userAgent.match('Edge') || navigator.userAgent.match('MSIE') || navigator.userAgent.match('.NET')) {
        if (args.target.files[0]) {
            let path = args.target.files[0];
            let reader = new FileReader();
            reader.onload = function (frEvent: any) {
                let base64String = frEvent.target.result;
                let image = document.createElement('img');
                image.addEventListener('load', function () {
                   documentEditor.editor.insertImage(base64String, this.width, this.height);
                })
                image.src = base64String;
            };
            reader.readAsDataURL(path);
        }
        //Safari does not Support FileReader Class
    } else {
        let image = document.createElement('img');
        image.addEventListener('load', function () {
             documentEditor.editor.insertImage(args.target.value);
        })
        image.src = args.target.value;
    }
}

}
```

{% endtab %}

Image files will be internally converted to base64 string. Whereas, online images are preserved as URL.

## Image resizing

Document editor provides built-in image resizer that can be injected into your application based on the requirements. This allows you to resize the image by dragging the resizing points using mouse or touch interactions. This resizer appears as follows.

![Image](images/image.png)

## Changing size

Document editor expose API to get or set the size of the selected image. Refer to the following sample code.

```typescript
this.documentEditor.selection.imageFormat.width = 800;
this.documentEditor.selection.imageFormat.height = 800;
```

>Note: Images are stored and processed(read/write) as base64 string in DocumentEditor. The online image URL is preserved as a URL in DocumentEditor upon saving.

## Text wrapping style

Text wrapping refers to how images fit with surrounding text in a document. Please [refer to this page](../document-editor/text-wrapping-style) for more information about text wrapping styles available in Word documents.

## Positioning the image

DocumentEditor preserves the position properties of the image and displays the image based on position properties. It does not support modifying the position properties. Whereas the image will be automatically moved along with text edited if it is positioned relative to the line or paragraph.

## See Also

* [Feature modules](../document-editor/feature-module/)
