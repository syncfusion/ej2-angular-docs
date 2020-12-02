---
title: "Angular Rich Text Editor Miscellaneous"
component: "Rich Text Editor"
description: "This section for Syncfusion's Angular Rich Text Editor component explains on how to directly edit HTML code via `Source View` in the text area."
---

# Miscellaneous

## Placeholder

Specifies the placeholder for the Rich Text Editor’s content used when the Rich Text Editor body is empty through the [`placeholder`](../api/rich-text-editor/#placeholder) property.

Through the `e-rte-placeholder` class to define our custom font family, font color, and styles to the placeholder text.

```typescript

.e-richtexteditor .e-rte-placeholder {
    font-family: monospace;
}

```

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='defaultRTE' placeholder='Type Something'></ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
})
export class AppComponent  {
}

```

{% endtab %}

## Character count

The Rich Text Editor automatically counts the number of characters in the content are while typing using the [`showCharCount`](../api/rich-text-editor/#showcharcount) property. The characters count displayed at the bottom of the editor. You can limit the number of characters in your content using the [`maxLength`](../api/rich-text-editor/#maxlength) property. By default, the editor sets the characters limit value is infinity.

The character count color will be modified based on the characters in the RichTextEditor.

| Status | Description |
|----------------|---------|
| normal | Till 70% of given maxLength count reach, character count color is black.|
| warning | Once the number of character count in the Rich Text Editor reached 70% of given maxLength count, the character count color will be orange, indicating that, the Rich Text Editor value going to reach the maximum count.|
| error | Once the number of character count in the Rich Text Editor reached 90% of given maxLength count, the character count color will be red, indicating that, the Rich Text Editor value reached the maximum count.|

To use quick `Character Count` feature, inject `CountService` in the provider section of `AppModule`.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, CountService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='defaultRTE' [showCharCount]='true' [maxLength]='maxLength'></ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService, CountService]
})
export class AppComponent  {
    public maxLength = 2000;
}

```

{% endtab %}

## Code view

RichTextEditor includes the ability for users to directly edit HTML code via `Source View` in the text area. If you made any modification in Source view directly, the changes will be reflected in the Rich Text Editor's content. So, the users will have more flexibility over the content they have created.

This sample used [`Code mirror`](https://codemirror.net/) plugin helps to highlight the HTML content and when changes happens in code view, the same has been reflected in preview mode.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component, ViewChild, AfterViewInit } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService} from '@syncfusion/ej2-angular-richtexteditor';
import { RichTextEditorComponent, CountService} from '@syncfusion/ej2-angular-richtexteditor';
import { createElement } from '@syncfusion/ej2-base';
import CodeMirror from 'codemirror';


@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor #toolsRTE id='alltoolRTE' [toolbarSettings]='tools'
    [showCharCount]='true' (actionComplete)='actionCompleteHandler($event)' [maxLength]='maxLength'>
            <ng-template #valueTemplate>
                <p>The Rich Text Editor is WYSIWYG ("what you see is what you get") editor useful to create and edit content and return
                the valid <a href="https://ej2.syncfusion.com/home/" target="_blank">HTML markup</a> or
                <a href="https://ej2.syncfusion.com/home/" target="_blank">markdown</a> of the content</p>

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
export class AppComponent implements AfterViewInit  {
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

## Undo/redo manager

Undo and redo tools allow you to edit the text by disregard/cancel the recently made changes and restore it to previous state. It is a useful tool to restore the performed action which got changed by mistake. By default, upto 30 actions can be undo/redo in the editor.

To undo and redo operations, do one of the following:

* Press the undo/redo button on the toolbar.
* Press the `Ctrl + Z/Ctrl + Y` combination on the keyboard.

Customize the undo/redo step count using the [`undoRedoSteps`](../api/rich-text-editor/#undoredosteps) property. By default, undo/redo actions take 300ms time interval for store the action to the undoRedoManager. The time interval can be customized by using the [`undoRedoTimer`](../api/rich-text-editor/#undoredotimer).

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, CountService } from '@syncfusion/ej2-angular-richtexteditor';

@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='defaultRTE' [toolbarSettings]='tools' [undoRedoSteps] ='steps' [undoRedoTimer]='timer'>
               </ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService, CountService]
})
export class AppComponent  {
    public tools = {items: ['Undo', 'Redo']};
    public steps = 50;
    public timer = 400;
}
```

{% endtab %}

## Prevention of cross-site scripting (XSS)

The Rich Text Editor allow the users to edit the content with security by preventing cross-site
scripting (XSS). By default, provided built-in support to remove the elements from editor content which cause XSS
attack. The editor removes the elements based on the attributes if there is possible to execute script.

In the following sample, removed `script` tag and `onmouseover` attribute from content of the Rich Text Editor.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='defaultRTE' [value]='rteValue'></ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
})
export class AppComponent  {
    public rteValue: string = `<div onmouseover='javascript:alert(1)'>Prevention of Cross Sit Scripting (XSS) </div><script>alert('hi')</script>`;
}

```

{% endtab %}

> It's only applicable to editorMode as HTML.

### Custom cross-site scripting

You can also filter the elements and attributes additionally which cause the XSS attack through
[`beforeSanitizeHtml`](../api/rich-text-editor/#beforesanitizehtml) event. Return the value from the event argument `helper` function to apply in the editor. If you want to prevent the built-in support and make own cross-site scripting rules, set `cancel` argument as true.

The following sample demonstrate how to filter `script` tag from value.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, BeforeSanitizeHtmlArgs } from '@syncfusion/ej2-angular-richtexteditor';
import { detach } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='defaultRTE' [value]='rteValue' (beforeSanitizeHtml)='onBeforeSanitizeHtml($event)'></ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
})
export class AppComponent  {
    public rteValue:string =`<div>Prevention of Cross Sit Scripting (XSS)</div><script>alert('hi')</script>`;
    public onBeforeSanitizeHtml(e: BeforeSanitizeHtmlArgs): void {
        e.helper = (value: string) => {
            e.cancel = true;
            let temp: HTMLElement = document.createElement('div');
            temp.innerHTML = value;
            let scriptTag: HTMLElement = temp.querySelector('script');
            if (scriptTag) {
                detach(scriptTag);
            }
            return temp.innerHTML;
      }
    }
}

```

{% endtab %}

## Resizable support

This feature allows the editor to be resized dynamically. The users can enable or disable this feature using the `enableResize` property in the Rich Text Editor. If `enableResize` is set to true, the Rich Text Editor component creates grip at the bottom right corner, which allows resizing the component in the diagonal direction. The following sample demonstrates the resizable feature.

### Enabling the resizable support

To render the Rich Text Editor in the resizable mode, set the `enableResize` property to true. The above feature is segregated into individual feature-wise module. To use Resizable feature, inject `ResizeService` in the provider section of `AppModule`.

{% tab template="rich-text-editor/toolbar/multirow", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, ResizeService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
        template: `<ejs-richtexteditor id='defaultRTE' [enableResize]="true">
        <ng-template #valueTemplate>
            <p>The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor that provides the best user experience to create and update the content.
                Users can format their content using standard toolbar commands.</p>
        </ng-template>
    </ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, ResizeService, HtmlEditorService]
})
export class AppComponent {
}

```

{% endtab %}

### Specifying the Minimum and Maximum width and height for Resize

To have a restricted resizable area for the Rich Text Editor, you need to specify the min-width, max-width, min-height, and max-height CSS properties for the control's wrapper element. By default, the control is capable of resizing upto the current viewport. The `e-richtexteditor` CSS class will be available in the component's wrapper and can be used for applying the above mentioned styles.

{% tab template="rich-text-editor/how-to/rename-image", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, ResizeService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
        template: `<ejs-richtexteditor id='defaultRTE' [enableResize]="true">
        <ng-template #valueTemplate>
            <p>The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor that provides the best user experience to create and update the content.
                Users can format their content using standard toolbar commands.</p>
        </ng-template>
    </ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, ResizeService, HtmlEditorService]
})
export class AppComponent {
}

```

{% endtab %}
