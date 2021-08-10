---
title: " Print And Export in Angular Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Print And Export feature of Syncfusion Angular Maps control and more."
---

# Print and Export in Angular Maps control

## Print

The rendered Maps can be printed directly from the browser by calling the [`print`](../api/maps/#print) method. To use the print functionality, the **PrintService** must be injected into the Maps using **providers** of the Angular component and set the [`allowPrint`](../api/maps/#allowprint) property to "**true**".

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Legend } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { PrintService, MapsComponent, LegendService } from '@syncfusion/ej2-angular-maps';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' #maps [allowPrint]=true [legendSettings] = 'legendSettings'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'  [shapePropertyPath]= 'shapePropertyPath' [shapeDataPath]= 'shapeDataPath' [dataSource] = 'dataSource' [shapeSettings] = 'shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>  <button  id='print' (click)='print()'>Print</button>`,
    providers: [PrintService, LegendService]
})

export class AppComponent {
    @ViewChild('maps')
    public mapObj: MapsComponent;
    public dataSource: Object[] = [
        {  "Country": "China", "Membership": "Permanent"},
        { "Country": "France", "Membership": "Permanent" },
        { "Country": "Russia", "Membership": "Permanent"},
        { "Country": "Kazakhstan", "Membership": "Non-Permanent"},
        { "Country": "Poland", "Membership": "Non-Permanent"},
        { "Country": "Sweden", "Membership": "Non-Permanent"}];
    public shapeData: Object = world_map;
    public shapePropertyPath: String = 'name';
    public shapeDataPath: String= 'Country';
    public shapeSettings: Object = {
        colorValuePath: 'Membership',
        colorMapping: [
            {
                value: 'Permanent', color: '#D84444'
            },
            {
                value: 'Non-Permanent', color: '#316DB5'
            }]
        };
    public legendSettings: Object = {
        visible: true
    };
    public print() {
        this.mapObj.print();
    };
}

```

{% endtab %}

## Export

### Image Export

To use the image export functionality in Maps, **ImageExport** module must be injected into the Maps using **Maps.Inject(ImageExport)** method and set the [`allowImageExport`](../api/maps/#allowimageexport) property to **true**. The rendered Maps can be exported as an image using the [`export`](../api/maps/#export) method. The method requires two parameters: image type and file name. The Maps can be exported as an image in the following formats.

* JPEG
* PNG
* SVG

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Legend } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { ImageExportService, MapsComponent, LegendService } from '@syncfusion/ej2-angular-maps';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' #maps [allowImageExport]=true [legendSettings] = 'legendSettings'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'  [shapePropertyPath]= 'shapePropertyPath' [shapeDataPath]= 'shapeDataPath' [dataSource] = 'dataSource' [shapeSettings] = 'shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>  <button  id='print' (click)='export()'>Export</button>`,
    providers: [ImageExportService, LegendService]
})

export class AppComponent {
     @ViewChild('maps')
    public mapObj: MapsComponent;
    public dataSource: Object[] = [
        {  "Country": "China", "Membership": "Permanent"},
        { "Country": "France", "Membership": "Permanent" },
        { "Country": "Russia", "Membership": "Permanent"},
        { "Country": "Kazakhstan", "Membership": "Non-Permanent"},
        { "Country": "Poland", "Membership": "Non-Permanent"},
        { "Country": "Sweden", "Membership": "Non-Permanent"}];
    public shapeData: Object = world_map;
    public shapePropertyPath: String = 'name';
    public shapeDataPath: String= 'Country';
    public shapeSettings: Object = {
        colorValuePath: 'Membership',
        colorMapping: [
            {
                value: 'Permanent', color: '#D84444'
            },
            {
                value: 'Non-Permanent', color: '#316DB5'
            }]
    };
    public legendSettings: Object = {
        visible: true
    };
    public export() {
        this.mapObj.export('JPEG', 'Maps');
    };
}

```

{% endtab %}

#### Exporting Maps as base64 string of the file

We can get the image file as base64 string for the JPEG and PNG formats. The rendered Maps can be exported to image as a base64 string using the [`export`](../api/maps/#export) method. There are four parameters required: image type, file name, orientation of the exported PDF document which must be set as **null** for image export and finally **allowDownload** which should be set as **false** to return base64 string.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Legend } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { ImageExportService, LegendService, MapsComponent } from '@syncfusion/ej2-angular-maps';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' #maps [allowImageExport]=true [legendSettings] = 'legendSettings'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'  [shapePropertyPath]= 'shapePropertyPath' [shapeDataPath]= 'shapeDataPath' [dataSource] = 'dataSource' [shapeSettings] = 'shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>  <button  id='print' (click)='export()'>Export</button>`,
    providers: [ImageExportService, LegendService]
})

export class AppComponent {
     @ViewChild('maps')
    public mapObj: MapsComponent;
    public dataSource: Object[] = [
        {  "Country": "China", "Membership": "Permanent"},
        {"Country": "France","Membership": "Permanent" },
        { "Country": "Russia","Membership": "Permanent"},
        {"Country": "Kazakhstan","Membership": "Non-Permanent"},
        { "Country": "Poland","Membership": "Non-Permanent"},
        {"Country": "Sweden","Membership": "Non-Permanent"}];
    public shapeData: Object = world_map;
    public shapePropertyPath: String = 'name';
    public shapeDataPath: String= 'Country';
    public shapeSettings: Object = {
        colorValuePath: 'Membership',
        colorMapping: [
            {
                value: 'Permanent', color: '#D84444'
            },
            {
                value: 'Non-Permanent', color: '#316DB5'
            }]
    };
    public legendSettings: Object = {
        visible: true
    };
    public export() {
        const promise = this.mapObj.export('PNG','Maps',null,false);
            promise.then((data)=>{
                document.writeln(data);
            })
    };
}

```

{% endtab %}

### PDF Export

To use the PDF export functionality, **PdfExport** module must be injected into the Maps using **Maps.Inject(PdfExport)** method and set the [`allowPdfExport`](../api/maps/#allowpdfexport) property to **true**. The rendered map can be exported as PDF using the [`export`](../api/maps/#export) method. The [`export`](../api/maps/#export) method requires three parameters: file type, file name and orientation of the PDF document. The orientation setting is optional and "0" indicates portrait and "1" indicates landscape.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Legend } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { PdfExportService, MapsComponent, LegendService } from '@syncfusion/ej2-angular-maps';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' #maps [allowPdfExport]=true [legendSettings] = 'legendSettings'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'  [shapePropertyPath]= 'shapePropertyPath' [shapeDataPath]= 'shapeDataPath' [dataSource] = 'dataSource' [shapeSettings] = 'shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>  <button  id='print' (click)='export()'>Export</button>`,
    providers: [PdfExportService, LegendService]
})

export class AppComponent {
    @ViewChild('maps')
    public mapObj: MapsComponent;
    public dataSource: Object[] = [
        {  "Country": "China", "Membership": "Permanent"},
        { "Country": "France", "Membership": "Permanent" },
        { "Country": "Russia", "Membership": "Permanent"},
        { "Country": "Kazakhstan", "Membership": "Non-Permanent"},
        { "Country": "Poland", "Membership": "Non-Permanent"},
        { "Country": "Sweden", "Membership": "Non-Permanent"}];
    public shapeData: Object = world_map;
    public shapePropertyPath: String = 'name';
    public shapeDataPath: String= 'Country';
    public shapeSettings: Object = {
        colorValuePath: 'Membership',
        colorMapping: [
            {
                value: 'Permanent', color: '#D84444'
            },
            {
                value: 'Non-Permanent', color: '#316DB5'
            }]
        };
    public legendSettings: Object = {
        visible: true
    };
    public export() {
        this.mapObj.export('PDF', 'Maps', 0);
    };
}

```

{% endtab %}

>Note: The exporting of the map as base64 string is not supported in the PDF export.

### Export the tile maps

The rendered Maps with providers such as OSM, Bing and Google static maps can be exported using the [`export`](../api/maps/#export) method. It supports the following export formats.

* JPEG
* PNG
* PDF

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, ViewChild } from '@angular/core';
import { Maps, Legend } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
import { PdfExportService, ImageExportService, MapsComponent, LegendService } from '@syncfusion/ej2-angular-maps';

@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' #maps [allowPdfExport]=true [allowImageExport]=true [titleSettings] = 'titleSettings'>
    <e-layers>
    <e-layer  layerType='OSM'></e-layer>
    </e-layers>
    </ejs-maps>  <button  id='export' (click)='export()'>Export</button>`,
    providers: [PdfExportService, ImageExportService, LegendService]
})

export class AppComponent implements OnInit {
    @ViewChild('maps')
    public mapObj: MapsComponent;
    ngOnInit(): void {
        public titleSettings: Object = {
            text: 'OSM'
        };
        public export() {
            this.mapObj.export('JPEG', 'Maps');
        };
    }
}

```

{% endtab %}