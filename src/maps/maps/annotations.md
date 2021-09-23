---
title: "Annotations in Angular Maps control | Syncfusion"

component: "Maps"

description: "Learn here all about Annotations feature of Syncfusion Blazor Maps (SfMaps) control and more."
---

# Annotations in Angular Maps

<!-- markdownlint-disable MD013 -->

Annotations are used to mark the specific area of interest in the Maps with texts, shapes, or images. Any number of annotations can be added to the Maps control.

## Annotation

By using the [`content`](../api/maps/annotationModel/#content) property of [`annotations`](../api/maps/annotationModel), text content or id of an element or an HTML string can be specified to render a new HTML element in Maps.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Annotations } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';

Maps.Inject(Annotations);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' style="display:block" [annotations]='annotations'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    public annotations: object;
    public shapeData: object;
        ngOnInit(): void {
            this.annotations = [{
                content: '<div id="first"><h1>Maps</h1></div>',
                x: '0%', y: '50%',
                zIndex: '-1'
            }];
            this.shapeData = world_map
        }
}
```

{% endtab %}

## Annotation customization

### Changing the z-index

The stack order of an annotation element can be changed using the [`zIndex`](../api/maps/annotationModel/#zindex) property in the [`annotations`](../api/maps/annotationModel).

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Annotations } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Annotations);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' style="display:block" [annotations]='annotations'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    public annotations: object;
    public shapeData: object;
        ngOnInit(): void {
            this.annotations = [{
                content: '<div id="first"><h1>Maps</h1></div>',
                x: '0%', y: '50%',
                zIndex: '-1'
            }];
        this.shapeData = world_map
    }
}
```

{% endtab %}

### Positioning an annotation

Annotations can be placed anywhere in the Maps by specifying pixel or percentage values to the [`x`](../api/maps/annotationModel/#x) and [`y`](../api/maps/annotationModel/#y) properties in the [`annotations`](../api/maps/annotationModel).

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Annotations } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Annotations);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' style="display:block" [annotations]='annotations'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    public annotations: object;
    public shapeData: object
    ngOnInit(): void {
        this.annotations = [{
            content: '<div id="first"><h1>Maps</h1></div>',
            x: '20%', y: '50%',
            zIndex: '-1'
        }];
        this.shapeData = world_map
    }
}
```

{% endtab %}

### Alignment of an annotation

Annotations can be aligned using the [`horizontalAlignment`](../api/maps/annotationModel/#horizontalalignment) and [`verticalAlignment`](../api/maps/annotationModel/#verticalalignment) properties in the [`annotations`](../api/maps/annotationModel). The possible values can be **Center**, **Far**, **Near** and **None**.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Annotations } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Annotations);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' style="display:block" [annotations]='annotations'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    public annotations: object;
    public shapeData: object;
    ngOnInit(): void {
        this.annotations = [{
            content: '<div id="first"><h1>Maps</h1></div>',
            verticalAlignment: 'Center',
            horizontalAlignment: 'Center',
            x: '20%', y: '50%',
            zIndex: '-1'
        }];
        this.shapeData = world_map
    }
}
```

{% endtab %}

## Multiple Annotation

Multiple annotations can be added to the Maps using the [`annotations`](../api/maps/annotationModel) in which the properties of annotations are added as an array. The customization for the annotations can be done with the [`annotations`](../api/maps/annotationModel).

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, OnInit } from '@angular/core';
import { Maps, Annotations } from '@syncfusion/ej2-angular-maps';
import { world_map } from 'world-map.ts';
Maps.Inject(Annotations);
@Component({
    selector: 'app-container',
    template:
    `<ejs-maps id='rn-container' style="display:block" [annotations]='annotations'>
    <e-layers>
    <e-layer  [shapeData]= 'shapeData'></e-layer>
    </e-layers>
    </ejs-maps>`
})

export class AppComponent implements OnInit {
    public annotations: object;
    public shapeData: object;
    ngOnInit(): void {
        this.annotations = [{
            content: '<div id="first"><h1>Maps-Annotation</h1></div>',
            x: '50%', y: '0%',
            zIndex: '-1'
        },
        {
            content: '<div id="first"><h1>Maps</h1></div>',
            x: '20%', y: '50%',
            zIndex: '-1'
        }];
        this.shapeData = world_map
    }
}
```

{% endtab %}