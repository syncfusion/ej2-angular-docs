---
title: "Annotation and Label"
component: "ProgressBar"
description: "ProgressBar component  supports the annotation and label"
---
# Annotation and Label

## Annotation

In the circular progress bar, you can add any view to the center using the **Content** property in annotation.

For example, you can include add, start, or pause button to control the progress. You can also add an image that indicates the actual task in progress or add custom text that conveys how far the task is completed.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
@Component({
    selector: 'app-container',
    template:
   ` <ejs-progressbar  id='percentage' type='Circular' trackColor='#FFD939' cornerRadius='Round'
       innerRadius='190%' [trackThickness]='trackThickness'
      >
      <e-progressbar-annotations>
        <e-progressbar-annotation
          content='<div id="point1" style="font-size:20px;font-weight:bold;color:#ffffff;fill:#ffffff"><span>60%</span></div>'
        </e-progressbar-annotation>
       </e-progressbar-annotations>

     </ejs-progressbar>`
})
export class AppComponent implements OnInit {
    public trackThickness: number;
    ngOnInit(): void {
        this.trackThickness = 80;
    }
}
```

## Label

You can show the progress value in both linear and cicular progress bar using **showProgressValue** property.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
import { FontModel,AnimationModel, ITextRenderEventArgs } from '@syncfusion/ej2-progressbar';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-progressbar  id='percentage' type='Linear' [trackThickness]='trackThickness'  [progressThickness]=    'progressThickness'  [value]=' value'   [labelStyle]='labelStyle'    [textRender]='textRender'   [showProgressValue]='showProgressValue' [animation]='animation'>
     </ejs-progressbar>`
})
export class AppComponent implements OnInit {
    public animation: AnimationModel;
    public value: number;
    public trackThickness: number;
    public progressThickness: number;
    public labelStyle: FontModel;
    public showProgressValue: boolean;
    public textRender2(args: ITextRenderEventArgs): void {
        args.text = '50';
     }
    ngOnInit(): void {
        this.trackThickness = 24;
        this.progressThickness = 24;
        this.value = 50;
        this.animation = { enable: true, duration: 2000, delay: 0 };
        this.labelStyle = { color: '#FFFFFF' };
        this.showProgressValue = true;
}
}
```
