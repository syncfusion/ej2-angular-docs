---
title: "Angular Rich Text Editor Third Party Integration"
component: "Rich Text Editor"
description: "This section for Syncfusion's Angular Rich Text Editor component explains how to integrate additional third-party libraries to enhance the content."
---

# Third-Party Integration

The Rich Text Editor can be integrated with third-party to suite the application scenario.

## CodeMirror Integration

RichTextEditor comes with a basic HTML source editor through the view-source property. CodeMirror plugin can be used to highlight the syntax of HTML. CodeMirror plugin for Rich Text Editor makes editing of HTML source code with a pleasant experience.

Import necessary CSS and JS files of CodeMirror to the HTML page.

Required JS files of code mirror.

```typescript
 <script src="scripts/CodeMirror/codemirror.js" type="text/javascript"></script>
 <script src="scripts/CodeMirror/javascript.js" type="text/javascript"></script>
 <script src="scripts/CodeMirror/css.js" type="text/javascript"></script>
 <script src="scripts/CodeMirror/htmlmixed.js" type="text/javascript"></script>

```

Required CSS file of code mirror

```typescript
 <link href="scripts/CodeMirror/codemirror.min.css" rel="stylesheet" />
```

Add a custom icon for HTML source editor in the toolbar of Rich Text Editor using the template option of ToolbarSettings, define the code mirror plugins, and then pass the Rich Text Editor content as argument in the [`actionComplete`](../api/rich-text-editor/#actioncomplete) event.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
  import { Component, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, RichTextEditorComponent,CountService} from '@syncfusion/ej2-angular-richtexteditor';
import { createElement, addClass, removeClass, Browser } from '@syncfusion/ej2-base';

@Component({
selector: 'app-root',
template: `<ejs-richtexteditor #toolsRTE id='alltoolRTE' [toolbarSettings]='tools' [showCharCount]='true' (actionComplete)='actionCompleteHandler($event)' [maxLength]='maxLength'>
        <ng-template #valueTemplate>
          <p>The Rich Text Editor is WYSIWYG ("what you see is what you get") editor useful to create and edit content, and return the valid <a href="https://ej2.syncfusion.com/home/" target="_blank">HTML markup</a> or <a href="https://ej2.syncfusion.com/home/" target="_blank">markdown</a> of the content</p>
            <p><b>Toolbar</b></p>
            <ol>
                <li>
                    <p> Toolbar contains commands to align the text, insert link, insert image, insert list, undo/redo operations, HTML view, etc </p>
                </li>
                <li>
                    <p> Toolbar is fully customizable </p>
                </li>
            </ol>
            <p><b>Links</b></p>
            <ol>
                <li>
                    <p>You can insert a hyperlink with its corresponding dialog </p>
                </li>
                <li>
                    <p>Attach a hyperlink to the displayed text. </p>
                </li>
                <li>
                    <p> Customize the quick toolbar based on the hyperlink </p>
                </li>
            </ol>
            <p><b>Image.</b></p>
            <ol>
                <li>
                    <p> Allows you to insert images from an online source as well as the
                    local computer </p>
                </li>
                <li>
                    <p> You can upload an image </p>
                </li>
                <li>
                    <p>Provides an option to customize quick toolbar for an image </p>
                </li>
            </ol>
        </ng-template>
    </ejs-richtexteditor>`,
providers: [ToolbarService, LinkService, ImageService, HtmlEditorService, CountService]
})
export class AppComponent  {
@ViewChild('toolsRTE') public rteObj: RichTextEditorComponent;
public tools: object = {
    items: ['Bold', 'Italic', 'Underline', 'StrikeThrough',
    'FontName', 'FontSize', 'FontColor', 'BackgroundColor',
    'LowerCase', 'UpperCase', '|',
    'Formats', 'Alignments', 'OrderedList', 'UnorderedList',
    'Outdent', 'Indent', '|',
    'CreateLink', 'Image', '|', 'ClearFormat', 'Print',
    'SourceCode', 'FullScreen', '|', 'Undo', 'Redo']
};
public maxLength: number = 1000;
public textArea: HTMLElement;
public myCodeMirror: any;
ngAfterViewInit(): void {
let rteObj: RichTextEditorComponent = this.rteObj;
setTimeout(() => { this.textArea = rteObj.contentModule.getEditPanel() as HTMLElement; }, 600);
}
public mirrorConversion(e?: any): void {
let id: string = this.rteObj.getID() + 'mirror-view';
let mirrorView: HTMLElement = this.rteObj.element.querySelector('#' + id) as HTMLElement;
let charCount: HTMLElement = this.rteObj.element.querySelector('.e-rte-character-count') as HTMLElement;
if (e.targetItem === 'Preview') {
    this.textArea.style.display = 'block';
    mirrorView.style.display = 'none';
    this.textArea.innerHTML = this.myCodeMirror.getValue();
    charCount.style.display = 'block';
} else {
    if (!mirrorView) {
        mirrorView = createElement('div', { className: 'e-content' });
        mirrorView.id = id;
        this.textArea.parentNode.appendChild(mirrorView);
    } else {
        mirrorView.innerHTML = '';
    }
    this.textArea.style.display = 'none';
    mirrorView.style.display = 'block';
    this.renderCodeMirror(mirrorView, this.rteObj.value);
    charCount.style.display = 'none';
}
}

public renderCodeMirror(mirrorView: HTMLElement, content: string): void {
this.myCodeMirror = CodeMirror(mirrorView, {
    value: content,
    lineNumbers: true,
    mode: 'text/html',
    lineWrapping: true,

});
}
public actionCompleteHandler(e: any): void {
if (e.targetItem && (e.targetItem === 'SourceCode' || e.targetItem === 'Preview')) {
    (this.rteObj.sourceCodeModule.getPanel() as HTMLTextAreaElement).style.display = 'none';
    this.mirrorConversion(e);
} else {
    setTimeout(() => { this.rteObj.toolbarModule.refreshToolbarOverflow(); }, 400);
}
}
}

```

{% endtab %}

## Integrate `embedly`

This can be achieved by binding the [`actionComplete`](../api/rich-text-editor/#actioncomplete) event to the toolbar items in the [`toolbarSettings`](../api/rich-text-editor/#toolbarsettings) property. In the event handler, create an element and add the appropriate class. The below script is have to add in the sample to embed the content,

Include `embedly` javascript.

```typescript

<script src="https://cdn.embedly.com/widgets/platform.js" charset="UTF-8"></script>

```

The above script is added to the page.

{% tab template="rich-text-editor/how-to/embedly", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, RichTextEditorComponent  } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='defaultRTE' #sample [toolbarSettings]='toolbarSettings' (actionComplete)='actionComplete($event)'>
    <ng-template #valueTemplate>
      <p>The Rich Text Editor triggers events based on its actions. </p>
      <p> The events can be used as an extension point to perform custom operations.</p>
      <ul>
        <li>created - Triggers when the component is rendered.</li>
        <li>change - Triggers only when RTE is blurred and changes are done to the content.</li>
        <li>focus - Triggers when RTE is focused in.</li>
        <li>blur - Triggers when RTE is focused out.</li>
        <li>actionBegin - Triggers before command execution using toolbar items or executeCommand method.</li>
        <li>actionComplete - Triggers after command execution using toolbar items or executeCommand method.</li>
        <li>destroyed – Triggers when the component is destroyed.</li>
      </ul>
    </ng-template></ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService ]
})
export class AppComponent  {
@ViewChild('sample') public rteObj: RichTextEditorComponent;
public toolbarSettings: Object = {
    items: ['createLink']};
public actionComplete(args: any): void {
      if (<String>args.requestType === 'Links') {
        if (args.elements[0].parentNode && (<Element>args.elements[0].parentNode).tagName === 'A'){
          const emberEle: HTMLElement = document.createElement('blockquote');
          emberEle.setAttribute('class', 'embedly-card');
          emberEle.appendChild(args.elements[0].parentElement);
          emberEle.appendChild(document.createElement('p'));
          args.range.insertNode(emberEle);
        }
    }
    }
}

```

{% endtab %}

## `At.js` Integration

RichTextEditor can easily be integrated with [`At.js`](https://github.com/ichord/At.js) library. To display the autocomplete list, type ‘@’.

Include `At.JS` style.

```typescript

 <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/at.js/1.4.0/css/jquery.atwho.min.css">

```

Include At.JS javascript.

```typescript

<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/at.js/1.4.0/js/jquery.atwho.min.js"></script>

```

Define the `At.js` configuration

> In below configuration, email id of employees list - email id of employees from the data source.

```typescript

var config = {
    at: "@",
    data: [email id of employees list],
    displayTpl: '<li>${name} <small>${email}</small></li>',
    limit: 200
  }

```

Populate the employee’s email id from local or remote data and set the result to the data of `At.js` configuration.

{% tab template="rich-text-editor/how-to/atjs-integration", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, RichTextEditorComponent  } from '@syncfusion/ej2-angular-richtexteditor';

@Component({
        selector: 'app-root',
        template: `<ejs-richtexteditor id='defaultRTE' #sample [placeholder]='placeholder' (created)='oncreate($event)'></ejs-richtexteditor>`,
        providers: [ToolbarService, LinkService, ImageService, HtmlEditorService ]
})
export class AppComponent  {
  @ViewChild('sample') public rteObj: RichTextEditorComponent;
  // Build data to be used in At.JS config.
  public employeeList: { [key: string]: Object }[] = [
      { id: 'emp01', name: 'Jacob', email: 'jacob@mail.com' },
      { id: 'emp02', name: 'Isabella', email: 'isabella@mail.com' },
      { id: 'emp03', name: 'Ethan', email: 'ethan@mail.com' },
      { id: 'emp04', name: 'Emma', email: 'emma@mail.com' },
      { id: 'emp05', name: 'Michael', email: 'michael@mail.com' },
      { id: 'emp06', name: 'Olivia', email: 'olivia@mail.com' },
      { id: 'emp07', name: 'Jeniffer', email: 'jeniffer@mail.com' }
  ];

  public config: Object = {
      at: "@",
       callbacks: {
        beforeReposition: function (offset) {
            offset.left = this.rect().left - (leftBarWdith + leftPadding);
        }
      },
      data: this.employeeList,
      displayTpl: '<li>${name} <small>${email}</small></li>',
      limit: 200
  };
public placeholder: String = "Type @ to get the e-mail list";
public leftBarWdith : number = window.parent.document.getElementById('doc-left-toc').offsetWidth;
public leftPadding : number = +getComputedStyle(window.parent.document.getElementById('md-cnt')).paddingRight.match(/\d/g).join('');

public oncreate(e: any): void {
    const textArea: HTMLElement = this.rteObj.contentModule.getEditPanel() as HTMLElement;
    $(textArea).atwho(this.config);
    $(textArea).on('keydown', function(e: any) {
    if (e.keyCode === 13 && $(textArea).atwho('isSelecting')) {
        return false;
      }
    });
    }
}

```

{% endtab %}
