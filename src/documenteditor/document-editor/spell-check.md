---
title: "SpellCheck"
component: "DocumentEditor"
description: "Learn how to perform spell check in JavaScript document editor"
---

# Spell Check

Document editor supports performing spell checking for any input text. You can perform spell checking for the text in Document Editor and it will provide suggestions for the mis-spelled words through dialog and in context menu.

```typescript
import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { ToolbarService } from '@syncfusion/ej2-angular-documenteditor';

@Component({
  selector: 'app-container',
  // specifies the template string for the DocumentEditorContainer component
  template: `<ejs-documenteditorcontainer #document_editor (created)="onCreated()" [enableToolbar]=true [enableSpellCheck]=true> </ejs-documenteditorcontainer>`,
  providers: [ToolbarService]
})
export class AppComponent {
@ViewChild('document_editor')
  public container: DocumentEditorContainerComponent;
    onCreated() {
        this.container.documentEditor.spellChecker.languageID = 1033 //LCID of "en-us";
        this.container.documentEditor.spellChecker.removeUnderline = false;
        this.container.documentEditor.spellChecker.allowSpellCheckAndSuggestion = true;
    }
}
```

## Features

* Supports context menu suggestions.
* Provides built-in options to Ignore, Ignore All, Change, Change All for error words in spell checker dialog.

## Enable SpellCheck

To enable spell check in DocumentEditor, set `enableSpellCheck` property as `true` and then configure SpellCheckSettings.

## Disable SpellCheck

To disable spell check in DocumentEditor, set `enableSpellCheck` property as `false` or remove `enableSpellCheck` property initialization code. The default value of this property is false.

## Spell check settings

### Remove Underline

By default, mis-spelled words are marked with squiggly line. You can also disable this behavior by enabling the `removeUnderline` API and now, the squiggly lines will never be rendered for mis-spelled words.

```typescript
this.container.documentEditor.spellChecker.removeUnderline = false;
```

### AllowSpellCheckAndSuggestion

By default, on performing spell check in Document Editor, both spelling and suggestions of the mis-spelled words will be retrieved, and this mis-spelled words can be corrected through context menu suggestions. You can modify this behavior using the `allowSpellCheckAndSuggestion` API, which will perform only spell check.

```typescript
this.container.documentEditor.spellChecker.allowSpellCheckAndSuggestion = false;
```

### LanguageID

Document Editor provides multi-language spell check support. You can add as many languages (dictionaries) in the server-side and to use that language for spell checking in Document Editor, it must be matched with `languageID` you pass in the Document Editor.

```typescript
this.container.documentEditor.spellChecker.languageID = 1033; //LCID of "en-us";
```

* Refer to the [Spell checker](https://github.com/SyncfusionExamples/EJ2-DocumentEditor-WebServices) link for configuring spell checker in server-side.