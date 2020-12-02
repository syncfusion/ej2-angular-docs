---
title: "Template"
component: "Uploader"
description: "Explains how to customize the file list with action buttons using a template that helps to design own user interface in the file upload control."
---

# Template

You can customize the default appearance of the uploader using a template along with buttons.

## File list template

The `template` property is used to customize the default appearance of each file in the list.
It can be represented as the HTML element or string. The selected or dropped files are displayed as per the template layout provided.
The remove and progress bar action is handled using the corresponding events when the template is defined.

For example, you can display file type icon along with default UI elements.

{% tab template="uploader/template", sourceFiles="app/**/*.ts, index.css"  %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { detach } from '@syncfusion/ej2-base';
import { UploaderComponent, FileInfo, SelectedEventArgs } from '@syncfusion/ej2-angular-inputs';

/**
 * Uploader Custom Template sample
 */
@Component({
    selector: 'app-root',
    template: `<div id='dropArea'><span id='drop' class="droparea"> Drop files here or <a href="" id='browse'><u>Browse</u></a> </span>
    <ejs-uploader #defaultupload autoUpload='false'  [asyncSettings]='path' (selected)="onSelect($event)" (failure)="onuploadFailed($event)" (progress)="onFileUpload($event)" (success)="onuploadSuccess($event)">
    <ng-template #template let-data="">
          <span class='wrapper'><span class='icon sf-icon-{{data.type}}'></span>
          <span class='name file-name'>{{data.name}}</span></span>
          <span class='file-size-td file-size'>{{data.size}} bytes</span>
          <span class='e-icons e-file-remove-btn' title='Remove'></span> <br/>
          <progress id='progressBar' class='progressbar' value='0' max='100'></progress>
          <span class='percent-td percent'></span>
      </ng-template>
</ejs-uploader>
    </div> `,
    styleUrls: ['index.css']
})
export class AppComponent {
     @ViewChild('defaultupload')
    public uploadObj: UploaderComponent;
    public path: Object = {
      saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
      removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove' };
    constructor() {
    }
     ngAfterViewInit() {
      document.getElementById('browse').onclick = function() {
      document.getElementsByClassName('e-file-select-wrap')[0].querySelector('button').click();
        return false;
      }
      document.getElementById('dropArea').onclick = (e: any) => {
            let target: HTMLElement = <HTMLElement>e.target;
            if (target.classList.contains('e-file-delete-btn')) {
                for (let i: number = 0; i < this.uploadObj.getFilesData().length; i++) {
                    if (target.closest('li').getAttribute('data-file-name') === this.uploadObj.getFilesData()[i].name) {
                        this.uploadObj.remove(this.uploadObj.getFilesData()[i]);
                    }
                }
            }
            else if (target.classList.contains('e-file-remove-btn')) {
                detach(target.closest('li'));
            }
        }
    }
   public parentElement : HTMLElement;
    public progressbarContainer : HTMLElement;
    public filesDetails : FileInfo[] = [];
    public filesList: HTMLElement[] = [];
    public dropElement: HTMLElement = document.getElementsByClassName('control-fluid')[0] asHTMLElement;public onFileUpload(args: any) {
    let li: HTMLElement = this.uploadObj.uploadWrapper.querySelector('[data-file-name="' + args.file.name + '"]');
    let progressValue: number = Math.round((args.e.loaded / args.e.total) * 100);
    li.getElementsByTagName('progress')[0].value = progressValue;
    li.getElementsByClassName('percent')[0].textContent = progressValue.toString() + " %";
  }
  public onuploadSuccess(args: any) {
    if (args.operation === 'remove') {
        let height: string = document.getElementById('dropArea').style.height;
        height = (parseInt(height) - 40) + 'px';
        document.getElementById('dropArea').style.height = height;
    } else {
        let li: HTMLElement = this.uploadObj.uploadWrapper.querySelector('[data-file-name="' + args.file.name + '"]');
        let progressBar: HTMLElement = li.getElementsByTagName('progress')[0];
        progressBar.classList.add('e-upload-success');
        li.getElementsByClassName('percent')[0].classList.add('e-upload-success');
        let height: string = document.getElementById('dropArea').style.height;
        document.getElementById('dropArea').style.height = parseInt(height) - 15 + 'px';
    }
}
public onuploadFailed(args: any) {
    let li: HTMLElement = this.uploadObj.uploadWrapper.querySelector('[data-file-name="' + args.file.name + '"]');
    let progressBar: HTMLElement = li.getElementsByTagName('progress')[0];
    progressBar.classList.add('e-upload-failed');
    li.getElementsByClassName('percent')[0].classList.add('e-upload-failed');
}
public onSelect(args: SelectedEventArgs) {
    let length: number = args.filesData.length;
    let height: string = document.getElementById('dropArea').style.height;
    height = parseInt(height) + (length * 55) + 'px';
    document.getElementById('dropArea').style.height = height;
}
}
```

{% endtab %}

## Custom template

You can design the own template by preventing the default file list including buttons.
The `showFileList` property is used to display whether the default file list or own file list when you use
custom template to upload or remove the files, pass the custom UI argument as true to call
`upload`/`remove` public method as follows:

* UploaderObj.upload(filesData, true);

* UploaderObj.remove(filesData, true);

Refer to the following code sample.

{% tab template="uploader/cus_template", sourceFiles="app/**/*.ts, index.css"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { EmitType, detach, isNullOrUndefined, createElement, EventHandler } from '@syncfusion/ej2-base';
import { UploaderComponent, FileInfo, SelectedEventArgs, RemovingEventArgs  } from '@syncfusion/ej2-angular-inputs';
import { createSpinner, showSpinner, hideSpinner  } from '@syncfusion/ej2-popups';

@Component({
    selector: 'app-root',
    template: `<div id='dropArea'>
                    <span id='drop' class="droparea"> Drop files here or <a href="" id='browse'><u>Browse</u></a> </span>
                    <ejs-uploader #templateupload id='templatefileupload' [asyncSettings]='path'(progress)='onFileUpload($event)' (selected)='onFileSelect($event)' (removing)='onFileRemove($event)' (failure)='onUploadFailed($event)' (success)='onUploadSuccess($event)'></ejs-uploader>
                </div>`,
    styleUrls: ['index.css']
})
export class AppComponent {
    @ViewChild('templateupload')
    public uploadObj: UploaderComponent;

    public path: Object = {
        saveUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Save',
        removeUrl: 'https://ej2.syncfusion.com/services/api/uploadbox/Remove'
    };

    ngAfterViewInit() {
    document.getElementById('browse').onclick = function() {
    document.getElementsByClassName('e-file-select-wrap')[0].querySelector('button').click();
      return false;
      }
    }
    constructor() {
    }
    public uploadWrapper: HTMLElement = document.getElementsByClassName('e-upload')[0] as HTMLElement;
    public parentElement : HTMLElement;
    public progressbarContainer : HTMLElement;
    public filesDetails : FileInfo[] = [];
    public filesList: HTMLElement[] = [];
    public onFileSelect(args : SelectedEventArgs) : void  {
        if (isNullOrUndefined(document.getElementById('dropArea').querySelector('.upload-list-root'))) {
            this.parentElement = createElement('div', { className: 'upload-list-root' });
            this.parentElement.appendChild(createElement('ul', {className: 'ul-element' }));
            document.getElementById('dropArea').appendChild(this.parentElement);
        }
        for (let i : number = 0; i < args.filesData.length; i++) {
            this.formSelectedData(args.filesData[i], this);  // create the LI element for each file Data
        }
        this.filesDetails = this.filesDetails.concat(args.filesData);
        this.uploadObj.upload(args.filesData, true);
        args.cancel = true;
    }
     public formSelectedData (selectedFiles : FileInfo, proxy: any ) : void {
        let liEle : HTMLElement = createElement('li',  { className: 'file-lists', attrs: {'data-file-name' : selectedFiles.name} });
        liEle.appendChild(createElement('span', {className: 'file-name ', innerHTML: selectedFiles.name }));
        liEle.appendChild(createElement('span', {className: 'file-size ', innerHTML: this.uploadObj.bytesToSize(selectedFiles.size) }));
        if (selectedFiles.status === 'Ready to upload') {
            this.progressbarContainer = createElement('span', {className: 'progress-bar-container'});
            this.progressbarContainer.appendChild(createElement('progress', {className: 'progress', attrs: {value : '0', max : '100'}} ));
            liEle.appendChild(this.progressbarContainer);
        } else { liEle.querySelector('.file-name').classList.add('upload-fails'); }
        let closeIconContainer : HTMLElement = createElement('span', {className: 'e-icons close-icon-container'});
        EventHandler.add(closeIconContainer, 'click', this.removeFiles, proxy);
        liEle.appendChild(closeIconContainer);
        document.querySelector('.ul-element').appendChild(liEle);
        this.filesList.push(liEle);
    }

    public onFileUpload(args : any) : void {
        let li : Element = document.getElementById('dropArea').querySelector('[data-file-name="' + args.file.name + '"]');
        EventHandler.remove(li.querySelector('.close-icon-container'), 'click', this.removeFiles);
        let progressValue : number = Math.round((args.e.loaded / args.e.total) * 100);
        if (!isNaN(progressValue)) {
            li.getElementsByTagName('progress')[0].value = progressValue;   // Updating the progress bar value
        }
    }

    public onUploadSuccess:  EmitType<Object> = (args: any) => {
        let spinnerElement: HTMLElement = document.getElementById('dropArea');
        let li: HTMLElement =  document.getElementById('dropArea').querySelector('[data-file-name="' + args.file.name + '"]');
        if (args.operation === 'upload') {
            let progressBar: HTMLElement = li.getElementsByTagName('progress')[0];
            li.querySelector('.close-icon-container').classList.add('delete-icon');
            detach(li.getElementsByTagName('progress')[0]);
            (li.querySelector('.file-size') as HTMLElement).style.display = 'inline-block';
            (li.querySelector('.file-name') as HTMLElement).style.color = 'green';
            (li.querySelector('.e-icons') as HTMLElement).onclick = () => {
                createSpinner({ target: spinnerElement, width: '25px' });
                showSpinner(spinnerElement);
            };
            (li.querySelector('.close-icon-container') as HTMLElement).onkeydown = (e: any) => {
                if (e.keyCode === 13) {
                    createSpinner({ target: spinnerElement, width: '25px' });
                    showSpinner(spinnerElement);
                }
            };
        } else {
            this.filesList.splice(this.filesList.indexOf(li), 1);
            this.filesDetails.splice(this.filesList.indexOf(li), 1);
            detach(li);
            hideSpinner(spinnerElement);
            detach(spinnerElement.querySelector('.e-spinner-pane'));
        }
        EventHandler.add(li.querySelector('.close-icon-container'), 'click', this.removeFiles, this);
    }

    public onFileRemove(args: RemovingEventArgs): void {
        args.postRawFile = false;
    }

    public onUploadFailed(args : any) : void {
        let li : Element = document.getElementById('dropArea').querySelector('[data-file-name="' + args.file.name + '"]');
        EventHandler.add(li.querySelector('.close-icon-container'), 'click', this.removeFiles, this);
        li.querySelector('.file-name ').classList.add('upload-fails');
        if (args.operation === 'upload') {
            detach(li.querySelector('.progress-bar-container'));
        }
    }

    public removeFiles(args : any) : void {
        let status : string = this.filesDetails[this.filesList.indexOf(args.currentTarget.parentElement)].status;
        if (status === 'File uploaded successfully') {
            this.uploadObj.remove(this.filesDetails[this.filesList.indexOf(args.currentTarget.parentElement)]);
        } else {
            detach(args.currentTarget.parentElement);
        }
        this.uploadObj.element.value = '';
    }

    public generateSpinner(targetElement: HTMLElement): void {
        createSpinner({ target: targetElement, width: '25px' });
        showSpinner(targetElement);
    }
}

```

{% endtab %}

## See Also

* [Customize progress bar](./how-to/customize-progressbar)
* [Customize button with HTML element](./how-to/customize-button-with-html-element)
* [Customize drop area](./how-to/hide-default-drop-area)
