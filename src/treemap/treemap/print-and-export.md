# Print and Export

## Print

To use the print functionality, we should inject the `PrintService` into the `@NgModule.providers` and set the [`allowPrint`](../api/treemap/#allowprint) property to **true**. The rendered treemap can be printed directly from the browser by calling the method [`print`](../api/treemap/#print).

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { TreeMap } from '@syncfusion/ej2-treemap';
import { Component, ViewChild} from '@angular/core';
import { PrintService } from '@syncfusion/ej2-angular-treemap';
@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' #treemap [allowPrint]=true style='display: block;'  [dataSource]='data' weightValuePath='GDP'
    [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>  <div>
    <button id="togglebtn2" (click)='print()'>Print</button>
    </div>`,
    providers: [PrintService]
})
export class AppComponent {
    @ViewChild('treemap')
    public treemap: TreeMap;
    public data: object[] = [
    {State:"United States", GDP:17946, percentage:11.08, Rank:1},
    {State:"China", GDP:10866, percentage: 28.42, Rank:2},
    {State:"Japan", GDP:4123, percentage:-30.78, Rank:3},
    {State:"Germany", GDP:3355, percentage:-5.19, Rank:4},
    {State:"United Kingdom", GDP:2848, percentage:8.28, Rank:5},
    {State:"France", GDP:2421, percentage:-9.69, Rank:6},
    {State:"India", GDP:2073, percentage:13.65, Rank:7},
    {State:"Italy", GDP:1814, percentage:-12.45, Rank:8},
    {State:"Brazil", GDP:1774, percentage:-27.88, Rank:9},
    {State:"Canada", GDP:1550, percentage:-15.02, Rank:10}
    ];
    public leafItemSettings: object = {
        labelPath: 'State',
            labelFormat: '${State}<br>$${GDP} Trillion<br>(${percentage} %)',
            labelStyle: {
                color: '#000000'
            },
            border: {
                color: '#000000',
                width: 0.5
            },
    };
    public print() {
        this.treemap.print();
    }
}

```

{% endtab %}

## Export

### Image Export

To use the image export functionality, we should inject the `ImageExportService` into the `@NgModule.providers` and set the [`allowImageExport`](../api/treemap/#allowimageexport) property to **true**. The rendered treemap can be exported as an image using the [`export`](../api/treemap/#export) method. The method requires two parameters: image type and file name. The treemap can be exported as an image in the following formats.

* JPEG
* PNG
* SVG

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { TreeMap } from '@syncfusion/ej2-treemap';
import { Component, ViewChild } from '@angular/core';
import { ImageExportService } from '@syncfusion/ej2-angular-treemap';
@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' #treemap [allowImageExport]=true style='display: block;' [dataSource]='data' weightValuePath='GDP'
    [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>  <div>
    <button id="togglebtn2"  (click)='export()'>Export</button>
    </div>`,
    providers: [ImageExportService]
})
export class AppComponent {
    @ViewChild('treemap')
    public treemap: TreeMap;
    public data: object[] = [
    {State:"United States", GDP:17946, percentage:11.08, Rank:1},
    {State:"China", GDP:10866, percentage: 28.42, Rank:2},
    {State:"Japan", GDP:4123, percentage:-30.78, Rank:3},
    {State:"Germany", GDP:3355, percentage:-5.19, Rank:4},
    {State:"United Kingdom", GDP:2848, percentage:8.28, Rank:5},
    {State:"France", GDP:2421, percentage:-9.69, Rank:6},
    {State:"India", GDP:2073, percentage:13.65, Rank:7},
    {State:"Italy", GDP:1814, percentage:-12.45, Rank:8},
    {State:"Brazil", GDP:1774, percentage:-27.88, Rank:9},
    {State:"Canada", GDP:1550, percentage:-15.02, Rank:10}
    ];
    public leafItemSettings: object = {
        labelPath: 'State',
            labelFormat: '${State}<br>$${GDP} Trillion<br>(${percentage} %)',
            labelStyle: {
                color: '#000000'
            },
            border: {
                color: '#000000',
                width: 0.5
            },
    };
    public export() {
        this.treemap.export('PNG', 'TreeMap');
        };
}

```

{% endtab %}

We can get the image file as base64 string for the JPEG and PNG formats. The treemap can be exported to image as a base64 string using the [`export`](../api/treemap/#export) method. There are four parameters required: image type, file name, orientation of the exported PDF document which must be set as **null** for image export and finally **allowDownload** which should be set as **false** to return base64 string.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { TreeMap } from '@syncfusion/ej2-treemap';
import { Component, ViewChild } from '@angular/core';
import { ImageExportService } from '@syncfusion/ej2-angular-treemap';
@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' #treemap [allowImageExport]=true style='display: block;' [dataSource]='data' weightValuePath='GDP'
    [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>  <div>
    <button id="togglebtn2"  (click)='export()'>Export</button>
    </div>`,
    providers: [ImageExportService]
})
export class AppComponent {
    @ViewChild('treemap')
    public treemap: TreeMap;
    public data: object[] = [
    {State:"United States", GDP:17946, percentage:11.08, Rank:1},
    {State:"China", GDP:10866, percentage: 28.42, Rank:2},
    {State:"Japan", GDP:4123, percentage:-30.78, Rank:3},
    {State:"Germany", GDP:3355, percentage:-5.19, Rank:4},
    {State:"United Kingdom", GDP:2848, percentage:8.28, Rank:5},
    {State:"France", GDP:2421, percentage:-9.69, Rank:6},
    {State:"India", GDP:2073, percentage:13.65, Rank:7},
    {State:"Italy", GDP:1814, percentage:-12.45, Rank:8},
    {State:"Brazil", GDP:1774, percentage:-27.88, Rank:9},
    {State:"Canada", GDP:1550, percentage:-15.02, Rank:10}
    ];
    public leafItemSettings: object = {
        labelPath: 'State',
            labelFormat: '${State}<br>$${GDP} Trillion<br>(${percentage} %)',
            labelStyle: {
                color: '#000000'
            },
            border: {
                color: '#000000',
                width: 0.5
            },
    };
     public export() {
        const promise = this.treemap.export('PNG','TreeMap',null,false);
        promise.then((data)=>{
            document.writeln(data);
          })
        };
}

```

{% endtab %}

### PDF Export

To use the PDF export functionality, we should inject the `PdfExportService` into the `@NgModule.providers` and set the [`allowPdfExport`](../api/treemap/#allowpdfexport) property to **true**. The rendered treemap can be exported as PDF using the [`export`](../api/treemap/#export) method. The [`export`](../api/treemap/#export) method requires three parameters: file type, file name and orientation of the PDF document. The orientation setting is optional and "0" indicates portrait and "1" indicates landscape.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { TreeMap } from '@syncfusion/ej2-treemap';
import { Component, ViewChild } from '@angular/core';
import { PdfExportService } from '@syncfusion/ej2-angular-treemap';
@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' #treemap [allowPdfExport]=true style='display: block;' [dataSource]='data' weightValuePath='GDP'
    [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>  <div>
    <button id="togglebtn2"  (click)='export()'>Export</button>
    </div>`,
    providers: [PdfExportService]
})
export class AppComponent {
    @ViewChild('treemap')
    public treemap: TreeMap;
    public data: object[] = [
    {State:"United States", GDP:17946, percentage:11.08, Rank:1},
    {State:"China", GDP:10866, percentage: 28.42, Rank:2},
    {State:"Japan", GDP:4123, percentage:-30.78, Rank:3},
    {State:"Germany", GDP:3355, percentage:-5.19, Rank:4},
    {State:"United Kingdom", GDP:2848, percentage:8.28, Rank:5},
    {State:"France", GDP:2421, percentage:-9.69, Rank:6},
    {State:"India", GDP:2073, percentage:13.65, Rank:7},
    {State:"Italy", GDP:1814, percentage:-12.45, Rank:8},
    {State:"Brazil", GDP:1774, percentage:-27.88, Rank:9},
    {State:"Canada", GDP:1550, percentage:-15.02, Rank:10}
    ];
    public leafItemSettings: object = {
        labelPath: 'State',
            labelFormat: '${State}<br>$${GDP} Trillion<br>(${percentage} %)',
            labelStyle: {
                color: '#000000'
            },
            border: {
                color: '#000000',
                width: 0.5
            },
    };
    public export() {
        this.treemap.export('PDF', 'TreeMap', 0);
        };
}

```

{% endtab %}

>Note: The exporting of the treemap as base64 string is not supported in the PDF export.
