# Annotations

Annotations are used to mark the specific area of interest in a map area with texts, shapes, or images. To
update the annotation in maps, please follow the given procedure.

Initialize the maps control with annotation option, and specify the ID of HTML element in the content that
needs to be displayed in maps area by using the `content` property. You can specify the content position
with `x` and `y` values as mentioned in the following code example. To know more about annotations, please
refer to the [`API`](../../api/maps/annotation) documentation.

[`app.module.ts`]

```typescript
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent }  from './app.component';
import { MapsModule } from '@syncfusion/ej2-angular-maps';
import { AnnotationsService } from '@syncfusion/ej2-angular-maps';


@NgModule({
  imports:      [ BrowserModule,MapsModule ],
  declarations: [ AppComponent ],
  bootstrap:    [ AppComponent ],
  providers: [AnnotationsService]
})
export class AppModule { }
```

[`app.component.ts`]

```typescript
import { Component, ViewEncapsulation } from '@angular/core';
import { africa_continent } from './MapData/africa_continent';

@Component({
    selector: 'my-app',
    // specifies the template string for the maps component
    template:`<div class="control-section">
    <div align='center'>
    <ejs-maps id='container' style="display:block;" [annotations ='annotation'>
    <e-layers>
    <e-layer [shapeData]='shapeData' [shapeSettings]='shapeSettings'></e-layer>
    </e-layers>
    </ejs-maps>
    </div>
    </div>`,
    encapsulation: ViewEncapsulation.None
  })
  export class AppComponent {
       public shapeData=africa_continent;
       public shapeSettings = {
           fill: 'url(#grad1)'
            };
    public annotation:Object[]=[
        {
            content: '<div id="maps-annotation"> <div id="annotation"> <div> <p style="margin-left:10px;font-size:13px;font-weight:500">Facts about Africa</p> </div> <hr style="margin-top:-3px;margin-bottom:10px;border:0.5px solid #DDDDDD"> <div> <ul style="list-style-type:disc; margin-left:-20px;margin-bottom:2px; font-weight:400"> <li>Africa is the second largest and second most populated continent in the world.</li> <li style="padding-top:5px;">Africa has 54 sovereign states and 10 non-sovereign territories.</li> <li style="padding-top:5px;">Algeria is the largest country in Africa, where as Mayotte is the smallest.</li> </ul> </div> </div> </div>',
            x: '0%', y: '70%'
        }, {
            content: '<div id="compass-maps"> <img src="compass.svg" width="75px" height="75px"> </div>',
            x: '85%', y: '5%'
        }
    ];
}
```

```html
 <svg height="150" width="400">
      <defs>
          <linearGradient id="grad1" x1="0%" y1="0%" x2="0%" y2="100%">
              <stop offset="0%" style="stop-color:#C5494B;stop-opacity:1"></stop>
              <stop offset="100%" style="stop-color:#4C134F;stop-opacity:1"></stop>
          </linearGradient>
      </defs>
   </svg>
   <style>
        #annotation {
          color: #DDDDDD;
          font-size: 12px;
          font-family: Roboto;
          background: #3E464C;
          margin: 20px;
          padding: 10px;
          border-radius: 2px;
          width: 300px;
          box-shadow: 0px 2px 5px #666;
         }
      </style>
```