---
title: "Data Matrix generator"
component: "BarcodeGenerator"
description: "BarcodeGenerator component is a pure JavaScript library which will convert a string to Barcode and show it to the user. This supports major 1D and 2D barcodes including coda bar, code 128, QR Code."
---

# Data Matrix generator

# Data Matrix

DataMatrix Barcode is a two dimensional barcode that consists of a grid of dark and light dots or blocks forming square or rectangular symbol. The data encoded in the barcode can either be numbers or alphanumeric. They are widely used in printed media such as labels and letters. You can read it easily with the help of a barcode reader and mobile phones.

{% tab template="barcode/datamatrix/datamatrix", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-container",
  // specifies the template string for the barcode generator component
  template: `<ejs-datamatrixgenerator style="display: block;"  #barcode id="barcode" width="200px" height="200px" mode="SVG" type="DataMatrix" value="Syncfusion"></ejs-datamatrixgenerator>`
})
export class AppComponent {}
```

{% endtab %}

## Customizing the Barcode color

A page or printed media with barcode often appears colorful in the background and surrounding region with other contents. In such cases the barcode can also be customized to suit the needs. You can achieve this by using the forecolor property .

{% tab template="barcode/datamatrix/color", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-container",
  // specifies the template string for the barcode generator component
  template: `<ejs-datamatrixgenerator style="display: block;"  #barcode id="barcode" width="200px" foreColor="red" height="200px" mode="SVG" type="DataMatrix" value="Syncfusion"></ejs-datamatrixgenerator>`
})
export class AppComponent {}
```

{% endtab %}

## Customizing the Barcode dimension

The dimension of the barcode can be changed using the height and width property of the barcodegenerator.

{% tab template="barcode/datamatrix/dimension", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from "@angular/core";

@Component({
  selector: "app-container",
  // specifies the template string for the barcode generator component
  template: `<ejs-datamatrixgenerator style="display: block;"  #barcode id="barcode" width="300px" height="300px" mode="SVG" type="DataMatrix" value="Syncfusion"></ejs-datamatrixgenerator>`
})
export class AppComponent {}
```

{% endtab %}

## Customizing the text

In barcode generators you can customize the barcode text by using the display text property .

{% tab template="barcode/datamatrix/text", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from "@angular/core";
import { Component ,ViewChild ,ViewEncapsulation} from "@angular/core";

@Component({
  selector: "app-container",
  // specifies the template string for the barcode generator component
  template: `<ejs-datamatrixgenerator style="display: block;"  #barcode id="barcode" width="200px"  height="200px" [displayText] = 'displayText' mode="SVG" type="DataMatrix" value="Syncfusion"></ejs-datamatrixgenerator>`
})
export class AppComponent {
   @ViewChild('barcode')
   @ViewChild('displayText')
   public displayText: DisplayTextModel;
   ngOnInit(): void {  

     this.displayText = {
       text:'text'
     }
   }
}
```

{% endtab %}