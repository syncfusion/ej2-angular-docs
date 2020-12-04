---
title: "Globalization"
component: "In-place Editor"
description: "Learn how to apply localization (l10n), internationalization (i18n), and right-to-left (RTL) format in the Essential JS 2 In-place Editor component."
---

# Globalization

## Localization

Localization library allows you to localize the default text content of the **In-place Editor** to different cultures using the [locale](../api/inplace-editor/#locale) property. **In-place Editor** following keys will be localize based on culture.

| Locale key | en-US (default) |
|------|------|
| save | Close |
| cancel | Cancel |
| loadingText | Loading... |
| editIcon | Click to edit |
| editAreaClick | Click to edit |
| editAreaDoubleClick | Double click to edit |

To load translation object in an application use `load` function of `L10n` class. In the following sample, `French` culture is set to **In-place Editor** and change the tooltip text.

{% tab template="in-place-editor/editable-on", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component, OnInit, ViewChild } from '@angular/core';
import { InPlaceEditorComponent, EditableType } from '@syncfusion/ej2-angular-inplace-editor';
import { ChangeEventArgs } from '@syncfusion/ej2-dropdowns';
import { L10n } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <div id='container'>
    <table class="table-section">
        <tr>
            <td> EditableOn: </td>
            <td>
                <ejs-dropdownlist #dropDown (change)="onChange($event)" id='dropDown' width="auto" [dataSource]='editableOnData' value='Click' placeholder="Select edit type">
                </ejs-dropdownlist>
            </td>
        </tr>
        <tr>
            <td  class="sample-td"> Enter your name: </td>
            <td  class="sample-td">
                <ejs-inplaceeditor #element id="element" mode="Inline" value="Andrew" locale="fr-BE" [model]="model"></ejs-inplaceeditor>
            </td>
        </tr>
    </table>
</div>
    `
})

export class AppComponent implements OnInit {
  @ViewChild('element') editObj: InPlaceEditorComponent;
  public model: object = { placeholder: 'Enter some text' };
  public editableOnData: string[] = ['Click', 'DblClick', 'EditIconClick'];
  public onChange(e: ChangeEventArgs): void {
    let editType: EditableType = e.itemData.value as EditableType;
    this.editObj.editableOn = editType;
    this.editObj.dataBind();
  }
  ngOnInit(): void {
    L10n.load({
      'fr-BE': {
          'inplace-editor': {
              'save': 'enregistrer',
              'cancel': 'Annuler',
              'loadingText': 'Chargement...',
              'editIcon': 'Cliquez pour éditer',
              'editAreaClick': 'Cliquez pour éditer',
              'editAreaDoubleClick': 'Double-cliquez pour éditer'
          }
      }
    });
  }
}

```

{% endtab %}

## Right to left

Specifies the direction of the **In-place Editor** component using the enableRtl property. For writing systems that require it like Arabic, Hebrew, etc., the direction can be switched to right-to-left.

> It will not change based on the locale property.

{% tab template="in-place-editor/default", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id='container'>
            <span class="content-title"> Enter your name: </span>
            <ejs-inplaceeditor #element id="element" mode="Inline" value="Andrew" enableRtl=true></ejs-inplaceeditor>
        </div>
    `
})

export class AppComponent {
}
```

{% endtab %}

## Format

Formatting is a way of representing the value in different format. You can format the following mentioned components with its `format` property, when it passed through the **In-place Editor** [model](../api/inplace-editor/#model) property.

* [DatePicker](../datepicker/date-format/)
* [DateRangePicker](../daterangepicker/globalization/#date-format-customization)
* [DateTimePicker](../../../api/datetimepicker/#format)
* [NumericTextBox](../numerictextbox/formats/#custom-formats)
* [Slider](../slider/format/)
* [TimePicker](../../../api/timepicker#format)

{% tab template="in-place-editor/format", sourceFiles="app/**/*.ts,index.html,index.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    template: `
        <div id='container'>
            <span class="content-title"> Select date: </span>
            <ejs-inplaceeditor #element id="element" type="Date" [model]="model" [value]="value"></ejs-inplaceeditor>
        </div>
    `
})

export class AppComponent {
    public model: object = { placeholder: 'Select date', format: 'yyyy-MM-dd' };
    public value: Date = new Date('11/23/2018');
}

```

{% endtab %}