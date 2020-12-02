---
title: "Rich Text Editor file attachments"
component: "Rich Text Editor"
description: "This section for Syncfusion Angular Rich Text Editor component explains on how to attach the files."
---

# File Attachments

The Rich Text Editor allows you to attach a file based on the file upload. You can attach your files using the file upload or drag-and-drop from your local path. When the file upload gets success, the attachment link inserts into the content.

In the below sample, configure the saveUrl and path properties to achieve file attachments.

        1. saveUrl: Provides service URL to save the files.
        2. path: Specifies the location to store the image.

The following sample illustrates how to attach a file in the RichTextEditor.

```html
<ejs-richtexteditor id='defaultRTE' #sample [insertImageSettings]='insertImageSettings'>
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

<ejs-uploader #defaultupload id='defaultfileupload' [asyncSettings]='path' [dropArea]='dropElement' (success)='onImageUploadSuccess($event)'></ejs-uploader>
```

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, RichTextEditorComponent , NodeSelection } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
    templateUrl: 'app.compoenent.html',
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService , NodeSelection ]
})
export class AppComponent  {
@ViewChild('sample') public rteObj: RichTextEditorComponent;
@ViewChild('defaultupload')  public uploadObj: uploaderComponent;

public insertImageSettings: object = {
    saveUrl: "[SERVICE_HOSTED_PATH]/api/uploadbox/Save",
    path: "../Files/"
};

    public path: Object = {
        saveUrl: '[SERVICE_HOSTED_PATH]/api/uploadbox/Save',
    };
     public dropElement ='#defaultRTE'
  public selection: NodeSelection = new NodeSelection();
    public range: Range;
    public saveSelection: NodeSelection;
  public onImageUploadSuccess = (args: any) => {  
      this.rteObj.contentModule.getEditPanel().focus();
        this.range = this.selection.getRange(document);
        this.saveSelection = this.selection.save(this.range, document);
        var fileUrl = document.URL + this.rteObj.insertImageSettings.path + args.file.name;
        if (rteObj.formatter.getUndoRedoStack().length === 0) {
            rteObj.formatter.saveData();
        }
        saveSelection.restore();
        rteObj.executeCommand('createLink', { url: fileUrl, text: fileUrl, selection: saveSelection });
        rteObj.formatter.saveData();
        rteObj.formatter.enableUndo(rteObj);
        this.uploadObj.clearAll();
}
}

```

To config server-side handler, refer the below code.

``` csharp
int x = 0;
string file;
 [AcceptVerbs("Post")]
        public void Save()
        {
            try
            {
                var httpPostedFile = System.Web.HttpContext.Current.Request.Files["UploadFiles"];
                file = httpPostedFile.FileName;
                if (httpPostedFile != null)
                {
                    Console.WriteLine(System.Web.HttpContext.Current.Server.MapPath("~/Files"));
                    var fileSave = System.Web.HttpContext.Current.Server.MapPath("~/Files");
                    if (!Directory.Exists(fileSave))
                    {
                        Directory.CreateDirectory(fileSave);
                    }
                    var fileName = Path.GetFileName(httpPostedFile.FileName);
                    var fileSavePath = Path.Combine(fileSave, fileName);
                    while (System.IO.File.Exists(fileSavePath))
                    {
                        file = "rte" + x + "-" + fileName;
                        fileSavePath = Path.Combine(fileSave, file);
                        x++;
                    }
                    if (!System.IO.File.Exists(fileSavePath))
                    {
                        httpPostedFile.SaveAs(fileSavePath);
                        HttpResponse Response = System.Web.HttpContext.Current.Response;
                        Response.Clear();
                        Response.Headers.Add("name", file);
                        Response.ContentType = "application/json; charset=utf-8";
                        Response.StatusDescription = "File uploaded succesfully";
                        Response.Headers.Add("url", fileSavePath);
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