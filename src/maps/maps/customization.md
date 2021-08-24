---
title: " Customization in Angular Maps control | Syncfusion "

component: "Maps"

description: "Learn here all about Customization of Syncfusion Angular Maps control and more."
---

# Customization in Angular Maps control

## Setting the size for Maps

The width and height of the Maps can be set using the [`width`](../api/maps/mapsModel/#width) and [`height`](../api/maps/mapsModel/#height) properties in the Maps control. Percentage or pixel values can be used for the height and width values.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the maps component
  template:
    `<ejs-maps id='rn-container' height='200px' width='200px'>
     <e-layers>
         <e-layer [shapeData]='shapeData' [shapeSettings]="shapeSettings"></e-layer>
    </e-layers>
    </ejs-maps>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public shapeData = world_map;
    public shapeSettings = {
        autofill: true
    }
}
```

{% endtab %}

## Maps title

The title for the Maps can be set using the [`titleSettings`](../api/maps/titleSettingsModel) property. It can be customized using the following properties.

* [`alignment`](../api/maps/titleSettingsModel/#alignment) - To customize the alignment for the text in the title for the Maps. The possible values are "**Center**", "**Near**" and "**Far**".
* [`description`](../api/maps/titleSettingsModel/#description) - To set the description of the title in Maps.
* [`text`](../api/maps/titleSettingsModel/#text) - To set the text for the title in Maps.
* [`textStyle`](../api/maps/titleSettingsModel/#textstyle) - To customize the text of the title in Maps.
* [`subtitleSettings`](../api/maps/titleSettingsModel/#subtitlesettings) - To customize the subtitle for the Maps.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the maps component
  template:
    `<ejs-maps id='rn-container' [titleSettings]='titleSettings'>
     <e-layers>
         <e-layer [shapeData]='shapeData' [shapeSettings]="shapeSettings"></e-layer>
    </e-layers>
    </ejs-maps>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public titleSettings: object = {
        text: 'Maps Control',
        textStyle: {
            color: 'red',
            fontStyle: 'italic',
            fontWeight: 'regular',
            fontFamily: 'arial',
            size: '14px'
        },
        alignment: 'Center'
    };
    public shapeData = world_map;
    public shapeSettings = {
        autofill: true
    }
}
```

{% endtab %}

## Setting theme

The Maps control supports following themes.

* Material
* Fabric
* Bootstrap
* Highcontrast
* MaterialDark
* FabricDark
* BootstrapDark
* Bootstrap4
* HighContrastLight
* Tailwind

By default, the Maps are rendered by the **"Material"** theme. The theme of the Maps component is changed using the [`theme`](../api/maps/#theme) property.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the maps component
  template:
    `<ejs-maps id='rn-container' theme="FabricDark">
     <e-layers>
         <e-layer [shapeData]='shapeData' [shapeSettings]="shapeSettings"></e-layer>
    </e-layers>
    </ejs-maps>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public shapeData = world_map;
    public shapeSettings = {
        autofill: true
    }
}
```

{% endtab %}

## Customizing Maps container

The following properties are available to customize the container in the Maps.

* [`background`](../api/maps/mapsModel/#background) - To apply the background color to the container in the Maps.
* [`border`](../api/maps/mapsModel/#border) - To customize the color, width and opacity of the border of the Maps.
* [`margin`](../api/maps/mapsModel/#margin) - To customize the margins of the Maps.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the maps component
  template:
    `<ejs-maps id='rn-container' [background]='background' [border]='border' [margin]='margin'>
     <e-layers>
         <e-layer [shapeData]='shapeData' [shapeSettings]="shapeSettings"></e-layer>
    </e-layers>
    </ejs-maps>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public background: string = '#CCD1D1';
    public border: object = {
        color: 'green',
        width: 2
    };
    public margin: object = {
        bottom: 10,
        left: 20,
        right: 20,
        top: 10
    }
    public shapeData = world_map;
    public shapeSettings = {
        autofill: true
    }
}
```

{% endtab %}

## Customizing Maps area

By default, the background color of the shape maps is set as white. To modify the background color of the Maps area, the [`background`](../api/maps/mapsAreaSettingsModel/#background) property in the [`mapsArea`](../api/maps/mapsAreaSettingsModel) is used. The border of the Maps area can be customized using [`border`](../api/maps/mapsAreaSettingsModel/#border) property in the [`mapsArea`](../api/maps/mapsAreaSettingsModel) property.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the maps component
  template:
    `<ejs-maps id='rn-container' [mapsArea]='mapsArea'>
     <e-layers>
         <e-layer [shapeData]='shapeData' [shapeSettings]="shapeSettings"></e-layer>
    </e-layers>
    </ejs-maps>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public mapsArea: object = {
        background: '#CCD1D1',
        border: {
            width: 2,
            color: 'green'
        }
    };
    public shapeData = world_map;
    public shapeSettings = {
        autofill: true
    }
}
```

{% endtab %}

## Customizing the shapes

The following properties are available in [`shapeSettings`](../api/maps/shapeSettingsModel) property to customize the shapes of the Maps component.

* [`fill`](../api/maps/shapeSettingsModel/#fill) - To apply the color to the shapes.
* [`autofill`](../api/maps/shapeSettingsModel/#autofill) - To apply the palette colors to the shapes if it is set as true.
* [`palette`](../api/maps/shapeSettingsModel/#palette) - To set the custom palette for the shapes.
* [`border`](../api/maps/shapeSettingsModel/#border) - To customize the color, width and opacity of the border of the shapes.
* [`dashArray`](../api/maps/shapeSettingsModel/#dasharray) - To define the pattern of dashes and gaps that is applied to the outline of the shapes.
* [`opacity`](../api/maps/shapeSettingsModel/#opacity) - To customize the transparency for the shapes.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the maps component
  template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer [shapeData]='shapeData' [shapeSettings]="shapeSettings"></e-layer>
    </e-layers>
  </ejs-maps>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  public shapeData = world_map;
  public shapeSettings = {
      autofill: true,
      palette: ['#33CCFF', '#FF0000', '#800000', '#FFFF00', '#808000'],
      border: {
          color: 'green',
          width: 2
      },
      dashArray: '1',
      opacity: 0.9
  };
}
```

{% endtab %}

## Setting color to the shapes from the data source

The color for each shape in the Maps can be set using the [`colorValuePath`](../api/maps/shapeSettingsModel/#colorvaluepath) property of [`shapeSettings`](../api/maps/shapeSettingsModel) property. The value for the [`colorValuePath`](../api/maps/shapeSettingsModel/#colorvaluepath) property is the field name from the data source of the [`shapeSettings`](../api/maps/shapeSettingsModel) property which contains the color values.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the maps component
  template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer [shapeData]='shapeData' [shapePropertyPath]='shapePropertyPath' [shapeDataPath]='shapeDataPath'  [dataSource]='dataSource' [shapeSettings]="shapeSettings"></e-layer>
    </e-layers>
  </ejs-maps>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public shapeData = world_map;
    public shapePropertyPath = 'continent';
    public shapeDataPath = 'continent';
    public dataSource = [
        { continent: "North America", color: '#71B081' },
        { continent: "South America", color: '#5A9A77' },
        { continent: "Africa", color: '#498770' },
        { continent: "Europe", color: '#39776C' },
        { continent: "Asia", color: '#266665' },
        { continent: "Oceania", color: '#124F5E' }
    ]
    public shapeSettings = {
        colorValuePath: 'color'
  };
}
```

{% endtab %}

## Applying border to individual shapes

The border of each shape in the Maps can be customized using the [`borderColorValuePath`](../api/maps/shapeSettingsModel/#bordercolorvaluepath) and [`borderWidthValuePath`](../api/maps/shapeSettingsModel/#borderwidthvaluepath) properties to modify the color and the width of the border respectively. The field name in the data source of the layer which contains the color and the width values must be set in the [`borderColorValuePath`](../api/maps/shapeSettingsModel/#bordercolorvaluepath) and [`borderWidthValuePath`](../api/maps/shapeSettingsModel/#borderwidthvaluepath) properties respectively. If the values of [`borderWidthValuePath`](../api/maps/shapeSettingsModel/#borderwidthvaluepath) and [`borderColorValuePath`](../api/maps/shapeSettingsModel/#bordercolorvaluepath) do not match with the field name from the data source, then the color and width of the border will be applied to the shapes using the [`border`](../api/maps/shapeSettingsModel/#border) property in the [`shapeSettings`](../api/maps/shapeSettingsModel) property.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the maps component
  template:
    `<ejs-maps id='rn-container'>
    <e-layers>
    <e-layer [shapeData]='shapeData' [shapePropertyPath]='shapePropertyPath' [shapeDataPath]='shapeDataPath'  [dataSource]='dataSource' [shapeSettings]="shapeSettings"></e-layer>
    </e-layers>
  </ejs-maps>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
    public shapeData = world_map;
    public shapePropertyPath = 'continent';
    public shapeDataPath = 'continent';
    public dataSource = [
        { continent: "North America", color: '#71B081', borderColor: '#CCFFE5', width: 2 },
        { continent: "South America", color: '#5A9A77', borderColor: 'red', width: 2 },
        { continent: "Africa", color: '#498770', borderColor: '#FFCC99', width: 2 },
        { continent: "Europe", color: '#39776C', borderColor: '#66B2FF', width: 2 },
        { continent: "Asia", color: '#266665', borderColor: '#999900', width: 2 },
        { continent: "Oceania", color: '#124F5E', borderColor: 'blue', width: 2 }
    ]
    public shapeSettings = {
        borderColorValuePath: 'borderColor',
        borderWidthValuePath: 'width',
        colorValuePath: 'color'
  };
}
```

{% endtab %}

## Projection type

The Maps control supports the following projection types:

* Mercator
* Equirectangular
* Miller
* Eckert3
* Eckert5
* Eckert6
* Winkel3
* AitOff

By default, the Maps are rendered by the "**Mercator**" projection type in which the Maps are rendered based on the coordinates. So, the Maps is not stretched. To change the type of projection in the Maps, the [`projectionType`](../api/maps/projectionType/) property is used.

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';
import { Maps, ProjectionType } from '@syncfusion/ej2-angular-maps';

@Component({
  selector: 'app-container',
  // specifies the template string for the maps component
  template:
    `<div>
      <div>
        <ejs-maps id='maps' #maps style="display:block;" projectionType="Miller">
          <e-layers>
            <e-layer [shapeData]='shapeData'></e-layer>
          </e-layers>
        </ejs-maps>
      </div>
  </div>`,
  encapsulation: ViewEncapsulation.None
})
export class AppComponent {
  public shapeData = world_map;
}
```

{% endtab %}