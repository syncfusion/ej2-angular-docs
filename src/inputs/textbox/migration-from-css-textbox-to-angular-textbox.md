---
title: "Migration from CSS textbox to Angular textbox component"
component: "Textbox"
description: "Explains the common steps for migrating from css textbox to angular textbox along with its key features such as a floating label, adding icons (input group), and ripple effect."
---

# Angular textbox component

> From v16.3.21 version, the textbox is provided as Angular component to achieve the floating label textbox with minimal code. You can find the available textbox properties, methods, and events in the [API reference](https://ej2.syncfusion.com/angular/documentation/api/textbox/).

The following table describes the migration from CSS textbox to Angular textbox component.

## Normal textbox

<!-- markdownlint-disable MD038 -->
| **Rendering mode** | **CSS textbox** | **Angular textbox component** |
| -----------------------| -----------------------------------| ------------------------------------------- |
| Default rendering |  `<div class='e-input-group'>`<br/>`<input class='e-input' type='text' placeholder='Enter Value'/>`<br/>`</div>` |  `<ejs-textbox id="default" placeholder="Enter Value" floatLabelType="Never"></ejs-textbox>` |
| Textbox with clear button |  `<div class='e-input-group'>`<br/>`<input class='e-input' placeholder='Enter Value' required='true'>`<br/>`<span class='e-clear-icon'></span>`<br/>`</div>`<br/><br/>Note: You have to write action for clear button. |  `<ejs-textbox id="clear-input" placeholder="Enter Value" floatLabelType="Never" [showClearButton]="true"></ejs-textbox>` |
| Validation states |  `<div class='e-input-group e-error'>`<br/>`<input class='e-input' type='text' placeholder='Enter Value' />`<br/>`</div>`<br/><br/> Note: Textbox component consists of three types of validation rules such as success, warning, and error. |  `<ejs-textbox id="validation" placeholder="Enter Value" floatLabelType="Never" cssClass="e-error"></ejs-textbox>` |

## Floating label textbox

<!-- markdownlint-disable MD038 -->
| **Rendering mode** | **CSS textbox** | **Angular textbox component** |
| -----------------------| -----------------------------------| ------------------------------------------- |
| Default rendering |  `<div class='e-float-input'>`<br/>`<input type='text' required />`<br/>`<span class='e-float-line'></span>`<br/>`<label class='e-float-text'>Enter Value</label>`<br/>`</div>` |  `<ejs-textbox id="default" placeholder="Enter Value" floatLabelType="Auto"></ejs-textbox>` |
| Textbox with clear button |  `<div class='e-float-input e-input-group'>`<br/>`<input type='text' required  value= 'Clear Input' />`<br/>`<span class='e-float-line'></span>`<br/>`<label class='e-float-text'>Enter Value</label>`<br/>`<span class='e-clear-icon'></span>`<br/>`</div>`<br/><br/>Note: You have to write action for clear button. |  `<ejs-textbox id="clear-input" placeholder="Enter Value" floatLabelType="Auto" [showClearButton]="true"></ejs-textbox>` |
| Validation states |  `<div class='e-float-input e-error'>`<br/>`<input type='text' required  />`<br/>`<span class='e-float-line'></span>`<br/>`<label class='e-float-text'>Enter Value</label>`<br/>`</div>`<br/><br/> Note: Textbox component consists of three types of validation rules such as success, warning, and error. |  `<ejs-textbox id="validation" placeholder="Enter Value" floatLabelType="Auto" cssClass="e-error"></ejs-textbox>` |