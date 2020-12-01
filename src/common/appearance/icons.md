# Icons Library

The Syncfusion Angular UI Components provides the set of `base64` formatted font icons, that can be utilized in the web application.

## Steps to Use Icon

1. Add a class `e-icons` to the HTML element that shows the icon. This class contains the font-family and common property of the font icons.

2. Add the icon class with corresponding icon content from the [available icons](#available-icons). For example, the below code snippet represents the search icon class.

    ```css
    .e-search:before{
        content:'\e993';
    }
    ```

3. Add `e-icons` and `e-search` class to the HTML element.

    ```html
    <span class="e-icons e-search"></span>
    ```

    The below code snippet represents the complete example of icon usage.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <style>
            .e-search:before{
                content:'\e993';
            }
            .e-upload:before{
                content: '\e725';
            }
            .e-font:before{
                content: '\e34c';
            }
    </style>

<h1>
    Hello Angular, Syncfusion Angular UI!
 </h1>
<div class="icons">
    <ul>
        <li><span class="e-icons e-search"></span></li>
        <li><span class="e-icons e-settings"></span></li>
        <li><span class="e-icons e-upload"></span></li>
        <li><span class="e-icons e-font"></span></li>
    </ul>
</div>

 `
 })
export class AppComponent {
}
```

## Customization

The Essential JS 2 icon library can be customize icon color, size by overriding the `e-icons` class.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <style>
            .e-icons{
                color: #00ffff;
                font-size: 26px;
            }
            .e-search:before{
                content:'\e993';
            }
            .e-upload:before{
                content: '\e725';
            }
            .e-font:before{
                content: '\e34c';
            }
    </style>

<h1>
    Hello Angular, Syncfusion Angular UI!
 </h1>
<div class="icons">
    <ul>
        <li><span class="e-icons e-search"></span></li>
        <li><span class="e-icons e-settings"></span></li>
        <li><span class="e-icons e-upload"></span></li>
        <li><span class="e-icons e-font"></span></li>
    </ul>
</div>

 `
 })
export class AppComponent {
}
```

## Available Icons

The complete pack of Essential JS 2 icons are listed in the following table. The corresponding icon content can be referred in the content section.

<!-- markdownlint-disable MD033 -->

### Material

<iframe class="doc-sample-frame" src="https://ej2.syncfusion.com/products/icons/material/demo.html" style="height:1000px;"></iframe>

### Fabric

<iframe class="doc-sample-frame" src="https://ej2.syncfusion.com/products/icons/fabric/demo.html" style="height:1000px;"></iframe>

### Bootstrap

<iframe class="doc-sample-frame" src="https://ej2.syncfusion.com/products/icons/bootstrap/demo.html" style="height:1000px;"></iframe>

### Bootstrap 4

<iframe class="doc-sample-frame" src="https://ej2.syncfusion.com/products/icons/bootstrap4/demo.html" style="height:1000px;"></iframe>

### High Contrast

<iframe class="doc-sample-frame" src="https://ej2.syncfusion.com/products/icons/highcontrast/demo.html" style="height:1000px;"></iframe>