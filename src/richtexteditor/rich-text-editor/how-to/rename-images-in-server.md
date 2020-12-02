---
title: "How To rename uploaded images before inserting in RichTextEditor"
component: "Rich Text Editor"
description: "This section for Syncfusion Angular Rich Text Editor component explains on how to rename images in server and get the updated name for the image."
---

# Rename uploaded images in server before inserting it in the RichTextEditor

By using the [`insertImageSettings`](./../../api/rich-text-editor/imageSettings/#imageSettings) property, you can specify the server handler to upload the selected image. Then, you can bind the [`imageUploadSuccess`](./../../api/rich-text-editor/imageSuccessEventArgs/#imageSuccessEventArgs) event, to receive the modified file name from the server and update it in the Rich Text Editor's insert image dialog.

```HTML

<ejs-richtexteditor id='defaultRTE' #sample [insertImageSettings]='insertImageSettings' [toolbarSettings]='toolbarSettings' (imageUploadSuccess)='onImageUploadSuccess($event)'>
    <ng-template #valueTemplate>
    <p>The Rich Text Editor triggers events based on its actions. </p>
    <p> The events can be used as an extension point to perform custom operations.</p>
    <ul>
      <li>created - Triggers when the component is rendered.</li>
      <li>change - Triggers only when Rich Text Editor is blurred and changes are done to the content.</li>
      <li>focus - Triggers when Rich Text Editor is focused in.</li>
      <li>blur - Triggers when Rich Text Editor is focused out.</li>
      <li>actionBegin - Triggers before command execution using toolbar items or executeCommand method.</li>
      <li>actionComplete - Triggers after command execution using toolbar items or executeCommand method.</li>
      <li>destroyed – Triggers when the component is destroyed.</li>
    </ul>
    </ng-template>
</ejs-richtexteditor>

```

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, RichTextEditorComponent  } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
    templateUrl: 'app.compoenent.html',
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService ]
})
export class AppComponent  {
@ViewChild('sample') public rteObj: RichTextEditorComponent;

public toolbarSettings: Object = {
  items: ['Bold', 'Italic', 'Underline', 'StrikeThrough','|',
      'FontName', 'FontSize', 'FontColor', 'BackgroundColor',
      'LowerCase', 'UpperCase', '|',
      'Formats', 'Alignments', 'OrderedList', 'UnorderedList',
      'Outdent', 'Indent', '|',
      'CreateLink', 'Image', '|', 'ClearFormat', 'Print',
      'SourceCode', 'FullScreen', '|', 'Undo', 'Redo']
};
public insertImageSettings: object = {
    saveUrl: "[SERVICE_HOSTED_PATH]/api/uploadbox/Rename",
    path: "../Images/"
};

public onImageUploadSuccess = (args: any) => {
    if (args.e.currentTarget.getResponseHeader('name') != null) {
        args.file.name = args.e.currentTarget.getResponseHeader('name');
        let filename: any = document.querySelectorAll(".e-file-name")[0];
        filename.innerHTML = args.file.name.replace(document.querySelectorAll(".e-file-type")[0].innerHTML, '');
        filename.title = args.file.name;
    }
}

```

To configure the server-side handler, refer the below code.

```csharp
[AcceptVerbs("Post")]
public void Rename()
{
    try
    {
        var httpPostedFile = System.Web.HttpContext.Current.Request.Files["UploadFiles"];
        imageFile = httpPostedFile.FileName;
        if (httpPostedFile != null)
        {
            var fileSave = System.Web.HttpContext.Current.Server.MapPath("~/Images");
            if (!Directory.Exists(fileSave))
            {
                Directory.CreateDirectory(fileSave);
            }
            var fileName = Path.GetFileName(httpPostedFile.FileName);
            var fileSavePath = Path.Combine(fileSave, fileName);
            while (System.IO.File.Exists(fileSavePath))
            {
                imageFile = "rteImage" + x + "-" + fileName;
                fileSavePath = Path.Combine(fileSave, imageFile);
                x++;
            }
            if (!System.IO.File.Exists(fileSavePath))
            {
                httpPostedFile.SaveAs(fileSavePath);
                HttpResponse Response = System.Web.HttpContext.Current.Response;
                Response.Clear();
                Response.Headers.Add("name", imageFile);
                Response.ContentType = "application/json; charset=utf-8";
                Response.StatusDescription = "File uploaded succesfully";
                Response.End();
            }
        }
    }
    catch (Exception e)
    {
        HttpResponse Response = System.Web.HttpContext.Current.Response;
        Response.Clear();
        Response.ContentType = "application/json; charset=utf-8";
        Response.StatusCode = 204;
        Response.Status = "204 No Content";
        Response.StatusDescription = e.Message;
        Response.End();
    }
}

```
