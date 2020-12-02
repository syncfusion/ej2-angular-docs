---
title: "Rich Text Editor KeyBoard interaction"
component: "Rich Text Editor"
description: "This section for Syncfusion's Angular Rich Text Editor component explains keyboard accessibility that includes shortcuts to interact with the component."
---

# KeyBoard Support

The Rich Text Editor has full keyboard accessibility that includes shortcuts to open and other actions with toolbar items, drop-down lists and dialogs.

## HTML formation shortcut key

You can use the following key shortcuts when the Rich Text Editor renders with HTML edit mode.

| Actions | Keyboard shortcuts |
|----------------|---------|
| Toolbar focus | <kbd>alt</kbd> + <kbd>f10</kbd> |
| Insert link | <kbd>ctrl</kbd> + <kbd>k</kbd> |
| Insert image | <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>i</kbd> |
| Insert table | <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>e</kbd> |
| Undo | <kbd>ctrl</kbd> + <kbd>z</kbd> |
| Redo | <kbd>ctrl</kbd> + <kbd>y</kbd> |
| Copy | <kbd>ctrl</kbd> + <kbd>c</kbd> |
| Cut | <kbd>ctrl</kbd> + <kbd>x</kbd> |
| Paste| <kbd>ctrl</kbd> + <kbd>v</kbd> |
| Bold| <kbd>ctrl</kbd> + <kbd>b</kbd> |
| Italic| <kbd>ctrl</kbd> + <kbd>i</kbd> |
| Underline| <kbd>ctrl</kbd> + <kbd>u</kbd> |
| Strikethrough| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>s</kbd> |
| Uppercase| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>u</kbd> |
| Lowercase| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>l</kbd> |
| Superscript| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>=</kbd> |
| Subscript| <kbd>ctrl</kbd> + <kbd>=</kbd> |
| Indents| <kbd>ctrl</kbd> + <kbd>]</kbd> |
| Outdents| <kbd>ctrl</kbd> + <kbd>[</kbd> |
| HTML source | <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>h</kbd> |
| Fullscreen| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>f</kbd> |
| Justify center| <kbd>ctrl</kbd> + <kbd>e</kbd> |
| Justify full | <kbd>ctrl</kbd> + <kbd>j</kbd> |
| Justify left | <kbd>ctrl</kbd> + <kbd>l</kbd> |
| Justify right | <kbd>ctrl</kbd> + <kbd>r</kbd> |
| Clear format | <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>r</kbd> |
| Ordered list | <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>o</kbd> |
| Unordered list | <kbd>ctrl</kbd> + <kbd>alt</kbd> + <kbd>o</kbd> |

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
    import { Component, ViewChild } from '@angular/core';
    import { ToolbarService, LinkService, ImageService, HtmlEditorService, RichTextEditorComponent} from '@syncfusion/ej2-angular-richtexteditor';
    @Component({
    selector: 'app-root',
    template:`<ejs-richtexteditor #defaultRTE id='defaultRTE' [toolbarSettings]='tools' (create)='onCreate($event)'></ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
    })
    export class AppComponent  {
        @ViewChild('defaultRTE') rteObj: RichTextEditorComponent;
        public tools = {
            items: ['Bold', 'Italic', 'Underline', 'StrikeThrough',
        'FontName', 'FontSize', 'FontColor', 'BackgroundColor',
        'LowerCase', 'UpperCase', '|',
        'Formats', 'Alignments', 'OrderedList', 'UnorderedList',
        'Outdent', 'Indent', '|',
        'CreateLink', 'Image', '|', 'ClearFormat', 'Print',
        'SourceCode', 'FullScreen', '|', 'Undo', 'Redo']
        };
        onCreate(e) {
            document.onkeyup = function (e) {
                if (e.altKey && e.keyCode === 84 /* t */) {
                    // press alt+t to focus the component.
                    this.rteObj.focusIn();
                }
            }
        }
    }

```

{% endtab %}

## Markdown formation shortcut key

You can use the following key shortcuts when the Rich Text Editor renders with Markdown edit mode

| Actions | Keyboard shortcuts |
|----------------|---------|
| Toolbar focus| <kbd>alt</kbd> + <kbd>f10</kbd> |
| Insert link| <kbd>ctrl</kbd> + <kbd>k</kbd> |
| Insert image| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>i</kbd> |
| Insert table| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>e</kbd> |
| Undo| <kbd>ctrl</kbd> + <kbd>z</kbd> |
| Redo| <kbd>ctrl</kbd> + <kbd>y</kbd> |
| Copy| <kbd>ctrl</kbd> + <kbd>c</kbd> |
| Cut| <kbd>ctrl</kbd> + <kbd>x</kbd> |
| Paste| <kbd>ctrl</kbd> + <kbd>v</kbd> |
| Bold| <kbd>ctrl</kbd> + <kbd>b</kbd> |
| Italic| <kbd>ctrl</kbd> + <kbd>i</kbd> |
| Strikethrough| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>s</kbd> |
| Uppercase| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>u</kbd> |
| Lowercase| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>l</kbd> |
| Superscript| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>=</kbd> |
| Subscript| <kbd>ctrl</kbd> + <kbd>=</kbd> |
| Fullscreen| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>f</kbd> |
| Ordered list| <kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>o</kbd> |
| Unordered list| <kbd>ctrl</kbd> + <kbd>alt</kbd> + <kbd>o</kbd> |

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
    import { Component, ViewChild } from '@angular/core';
    import { ToolbarService, LinkService, ImageService, MarkdownEditorService, RichTextEditorComponent} from '@syncfusion/ej2-angular-richtexteditor';
    @Component({
    selector: 'app-root',
    template:`<ejs-richtexteditor #defaultRTE id='defaultRTE' [toolbarSettings]='tools' [editorMode]='mode'(create)='onCreate($event)'></ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, MarkdownEditorService]
    })
    export class AppComponent  {
        @ViewChild('defaultRTE') rteObj: RichTextEditorComponent;
        public tools = {
           items: ['Bold', 'Italic', 'StrikeThrough', '|',
            'Formats', 'OrderedList', 'UnorderedList', '|',
            'CreateLink', 'Image', '|','Undo', 'Redo']
        };
        public mode = 'Markdown';
        onCreate(e) {
            document.onkeyup = function (e) {
                if (e.altKey && e.keyCode === 84 /* t */) {
                    // press alt+t to focus the component.
                    this.rteObj.focusIn();
                }
            }
        }
    }

```

{% endtab %}

## Custom key config

You can able to customize the key config for the keyboard interaction of Rich Text Editor, using [`keyConfig`](../api/rich-text-editor/#keyconfig) property.

In the below sample, you have customize the bold, italic, underline toolbar action with ctrl+alt+b, ctrl+alt+i and ctrl+alt+u respectively.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
    import { Component, ViewChild } from '@angular/core';
    import { ToolbarService, LinkService, ImageService, HtmlEditorService, RichTextEditorComponent} from '@syncfusion/ej2-angular-richtexteditor';
    @Component({
    selector: 'app-root',
    template:`<ejs-richtexteditor #defaultRTE id='defaultRTE' [toolbarSettings]='tools' [keyConfig]='keyConfig' (create)='onCreate($event)'></ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
    })
    export class AppComponent  {
        @ViewChild('defaultRTE') rteObj: RichTextEditorComponent;
        public tools = {
            items: ['Bold', 'Italic', 'Underline', 'StrikeThrough',
        'FontName', 'FontSize', 'FontColor', 'BackgroundColor',
        'LowerCase', 'UpperCase', '|',
        'Formats', 'Alignments', 'OrderedList', 'UnorderedList',
        'Outdent', 'Indent', '|',
        'CreateLink', 'Image', '|', 'ClearFormat', 'Print',
        'SourceCode', 'FullScreen', '|', 'Undo', 'Redo']
        };
        public keyConfig = {
            'copy': 'ctrl+1',
            'cut': 'ctrl+2',
            'paste': 'ctrl+3'
        }
        onCreate(e) {
            document.onkeyup = function (e) {
                if (e.altKey && e.keyCode === 84 /* t */) {
                    // press alt+t to focus the component.
                    this.rteObj.focusIn();
                }
            }
        }
    }

```

{% endtab %}
