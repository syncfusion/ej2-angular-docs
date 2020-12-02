# Customization

## Customize Shape

The following properties are available in `shapeSettings` property to customize the shapes of the Maps component.

* `fill` - Customizes the shape color.
* `autofill` - Applies the default palette colors to shapes.
* `palette` - Applies own custom palette for shapes.
* `border` - Customizes the maps shape border.
* `dashArray` - Customizes the different dash array border line format.
* `opacity` - Customizes the shape opacity.

[`app.component.ts`]

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
    fill: '#33CCFF',
    border: { color: '#FFFFFF', width: 2 }
  };
}
```

{% endtab %}

[`app.module.ts`]

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

To apply default palette colors for shapes need to enable the `autofill` property.

[`app.component.ts`]

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
    autofill: true
  };
}
```

{% endtab %}

[`app.module.ts`]

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

you can apply own custom palette for shape, you need to provide the palette colors for `palette`.

[`app.component.ts`]

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
    palette: ['#33CCFF', '#FF0000', '#800000', '#FFFF00', '#808000']
  };
}
```

{% endtab %}

[`app.module.ts`]

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
// import the MapsModule for the Maps component
import { MapsModule } from '@syncfusion/ej2-angular-maps';
import { AppComponent }  from './app.component';

@NgModule({
  // declaration of ej2-angular-maps module into NgModule
  imports:      [ BrowserModule, MapsModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

Refer the `shapeSettings` [`API`](../api/maps/shapeSettingsModel) for Shape Customization.
For more customization see [`colormapping`](../maps/color-mapping) feature.

## Projection Type

By default, the maps are rendered by Mercator projection type. In this type, the maps are rendered based on coordinates, so it is not stretched.

The maps control has the following projection types:

* Mercator
* Equirectangular
* Miller
* Eckert3
* Eckert5
* Eckert6
* Winkel3
* AitOff.

[`app.component.ts`]

{% tab template="maps/default-map/datetime", sourceFiles="app/**/*.ts" %}

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { world_map } from 'world-map.ts';

@Component({
  selector: 'app-container',
  // specifies the template string for the maps component
  template:
    `<div>
      <div>
        <table id="property" title="Properties">
           <tbody>
              <tr style="height: 50px">
                  <td style="width: 60%">
                      <div>Projection Type</div>
                  </td>
                  <td style="width: 40%;">
                      <select name="projectionType" id="projectiontype" style="margin-left: -25px">
                                    <option value="Mercator">Mercator</option>
                                    <option value="Equirectangular">Equirectangular</option>
                                    <option value="Miller">Miller</option>
                                    <option value="Eckert3">Eckert3</option>
                                    <option value="Eckert5">Eckert5</option>
                                    <option value="Eckert6">Eckert6</option>
                                    <option value="Winkel3">Winkel3</option>
                                    <option value="AitOff">AitOff</option>
                                </select>
                  </td>
              </tr>
            </tbody>
          </table>
      </div>
      <div>
        <ejs-maps id='maps' #maps style="display:block;">
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
  ngAfterViewInit(){
      document.getElementById("projectiontype").onchange =function() {
      let ele: HTMLSelectElement = (<HTMLSelectElement>document.getElementById("projectiontype"));
      let maps: Maps = document.getElementById('maps').ej2_instances[0];
      maps.projectionType = <ProjectionType>ele.value;
      maps.refresh();
      }
  }
}
```

{% endtab %}