---
title: "Rich Text Editor Markdown"
component: "Rich Text Editor"
description: "This section for Syncfusion's Angular Rich Text Editor component explains the markdown editing and custom formatting."
---

# Markdown

When you format the word in Markdown format, you should add Markdown syntax to the word to indicate the words and phrases that looks different from each other.

Rich Text Editor supports markdown editing when the [`editorMode`](..api/rich-text-editor/#editormode) set as **markdown** and using both *keyboard interaction* and *toolbar action*, you can apply the formatting to text

To use quick Markdown editing feature, inject `MarkdownEditorService` in the provider section of `AppModule`.

## Supported Commands

The Angular Markdown editor supports the following commands to format the markdown content:

|Commands|Syntax| Description |
|--------|------------------------------------------|------------|
| Bold | Sample content for `**`bold text`**`. | For bold, add `**` or `__` to front and back of the text. | For order list, precede each line with a number. |
| Italic | Sample content for `*`Italic text`*`. | For Italic, add `*` or `_` to front and back of the text. |
| Bold and Italics | Sample content for `***`bold and Italic text`***`. | For bold and Italics, add `***` to the front and back of the text. |
| Heading 1 | `#` Heading 1 content | For heading 1, add `#` to start of the line. |
| Heading 2 | `##` Heading 2 content | For heading 2, add `##` to start of the line. |
| Heading 3 | `###` Heading 3 content | For heading 3, add `###` to start of the line. |
| Heading 4 | `####` Heading 4 content | For heading 4, add `####` to start of the line. |
| Heading 5 | `#####` Heading 5 content | For heading 5, add `#####` to start of the line. |
| Heading 6 | `######` Heading 6 content | For heading 6, add `######` to start of the line. |
| Line Break | First line `<br>`Second line | For line break, press enter two times (or) add `<br>` in between the first and the second line. |
| Blockquotes | `>` Blockquotes text | For blockquotes, add `>` to start of the line. |
| Strike Through | Sample content for `~~`strike through text`~~`. | For strike through, add `~~` to front and back of the text. |
| Code (Single line) | \`Single line code\` | For single line code, add \` to front and back of the text. |
| Code block (Multi Line) | \`\`\`<br>Multi line code text<br>Multi line code text<br>\`\`\` | For multiple line code, add \`\`\` in the new line before and after the content. |
| Subscript | `<sub>`Subscript text`</sub>` | For subscript, add `<sub>` to the front and `</sub>` to the back of the text. |
| Superscript | `<sup>`Superscript text`</sup>` | For superscript, add `<sup>` to the front and `</sup>` to the back of the text. |
| Ordered List | `1.` First<br>`1.` Second | For ordered list, preceding one or more lines of text with `1.` |
| Unordered List | `*` First<br> `*` second | For unordered list, preceding one or more lines of text with `*`. |
| Links | **Link text without title text**<br>`[` Link text `](`URL`)`<br> **Link text with title text**<br>`[` Link text `](`URL , “title text”`)` | Create an inline link by wrapping link text in brackets `[ ]`, and then wrapping the URL as first parameter and title as second parameter in the parentheses `()`.<br>**Note:** The title text is optional, if needed it can be given manually.|
| Table | `|` Heading 1 `|` Heading 2 `|`<br>`|---------|---------|`<br>`|` Col A1 `|` Col A2 `|`<br>`|` Col B1 `|` Col B2 `|` | Create a table using the pipes and underscores as given in the syntax to create 2 x 2 table. |
| Horizontal Line | `***` (three asterix in new line)<br>(or)<br>`___` (three underscores in new line) | For horizontal line, add `***` or `___` to the start of the new line. |
| Image | `![](`URL path`)` | Create an image by wrapping the image source in parentheses `()`. |
| Image with alternate text | `![` alternate text `](`URL path`)` | Create an image with alternate text by wrapping an alternative text in brackets `[]`, and then link of the image source in parentheses `()`.<br>**Note:** When inserting the image using toolbar, the alternate text cannot be provided that needs to be given manually. |
| Escape tick marks supported | Sample text content with `**`bold and `**`not bold`**` text can be in the same line.`**` | In the syntax, the whole content is made as bold where the content `not bold` can be made as normal text by adding the bold syntax to the start and end of the respective text. Likewise you can do the same for various inline commands. |
| Escape Character | `\(`any syntax`)` | Escape any markdown syntax by prefix `\` to the syntax.<br>Example:<br>`\**`Bold text`**`|
| HTML Entities | Copyright: &copy; - `&copy;` <br>Trade mark: &trade; - `&trade;`<br>Registered: &reg; - `&reg;`<br>Ampersand: &amp; - `&amp;`<br>Less than: &lt; - `&lt;`<br>Greater than: &gt; - `&gt;` | For HTML entities, add & and ; to the front and back of the respective entities. |

> The above listed commands alone are supported in Syncfusion Markdown editor. For other unsupported commands, you can achieve using the HTML tags in Markdown editor. The foot notes, definitions, math, and check list markdown syntax are also not supported.

## Markdown to HTML

The Rich Text Editor allows you to preview markdown changes immediately using preview. In this sample, the third-party library [`Marked`](https://marked.js.org/) is used to convert markdown into HTML content.

This sample demonstrates how to preview markdown changes in Rich Text Editor. Type or edit the display text, and apply format to view the preview of markdown. The [`actionComplete`](../api/rich-text-editor/#actioncomplete) event can be used to convert Markdown to HTML.

{% tab template="rich-text-editor/markdown", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { enableRipple } from '@syncfusion/ej2-base';
enableRipple(true);
/**
 * Rich Text Editor Markdown Preview demo
 */
import { Component, ViewChild } from '@angular/core';
import { addClass, removeClass, Browser } from '@syncfusion/ej2-base';
import { RichTextEditorComponent, ToolbarService, LinkService } from '@syncfusion/ej2-angular-richtexteditor';
import { ImageService, MarkdownEditorService } from '@syncfusion/ej2-angular-richtexteditor';
import { createElement, KeyboardEventArgs, isNullOrUndefined } from '@syncfusion/ej2-base';
import * as Marked from 'marked';
    @Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='mdPreview' #mdPreview [toolbarSettings]='tools' [editorMode]='mode' (created)='onCreate()' (actionComplete)="actionComplete($event)">
        <ng-template #valueTemplate>
            In Rich Text Editor , you click the toolbar buttons to format the words and the changes are visible immediately.
            Markdown is not like that. When you format the word in Markdown format, you need to
            add Markdown syntax to the word to indicate which words
            and phrases should look different from each other.
            Rich Text Editor supports markdown editing when the editorMode set as **markdown** and using both *keyboard interaction* and *toolbar action*, you can apply the formatting to text.
            You can add our own custom formation syntax for the Markdown formation, [sample link](https://ej2.syncfusion.com/home/).
            The third-party library <b>Marked</b> is used in this sample to convert markdown into HTML content.
        </ng-template>
    </ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, MarkdownEditorService]
    })
export class AppComponent  {
        @ViewChild('mdPreview')
public rteObj: RichTextEditorComponent;
public textArea: HTMLTextAreaElement;
public mdsource: HTMLElement;
public mdSplit: HTMLElement;
public htmlPreview: HTMLElement;
public tools: object = {
    items: ['Bold', 'Italic', 'StrikeThrough', '|', 'Formats', 'OrderedList', 'UnorderedList', '|', 'CreateLink', 'Image', '|',
        {
            tooltipText: 'Preview',
            template: '<button id="preview-code" class="e-tbar-btn e-control e-btn e-icon-btn">' +
            '<span class="e-btn-icon e-md-preview e-icons"></span></button>'
        }, {
            tooltipText: 'Split Editor',
            template: '<button id="MD_Preview" class="e-tbar-btn e-control e-btn e-icon-btn">' +
            '<span class="e-btn-icon e-view-side e-icons"></span></button>'
        }, 'FullScreen', '|', 'Undo', 'Redo']
};
public mode: string = 'Markdown';
public onCreate(): void {
    let script = document.createElement('script');
    script.src = 'https://cdn.jsdelivr.net/npm/marked/marked.min.js';
    document.head.appendChild(script);
    this.textArea = this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement;
    this.textArea.addEventListener('keyup', (e: KeyboardEventArgs) => {
        this.markDownConversion();
    });
    this.mdsource = document.getElementById('preview-code');
    this.mdsource.addEventListener('click', (e: MouseEvent) => {
        this.fullPreview({ mode: true, type: 'preview' });
        if ((e.target as HTMLElement).parentElement.classList.contains('e-active')) {
            this.rteObj.disableToolbarItem(['Bold', 'Italic', 'StrikeThrough', 'OrderedList',
                'UnorderedList', 'CreateLink', 'Image']);
            (e.target as HTMLElement).parentElement.parentElement.nextElementSibling.classList.add('e-overlay');
        } else {
            this.rteObj.enableToolbarItem(['Bold', 'Italic', 'StrikeThrough', 'OrderedList',
                'UnorderedList', 'CreateLink', 'Image']);
            (e.target as HTMLElement).parentElement.parentElement.nextElementSibling.classList.remove('e-overlay');
        }
    });
    this.mdSplit = document.getElementById('MD_Preview');
    this.mdSplit.addEventListener('click', (e: MouseEvent) => {
        if (this.rteObj.element.classList.contains('e-rte-full-screen')) {
            this.fullPreview({ mode: true, type: '' });
        }
        this.mdsource.classList.remove('e-active');
        this.rteObj.showFullScreen();
    });
}
public actionComplete(e: any): void {
    if (e.targetItem === 'Maximize' && isNullOrUndefined(e.args)) {
        this.fullPreview({ mode: true, type: '' });
    } else if (!this.mdSplit.parentElement.classList.contains('e-overlay')) {
        if (e.targetItem === 'Minimize') {
            this.textArea.style.display = 'block';
            this.textArea.style.width = '100%';
            if (this.htmlPreview) { this.htmlPreview.style.display = 'none'; }
            this.mdSplit.classList.remove('e-active');
            this.mdsource.classList.remove('e-active');
        }
        this.markDownConversion();
    }
}
public markDownConversion(): void {
    if (this.mdSplit.classList.contains('e-active')) {
        let id: string = this.rteObj.getID() + 'html-preview';
        let htmlPreview: HTMLElement = this.rteObj.element.querySelector('#' + id) as HTMLElement;
        debugger
        htmlPreview.innerHTML =  marked((this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement).value);
    }
}
public fullPreview(e: { [key: string]: string | boolean }): void {
    let id: string = this.rteObj.getID() + 'html-preview';
    this.htmlPreview = this.rteObj.element.querySelector('#' + id) as HTMLElement;
    if ((this.mdsource.classList.contains('e-active') || this.mdSplit.classList.contains('e-active')) && e.mode) {
        this.mdsource.classList.remove('e-active');
        this.mdSplit.classList.remove('e-active');
        this.textArea.style.display = 'block';
        this.textArea.style.width = '100%';
        this.htmlPreview.style.display = 'none';
    } else {
        this.mdsource.classList.add('e-active');
        this.mdSplit.classList.add('e-active');
        if (!this.htmlPreview) {
            this.htmlPreview = createElement('div', { className: 'e-content' });
            this.htmlPreview.id = id;
            this.textArea.parentNode.appendChild(this.htmlPreview);
        }
        if (e.type === 'preview') {
            this.textArea.style.display = 'none';
            this.htmlPreview.classList.add('e-pre-source');
        } else {
            this.htmlPreview.classList.remove('e-pre-source');
            this.textArea.style.width = '50%';
        }
        this.htmlPreview.style.display = 'block';
        this.htmlPreview.innerHTML = marked((this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement).value);
    }
}
}

```

{% endtab %}

## Table

Rich Text Editor allows to insert Markdown table in edit panel with 2 X 2 rows and columns along with the heading.
To use table tool, add the `CreateTable` item in toolbar items.

### Insert table

To insert the table in Rich Text Editor's content area, click the insert table icon in the toolbar option.
Please refer the below sample and code snippets to add the table in Markdown editor

{% tab template="rich-text-editor/markdown", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { enableRipple } from '@syncfusion/ej2-base';
enableRipple(true);
/**
 * Rich Text Editor Markdown demo with table
 */
import { Component, ViewChild } from '@angular/core';
import { RichTextEditorComponent, ToolbarService, LinkService } from '@syncfusion/ej2-angular-richtexteditor';
import { ImageService, MarkdownEditorService } from '@syncfusion/ej2-angular-richtexteditor';
import { createElement, KeyboardEventArgs, isNullOrUndefined } from '@syncfusion/ej2-base';
import * as Marked from 'marked';
@Component({
selector: 'app-root',
template: `<ejs-richtexteditor id='mdPreview' #mdPreview [toolbarSettings]='tools' [editorMode]='mode' (created)='onCreate()'
            (actionComplete)="actionComplete($event)">
            <ng-template #valueTemplate>
                In Rich Text Editor , you click the toolbar buttons to format the words and the changes are visible immediately.
                Markdown is not like that. When you format the word in Markdown format, you need to
                add Markdown syntax to the word to indicate which words
                and phrases should look different from each other.
                Rich Text Editor supports markdown editing when the editorMode set as **markdown** and using
                both *keyboard interaction* and *toolbar action*,you can apply the formatting to text.
                You can add our own custom formation syntax for the Markdown formation, [sample link](https://ej2.syncfusion.com/home/).
                The third-party library <b>Marked</b> is used in this sample to convert markdown into HTML content.
            </ng-template>
           </ejs-richtexteditor>`,
providers: [ToolbarService, LinkService, ImageService, MarkdownEditorService]
})
export class AppComponent  {
      @ViewChild('mdPreview')
public rteObj: RichTextEditorComponent;
public textArea: HTMLTextAreaElement;
public mdsource: HTMLElement;
public mdSplit: HTMLElement;
public htmlPreview: HTMLElement;
public tools: object = {
    items: ['Bold', 'Italic', 'StrikeThrough', '|', 'Formats', 'OrderedList',
            'UnorderedList', '|', 'CreateLink', 'Image', 'CreateTable', '|',
        {
            tooltipText: 'Preview',
            template: '<button id="preview-code" class="e-tbar-btn e-control e-btn e-icon-btn">' +
            '<span class="e-btn-icon e-md-preview e-icons"></span></button>'
        }, {
            tooltipText: 'Split Editor',
            template: '<button id="MD_Preview" class="e-tbar-btn e-control e-btn e-icon-btn">' +
            '<span class="e-btn-icon e-view-side e-icons"></span></button>'
        }, 'FullScreen', '|', 'Undo', 'Redo']
};
public mode: string = 'Markdown';
public onCreate(): void {
    let script = document.createElement('script');
    script.src = 'https://cdn.jsdelivr.net/npm/marked/marked.min.js';
    document.head.appendChild(script);
    this.textArea = this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement;
    this.textArea.addEventListener('keyup', (e: KeyboardEventArgs) => {
        this.markDownConversion();
    });
    this.mdsource = document.getElementById('preview-code');
    this.mdsource.addEventListener('click', (e: MouseEvent) => {
        this.fullPreview({ mode: true, type: 'preview' });
        if ((e.target as HTMLElement).parentElement.classList.contains('e-active')) {
            this.rteObj.disableToolbarItem(['Bold', 'Italic', 'StrikeThrough', 'OrderedList',
                'UnorderedList', 'CreateLink', 'Image', 'CreateTable']);
            (e.target as HTMLElement).parentElement.parentElement.nextElementSibling.classList.add('e-overlay');
        } else {
            this.rteObj.enableToolbarItem(['Bold', 'Italic', 'StrikeThrough', 'OrderedList',
                'UnorderedList', 'CreateLink', 'Image', 'CreateTable']);
            (e.target as HTMLElement).parentElement.parentElement.nextElementSibling.classList.remove('e-overlay');
        }
    });
    this.mdSplit = document.getElementById('MD_Preview');
    this.mdSplit.addEventListener('click', (e: MouseEvent) => {
        if (this.rteObj.element.classList.contains('e-rte-full-screen')) {
            this.fullPreview({ mode: true, type: '' });
        }
        this.mdsource.classList.remove('e-active');
        this.rteObj.showFullScreen();
    });
}
public actionComplete(e: any): void {
    if (e.targetItem === 'Maximize' && isNullOrUndefined(e.args)) {
        this.fullPreview({ mode: true, type: '' });
    } else if (!this.mdSplit.parentElement.classList.contains('e-overlay')) {
        if (e.targetItem === 'Minimize') {
            this.textArea.style.display = 'block';
            this.textArea.style.width = '100%';
            if (this.htmlPreview) { this.htmlPreview.style.display = 'none'; }
            this.mdSplit.classList.remove('e-active');
            this.mdsource.classList.remove('e-active');
        }
        this.markDownConversion();
    }
}
public markDownConversion(): void {
    if (this.mdSplit.classList.contains('e-active')) {
        let id: string = this.rteObj.getID() + 'html-preview';
        let htmlPreview: HTMLElement = this.rteObj.element.querySelector('#' + id) as HTMLElement;
        htmlPreview.innerHTML = marked((this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement).value);
    }
}
public fullPreview(e: { [key: string]: string | boolean }): void {
    let id: string = this.rteObj.getID() + 'html-preview';
    this.htmlPreview = this.rteObj.element.querySelector('#' + id) as HTMLElement;
    if ((this.mdsource.classList.contains('e-active') || this.mdSplit.classList.contains('e-active')) && e.mode) {
        this.mdsource.classList.remove('e-active');
        this.mdSplit.classList.remove('e-active');
        this.textArea.style.display = 'block';
        this.textArea.style.width = '100%';
        this.htmlPreview.style.display = 'none';
    } else {
        this.mdsource.classList.add('e-active');
        this.mdSplit.classList.add('e-active');
        if (!this.htmlPreview) {
            this.htmlPreview = createElement('div', { className: 'e-content' });
            this.htmlPreview.id = id;
            this.textArea.parentNode.appendChild(this.htmlPreview);
        }
        if (e.type === 'preview') {
            this.textArea.style.display = 'none';
            this.htmlPreview.classList.add('e-pre-source');
        } else {
            this.htmlPreview.classList.remove('e-pre-source');
            this.textArea.style.width = '50%';
        }
        this.htmlPreview.style.display = 'block';
        this.htmlPreview.innerHTML = marked((this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement).value);
    }
}
}

```

{% endtab %}

### Changing table constants

The Markdown table constants can be changed for the table heading and the column names.

{% tab template="rich-text-editor/markdown", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { enableRipple } from '@syncfusion/ej2-base';
enableRipple(true);
/**
 * Rich Text Editor changing table constants (markdown)
 */
import { Component, ViewChild } from '@angular/core';
import { RichTextEditorComponent, ToolbarService, LinkService } from '@syncfusion/ej2-angular-richtexteditor';
import { ImageService, MarkdownEditorService } from '@syncfusion/ej2-angular-richtexteditor';
import { createElement, KeyboardEventArgs, isNullOrUndefined } from '@syncfusion/ej2-base';
import { L10n } from '@syncfusion/ej2-base';
import * as Marked from 'marked';

L10n.load({
'en-US': {
    'richtexteditor': {
        'TableHeadingText': 'Header',
        'TableColText': 'Cell'
      }
  }
});
@Component({
selector: 'app-root',
template: `<ejs-richtexteditor id='mdPreview' #mdPreview [toolbarSettings]='tools' [editorMode]='mode'
(created)='onCreate()' (actionComplete)="actionComplete($event)">
    <ng-template #valueTemplate>
        In Rich Text Editor , you click the toolbar buttons to format the words and the changes are visible immediately.
        Markdown is not like that. When you format the word in Markdown format, you need to
        add Markdown syntax to the word to indicate which words
        and phrases should look different from each other.
        Rich Text Editor supports markdown editing when the editorMode set as **markdown** and using
        both *keyboard interaction* and *toolbar action*, you can apply the formatting to text.
        You can add our own custom formation syntax for the Markdown formation, [sample link](https://ej2.syncfusion.com/home/).
        The third-party library <b>Marked</b> is used in this sample to convert markdown into HTML content.
    </ng-template>
</ejs-richtexteditor>`,
providers: [ToolbarService, LinkService, ImageService, MarkdownEditorService]
})
export class AppComponent  {
      @ViewChild('mdPreview')
public rteObj: RichTextEditorComponent;
public textArea: HTMLTextAreaElement;
public mdsource: HTMLElement;
public mdSplit: HTMLElement;
public htmlPreview: HTMLElement;
public tools: object = {
    items: ['Bold', 'Italic', 'StrikeThrough', '|', 'Formats', 'OrderedList', 'UnorderedList',
          '|', 'CreateLink', 'Image', 'CreateTable', '|',
        {
            tooltipText: 'Preview',
            template: '<button id="preview-code" class="e-tbar-btn e-control e-btn e-icon-btn">' +
            '<span class="e-btn-icon e-md-preview e-icons"></span></button>'
        }, {
            tooltipText: 'Split Editor',
            template: '<button id="MD_Preview" class="e-tbar-btn e-control e-btn e-icon-btn">' +
            '<span class="e-btn-icon e-view-side e-icons"></span></button>'
        }, 'FullScreen', '|', 'Undo', 'Redo']
};
public mode: string = 'Markdown';
public onCreate(): void {
    let script = document.createElement('script');
    script.src = 'https://cdn.jsdelivr.net/npm/marked/marked.min.js';
    document.head.appendChild(script);
    this.textArea = this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement;
    this.textArea.addEventListener('keyup', (e: KeyboardEventArgs) => {
        this.markDownConversion();
    });
    this.mdsource = document.getElementById('preview-code');
    this.mdsource.addEventListener('click', (e: MouseEvent) => {
        this.fullPreview({ mode: true, type: 'preview' });
        if ((e.target as HTMLElement).parentElement.classList.contains('e-active')) {
            this.rteObj.disableToolbarItem(['Bold', 'Italic', 'StrikeThrough', 'OrderedList',
                'UnorderedList', 'CreateLink', 'Image', 'CreateTable']);
            (e.target as HTMLElement).parentElement.parentElement.nextElementSibling.classList.add('e-overlay');
        } else {
            this.rteObj.enableToolbarItem(['Bold', 'Italic', 'StrikeThrough', 'OrderedList',
                'UnorderedList', 'CreateLink', 'Image', 'CreateTable']);
            (e.target as HTMLElement).parentElement.parentElement.nextElementSibling.classList.remove('e-overlay');
        }
    });
    this.mdSplit = document.getElementById('MD_Preview');
    this.mdSplit.addEventListener('click', (e: MouseEvent) => {
        if (this.rteObj.element.classList.contains('e-rte-full-screen')) {
            this.fullPreview({ mode: true, type: '' });
        }
        this.mdsource.classList.remove('e-active');
        this.rteObj.showFullScreen();
    });
}
public actionComplete(e: any): void {
    if (e.targetItem === 'Maximize' && isNullOrUndefined(e.args)) {
        this.fullPreview({ mode: true, type: '' });
    } else if (!this.mdSplit.parentElement.classList.contains('e-overlay')) {
        if (e.targetItem === 'Minimize') {
            this.textArea.style.display = 'block';
            this.textArea.style.width = '100%';
            if (this.htmlPreview) { this.htmlPreview.style.display = 'none'; }
            this.mdSplit.classList.remove('e-active');
            this.mdsource.classList.remove('e-active');
        }
        this.markDownConversion();
    }
}
public markDownConversion(): void {
    if (this.mdSplit.classList.contains('e-active')) {
        let id: string = this.rteObj.getID() + 'html-preview';
        let htmlPreview: HTMLElement = this.rteObj.element.querySelector('#' + id) as HTMLElement;
        htmlPreview.innerHTML = marked((this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement).value);
    }
}
public fullPreview(e: { [key: string]: string | boolean }): void {
    let id: string = this.rteObj.getID() + 'html-preview';
    this.htmlPreview = this.rteObj.element.querySelector('#' + id) as HTMLElement;
    if ((this.mdsource.classList.contains('e-active') || this.mdSplit.classList.contains('e-active')) && e.mode) {
        this.mdsource.classList.remove('e-active');
        this.mdSplit.classList.remove('e-active');
        this.textArea.style.display = 'block';
        this.textArea.style.width = '100%';
        this.htmlPreview.style.display = 'none';
    } else {
        this.mdsource.classList.add('e-active');
        this.mdSplit.classList.add('e-active');
        if (!this.htmlPreview) {
            this.htmlPreview = createElement('div', { className: 'e-content' });
            this.htmlPreview.id = id;
            this.textArea.parentNode.appendChild(this.htmlPreview);
        }
        if (e.type === 'preview') {
            this.textArea.style.display = 'none';
            this.htmlPreview.classList.add('e-pre-source');
        } else {
            this.htmlPreview.classList.remove('e-pre-source');
            this.textArea.style.width = '50%';
        }
        this.htmlPreview.style.display = 'block';
        this.htmlPreview.innerHTML = marked((this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement).value);
    }
}
}

```

{% endtab %}

## Custom formation

The Rich Text Editor allows you to customize the markdown syntax by overriding its default syntax. Configure the customized markdown syntax using the [`formatter`](../api/rich-text-editor/#formatter)property.

This sample demonstrates how to customize tags of markdown formatting.

For example, apply ‘+’ to Unordered list, apply ‘1., 2., 3.’ to Ordered list, for bold, ‘__’, and for italic ‘_’.

{% tab template="rich-text-editor/markdown", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { enableRipple } from '@syncfusion/ej2-base';
enableRipple(true);
/**
 * Rich Text Editor Markdown Preview Sample
 */
import { Component, ViewChild } from '@angular/core';
import { RichTextEditorComponent, MarkdownFormatter, ToolbarService } from '@syncfusion/ej2-angular-richtexteditor';
import { LinkService, ImageService, MarkdownEditorService } from '@syncfusion/ej2-angular-richtexteditor';
import { createElement, KeyboardEventArgs } from '@syncfusion/ej2-base';
import * as Marked from 'marked';
    @Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='mdCustom' #mdCustom [toolbarSettings]='tools' [editorMode]='mode' [formatter]='formatter' (created)='onCreate()'>
        <ng-template #valueTemplate>
          The sample is configured with customized markdown syntax using the __formatter__ property.
          Type the content and click the toolbar item to view customized markdown syntax.
          For unordered list, you need to add a plus sign before the word (e.g., + list1).
          Or To make a phrase bold, you need to add two underscores before and after the phrase (e.g., __this text is bold__).
        </ng-template>
    </ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, MarkdownEditorService]
    })
    export class AppComponent  {
    @ViewChild('mdCustom')
    public rteObj: RichTextEditorComponent;
    public textArea: HTMLTextAreaElement;
    public mdsource: HTMLElement;
    public tools: object = {
        items:  ['Bold', 'Italic', 'StrikeThrough', '|',
        'Formats', 'OrderedList', 'UnorderedList', '|',
        'CreateLink', 'Image', '|',
        {
            tooltipText: 'Preview',
            template: '<button id="preview-code" class="e-tbar-btn e-control e-btn e-icon-btn">' +
                '<span class="e-btn-icon e-icons e-md-preview"></span></button>'
        }, 'Undo', 'Redo']
    };
    public mode: string = 'Markdown';
     public formatter: MarkdownFormatter = new MarkdownFormatter({
        listTags: { 'OL': '1., 2., 3.', 'UL': '+ ' },
        formatTags: {
            'Blockquote': '> '
        },
        selectionTags: {'Bold': '__',  'Italic': '_'}

    });
    public onCreate(): void {
        this.textArea = this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement;
        this.textArea.addEventListener('keyup', (e: KeyboardEventArgs) => {
            this.markDownConversion();
        });
        this.mdsource = document.getElementById('preview-code');
        this.mdsource.addEventListener('click', (e: MouseEvent) => {
            this.fullPreview();
        });
    }
    public markDownConversion(): void {
        if (this.mdsource.classList.contains('e-active')) {
            let id: string = this.rteObj.getID() + 'html-view';
            let htmlPreview: Element = this.rteObj.element.querySelector('#' + id);
            htmlPreview.innerHTML = marked((this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement).value);
        }
    }
    public fullPreview(): void {
        let id: string = this.rteObj.getID() + 'html-preview';
        let htmlPreview: HTMLElement = this.rteObj.element.querySelector('#' + id) as HTMLElement;
        if (this.mdsource.classList.contains('e-active')) {
            this.mdsource.classList.remove('e-active');
            this.textArea.style.display = 'block';
            htmlPreview.style.display = 'none';
        } else {
            this.mdsource.classList.add('e-active');
            if (!htmlPreview) {
                htmlPreview = createElement('div', { className: 'e-content e-pre-source' });
                htmlPreview.id = id;
                this.textArea.parentNode.appendChild(htmlPreview);
            }
            this.textArea.style.display = 'none';
            htmlPreview.style.display = 'block';
            htmlPreview.innerHTML = marked((this.rteObj.contentModule.getEditPanel() as HTMLTextAreaElement).value);
            this.mdsource.parentElement.title = 'Code View';
        }
    }
    }

```

{% endtab %}