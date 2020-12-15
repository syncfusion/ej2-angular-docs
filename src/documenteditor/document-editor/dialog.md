---
title: "Dialog"
component: "DocumentEditor"
description: "Learn the built-in dialog support in JavaScript document editor and how to open it."
---

# Dialog

Document editor provides dialog support to major operations such as insert or edit hyperlink, formatting text, paragraph, style, list and table properties.

## Font Dialog

Font dialog allows you to modify all text properties for selected contents at once such as bold, italic, underline, font size, font color, strikethrough, subscript and superscript.

Refer to the following example.

{% tab template="document-editor/dialog",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, FontDialogService, EditorService, ContextMenuService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSelection]=true
    [enableSfdtExport]=true [enableContextMenu]=true
    [enableFontDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, FontDialogService, EditorService, ContextMenuService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('Font');
 }
}
```

{% endtab %}

## Paragraph dialog

This dialog allows modifying the paragraph formatting for selection at once such as text alignment, indentation, and spacing.

To open this dialog, refer to the following example.

{% tab template="document-editor/dialog",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, ParagraphDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enableParagraphDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, ParagraphDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('Paragraph');
 }
}
```

{% endtab %}

## Table dialog

This dialog allows creating and inserting a table at cursor position by specifying the required number of rows and columns.

To open this dialog, refer to the following example.

{% tab template="document-editor/dialog",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, TableDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enableTableDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, TableDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('Table');
 }
}
```

{% endtab %}

## Bookmark dialog

This dialog allows you to perform the following operations:

* View all bookmarks.
* Navigate to a bookmark.
* Create a bookmark at current selection.
* Delete an existing bookmark.
To open this dialog, refer to the following example.

{% tab template="document-editor/dialog",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, BookmarkDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enableBookmarkDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, BookmarkDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('Bookmark');
 }
}
```

{% endtab %}

## Hyperlink dialog

This dialog allows editing or inserting a hyperlink at cursor position.

To open this dialog, refer to the following example.

{% tab template="document-editor/dialog",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, HyperlinkDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enableHyperlinkDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, HyperlinkDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('Hyperlink');
 }
}
```

{% endtab %}

## Table of contents dialog

This dialog allows creating and inserting table of contents at cursor position. If the table of contents already exists at cursor position, you can customize its properties.

To open this dialog, refer to the following example.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, TableOfContentsDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enableTableOfContentsDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, TableOfContentsDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('TableOfContents');
 }
}
```

## Styles Dialog

This dialog allows managing the styles in a document. It will display all the styles in the document with options to modify the properties of the existing style or create new style with the help of ‘Style dialog’. Refer to the following example.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, StyleDialogService, StylesDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enableStyleDialog]=true [enableStylesDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, StyleDialogService, StylesDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('Styles');
 }
}
```

## Style dialog

You can directly use this dialog for modifying any existing style or add new style by providing the style name.

To open this dialog, refer to the following example.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, StyleDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enableStyleDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, StyleDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('Style');
 }
}
```

## List dialog

This dialog allows creating a new list or modifying existing lists in the document.

To open this dialog, refer to the following example.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, ListDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enableListDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, ListDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('List');
 }
}
```

## Borders and shading dialog

This dialog allows customizing the border style, border width, and background color of the table or selected cells.

To open this dialog, refer to the following example.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, BordersAndShadingDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enableBordersAndShadingDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, BordersAndShadingDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('BordersAndShading');
 }
}
```

## Table options dialog

This dialog allows customizing the default cell margins and spacing between each cells of the selected table.

To open this dialog, refer to the following example.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, TableOptionsDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enableTableOptionsDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, TableOptionsDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('TableOptions');
 }
}
```

## Table properties dialog

This dialog allows customizing the table, row, and cell properties of the selected table.

To open this dialog, refer to the following example.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, TableOptionsDialogService, TablePropertiesDialogService, BordersAndShadingDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enableTableOptionsDialog]=true [enableTablePropertiesDialog]=true [enableBordersAndShadingDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, TableOptionsDialogService, TablePropertiesDialogService, BordersAndShadingDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('TableProperties');
 }
}
```

## Page setup dialog

This dialog allows customizing margins, size, and layout options for pages of the section.

To open this dialog, refer to the following example.

{% tab template="document-editor/dialog",isDefaultActive=false, sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import {
    DocumentEditorComponent, SfdtExportService, SelectionService, PageSetupDialogService, EditorService
} from '@syncfusion/ej2-angular-documenteditor';

@Component({
    selector: 'app-container',
    template: `<div style="height:330px">
    <button ejs-button (click)="btnClick()" >Show Dialog</button>
    <ejs-documenteditor #document_editor  id="container" style="width: 100%;height: 100%;display:block" [isReadOnly]=false [enableSfdtExport]=true
    [enablePageSetupDialog]=true [enableEditor]=true>
    </ejs-documenteditor>
    </div>`,
    encapsulation: ViewEncapsulation.None,
    providers: [SfdtExportService, SelectionService, PageSetupDialogService, EditorService]
})

export class AppComponent {
 @ViewChild('document_editor')
 public documentEditor: DocumentEditorComponent;

 public btnClick() :void {
    this.documentEditor.showDialog('PageSetup');
 }
}
```

{% endtab %}

## See Also

* [Feature module](../document-editor/feature-module/)