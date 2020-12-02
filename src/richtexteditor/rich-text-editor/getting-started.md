---
title: "Rich Text Editor Getting started"
component: "Rich Text Editor"
description: "This section explains how to create a simple Syncfusion Angular Rich Text Editor component and configure its functionalities in Angular application."
---
# Getting started

This section explains the steps to create a simple **Rich Text Editor** component and configure its available functionalities in Angular.

## Getting Started with Angular CLI

The following section explains the steps required to create a simple angular-cli application and how to configure `Rich Text Editor` component.

### Prerequisites

To get started with Syncfusion Angular UI Components, make sure that you have compatible versions of Angular and TypeScript.

* Angular : 4+
* TypeScript : 2.6+

### Setting up an Angular project

Angular provides an easiest way to setup project using Angular CLI [Angular CLI](https://github.com/angular/angular-cli) tool.

Install the CLI application globally in your machine.

```javascript

  npm install -g @angular/cli

```

### Create a new application

```javascript

  ng new syncfusion-angular-app

```

Once you have executed the above command you may ask for following options,
* Would you like to add Angular routing?
* Which stylesheet format would you like to use?

By default it install the CSS style based application. To setup with SCSS, add `--style=SCSS` suffix on creating project.

Example code snippet.

```javascript

  ng new syncfusion-angular-app --style=SCSS

```

Use below command to Navigate into the created project folder.

```javascript

  cd syncfusion-angular-app

```

## Install Syncfusion Rich Text Editor package

Syncfusion packages are distributed in `npm` server as `@syncfusion` scoped packages. You can get all the Angular Syncfusion package from npm [link](https://www.npmjs.com/search?q=%40syncfusion%2Fej2-angular-).

Add Syncfusion Angular Rich Text Editor package in your application by using following Command,

```javascript

npm install @syncfusion/ej2-angular-richtexteditor --save
(or)
npm i @syncfusion/ej2-angular-richtexteditor --save

```

## Adding Rich Text Editor module

Once you have successfully installed the Rich Text Editor package, corresponding component modules are ready to configure in your application from the installed location. Syncfusion Angular package provides two different types of ngModules.

Refer to [Ng-Module](https://ej2.syncfusion.com/angular/documentation/common/ng-module/) to learn about `ngModules`.

Refer to the following snippet to import the `RichTextEditorModule` in `app.module.ts` from the `@syncfusion/ej2-angular-richtexteditor`.

```javascript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
// Imported Syncfusion RichTextEditorModule from Rich Text Editor package
import { RichTextEditorModule } from '@syncfusion/ej2-angular-richtexteditor';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    // Registering EJ2 Rich Text Editor Module
    RichTextEditorModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

## Adding Rich Text Editor component

Add the Rich Text Editor component snippet in `app.component.ts` as follows.

```typescript

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
  selector: 'app-root',
  template: `<ejs-richtexteditor id='defaultRTE'>
  <ng-template #valueTemplate>
  <p>The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor that provides the best user experience to create and update the content.
  Users can format their content using standard toolbar commands.</p>
  <p><b>Key features:</b></p>
  <ul><li><p>Provides &lt;IFRAME&gt; and &lt;DIV&gt; modes.</p></li>
  <li><p>Capable of handling markdown editing.</p></li>
  <li><p>Contains a modular library to load the necessary functionality on demand.</p></li>
  <li><p>Provides a fully customizable toolbar.</p></li>
  <li><p>Provides HTML view to edit the source directly for developers.</p></li>
  <li><p>Supports third-party library integration.</p></li>
  <li><p>Allows preview of modified content before saving it.</p></li>
  <li><p>Handles images, hyperlinks, video, hyperlinks, uploads, etc.</p></li>
  <li><p>Contains undo/redo manager. </p></li>
  <li><p>Creates bulleted and numbered lists.</p></li>
  </ul>
  </ng-template>
  </ejs-richtexteditor>`,
  providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
})

export class AppComponent {

}

```

## Adding CSS reference

The following CSS files are available in `../node_modules/@syncfusion` package folder. This can be referenced in [src/styles.css] using following code.

```css

      @import '../node_modules/@syncfusion/ej2-base/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-icons/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-buttons/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-splitbuttons/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-inputs/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-lists/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-navigations/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-popups/styles/material.css';
      @import '../node_modules/@syncfusion/ej2-richtexteditor/styles/material.css';

```

> The [Custom Resource Generator (CRG)](https://crg.syncfusion.com/) is an online web tool, which can be used to generate the custom script and styles for a set of specific components.
> This web tool is useful to combine the required component scripts and styles in a single file.

## Running the application

Run the `ng serve` command in command window, it will serve your application and you can open the browser window. Output will appear as follows.

{% tab template="rich-text-editor/getting-started-value", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
  selector: 'app-root',
  template: `<ejs-richtexteditor id='defaultRTE'>
  <ng-template #valueTemplate>
  <p>The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor that provides the best user experience to create and update the content.
  Users can format their content using standard toolbar commands.</p>
  <p><b>Key features:</b></p>
  <ul><li><p>Provides &lt;IFRAME&gt; and &lt;DIV&gt; modes.</p></li>
  <li><p>Capable of handling markdown editing.</p></li>
  <li><p>Contains a modular library to load the necessary functionality on demand.</p></li>
  <li><p>Provides a fully customizable toolbar.</p></li>
  <li><p>Provides HTML view to edit the source directly for developers.</p></li>
  <li><p>Supports third-party library integration.</p></li>
  <li><p>Allows preview of modified content before saving it.</p></li>
  <li><p>Handles images, hyperlinks, video, hyperlinks, uploads, etc.</p></li>
  <li><p>Contains undo/redo manager. </p></li>
  <li><p>Creates bulleted and numbered lists.</p></li>
  </ul>
  </ng-template>
  </ejs-richtexteditor>`,
  providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
})

export class AppComponent {

}

```

{% endtab %}

## Initialize Rich Text Editor from `<iframe>` element

The Rich Text Editor’s content is placed in an `iframe` and isolated from the rest of the page.

Initialize the Rich Text Editor on div element and set the enable field [`iframeSettings`](../api/rich-text-editor/#iframesettings) property to true.

{% tab template="rich-text-editor/getting-started-iframe", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
  selector: 'app-root',
  template: `<ejs-richtexteditor id='iframeRTE' [toolbarSettings]='tools' [iframeSettings]='iframe' [height]='height'>
  <ng-template #valueTemplate>
  <p>The Rich Text Editor component is WYSIWYG ("what you see is what you get") editor
        that provides the best user experience to create and update the content.
            Users can format their content using standard toolbar commands.</p>

            <p><b>Key features:</b></p>

            <ul><li><p>Provides &lt;IFRAME&gt; and &lt;DIV&gt; modes</p></li>
            <li><p>Capable of handling markdown editing.</p></li>
            <li><p>Contains a modular library to load the necessary functionality on demand.</p></li>
            <li><p>Provides a fully customizable toolbar.</p></li>
            <li><p>Provides HTML view to edit the source directly for developers.</p></li>
            <li><p>Supports third-party library integration.</p></li>
            <li><p>Allows preview of modified content before saving it.</p></li>
            <li><p>Handles images, hyperlinks, video, hyperlinks, uploads, etc.</p></li>
            <li><p>Contains undo/redo manager.</p></li>
            <li><p>Creates bulleted and numbered lists.</p></li>
            </ul>
  </ng-template>
  </ejs-richtexteditor>`,
  providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
})

export class AppComponent {
        public tools: object = {
            items: ['Undo', 'Redo', '|',
                'Bold', 'Italic', 'Underline', 'StrikeThrough', '|',
                'FontName', 'FontSize', 'FontColor', 'BackgroundColor', '|',
                'SubScript', 'SuperScript', '|',
                'LowerCase', 'UpperCase', '|',
                'Formats', 'Alignments', '|', 'OrderedList', 'UnorderedList', '|',
                'Indent', 'Outdent', '|', 'CreateLink',
                'Image', '|', 'ClearFormat', 'Print', 'SourceCode', '|', 'FullScreen']
        };
        public iframe: object = { enable: true };
        public height: number = 500;
}

```

{% endtab %}

## Module Injection

To create Rich Text Editor with additional features, inject the required modules. The following modules are used to extend Rich Text Editor’s basic functionality.

* `toolbar` - Inject this module to use Toolbar features.
* `link` - Inject this module to use link features in RTE.
* `image`- Inject this module to use image features in RTE.
* `count` - Inject this module to use character count in RTE.
* `markdownEditor`-Inject this module to use RTE as markdown editor.
* `htmlEditor` - Inject this module to use RTE as html editor.
* `quickToolbar` - Inject this module to use quick toolbar feature for the target element.

These modules should be injected into the provider section of `AppModule`.

## Configure the Toolbar

Configure the toolbar with custom tools using items field of toolbarSettings property in your application.

{% tab template="rich-text-editor/getting-started-toolbar", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
  selector: 'app-root',
  template: `<ejs-richtexteditor id='rteTool' [toolbarSettings]='tools'>
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
  </ng-template>
  </ejs-richtexteditor>`,
  providers: [ToolbarService, LinkService, ImageService, HtmlEditorService]
})

export class AppComponent {
  public tools: object = {
      items: ['Undo', 'Redo', '|',
          'Bold', 'Italic', 'Underline', 'StrikeThrough', '|',
          'FontName', 'FontSize', 'FontColor', 'BackgroundColor', '|',
          'SubScript', 'SuperScript', '|',
          'LowerCase', 'UpperCase', '|',
          'Formats', 'Alignments', '|', 'OrderedList', 'UnorderedList', '|',
          'Indent', 'Outdent', '|', 'CreateLink',
          'Image', '|', 'ClearFormat', 'Print', 'SourceCode', '|', 'FullScreen']
  };
}

```

{% endtab %}

## Insert images and links

The image module inserts an image into Rich Text Editor’s content area, and the link module links external resources such as website URLs, to selected text in the Rich Text Editor’s content, respectively.

The link inject module adds a link icon to the toolbar and the image inject module adds an image icon to the toolbar.

Specifies the items to be rendered in the quick toolbar based on the target element such image, link, and text element. The quick toolbar opens to customize the element by clicking the target element.

{% tab template="rich-text-editor/getting-started", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript

import { Component } from '@angular/core';
import { ToolbarService, LinkService, ImageService, HtmlEditorService, QuickToolbarService } from '@syncfusion/ej2-angular-richtexteditor';
@Component({
    selector: 'app-root',
    template: `<ejs-richtexteditor id='defaultRTE' [toolbarSettings]='tools' [quickToolbarSettings]='quickTools'>
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
    </ng-template>
    </ejs-richtexteditor>`,
    providers: [ToolbarService, LinkService, ImageService, HtmlEditorService, QuickToolbarService]
})
export class AppComponent  {
    public tools: object = {
        items: ['Undo', 'Redo', '|',
            'Bold', 'Italic', 'Underline', 'StrikeThrough', '|',
            'FontName', 'FontSize', 'FontColor', 'BackgroundColor', '|',
            'SubScript', 'SuperScript', '|',
            'LowerCase', 'UpperCase', '|',
            'Formats', 'Alignments', '|', 'OrderedList', 'UnorderedList', '|',
            'Indent', 'Outdent', '|', 'CreateLink',
            'Image', '|', 'ClearFormat', 'Print', 'SourceCode', '|', 'FullScreen']
    };
    public quickTools: object = {
        image: [
            'Replace', 'Align', 'Caption', 'Remove', 'InsertLink', '-', 'Display', 'AltText', 'Dimension']
    };
}

```

{% endtab %}

## Retrieve the formatted content

To retrieve the editor contents, use the value property of Rich Text Editor.

```typescript

  let rteValue: string = this.rteObj.value;

```

Or, you can use the [getHtml](../api/rich-text-editor/#gethtml) public method to retrieve the Rich Text Editor content.

```typescript

  let rteValue: string = this.rteObj.getHtml();

```

To fetch the Rich Text Editor's text content, use [getText](../api/rich-text-editor/#gettext) method.

```typescript
  
  let rteValue: string = this.rteObj.contentModule.getText();

```
