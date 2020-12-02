---
title: "Customization"
component: "ProgressBar"
description: "The progressBar can  be customized in various ways "
---
# Customization

## Segments

We can divide a progress bar into multiple segments using a `segmentCount` to visualize the progress of multiple sequential tasks.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-progressbar';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-progressbar  id='percentage' type='Circular' height='60' segmentCount=8 value=100                        [animation]='animation'>
     </ejs-progressbar>`
})
export class AppComponent implements OnInit {
    public animation: AnimationModel;
    ngOnInit(): void {
        this.animation = { enable: true, duration: 2000, delay: 0 };
    }

}
```

## Thickness

You can customize the thickness of the track  using `trackThickness` and progress using `progressThickness` to render the ProgressBar with different appearances.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
import { AnimationModel, FontModel } from '@syncfusion/ej2-progressbar';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-progressbar  id='percentage' type='Linear' height='60' width='90%'  trackThickness=24                     progressThickness=24 value=100 [showProgressValue]='showProgressValue' [labelStyle]='labelStyle'              [animation]='animation'>
     </ejs-progressbar>`
})
export class AppComponent implements OnInit {
    public showProgressValue: boolean;
    public labelStyle: FontModel;
    public animation: AnimationModel;
    ngOnInit(): void {
      this.labelStyle = { color: '#FFFFFF' };
      this.showProgressValue = true;
      this.animation = { enable: true, duration: 2000, delay: 0 };
    }
}
```

## Radius

The  radius of the progress bar can be customized using `radius` property and  corner can be customized by **cornerRadius** property.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-progressbar';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-progressbar  id='percentage' type='Circular' height='160px' width='160px'  trackColor='#FFD939'        radius='100%' progressColor='white' cornerRadius='Round' trackThickness=80 progressThickness=10 value=60 [animation]='animation'>
     </ejs-progressbar>`
})
export class AppComponent implements OnInit {
    public animation: AnimationModel;
    ngOnInit(): void {
        this.animation = { enable: true, duration: 2000, delay: 0 };

}
```

## InnerRadius

The inner radius of the progress bar can be customized using `innerRadius` property.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-progressbar';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-progressbar  id='percentage' type='Circular' height='160px' width='160px'  trackColor='#FFD939'        radius='100%' innerRadius='80%' progressColor='white' cornerRadius='Round' trackThickness=80 progressThickness=10 value=60 [animation]='animation'>
     </ejs-progressbar>`
})
export class AppComponent implements OnInit {
    public animation: AnimationModel;
    ngOnInit(): void {
        this.animation = { enable: true, duration: 2000, delay: 0 };

}
```

## Progress color and track color

We can customize the color of progress and track by using  **progressColor** and **trackColor** property.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
import { FontModel,AnimationModel, ITextRenderEventArgs } from '@syncfusion/ej2-progressbar';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-progressbar  id='percentage' type='Linear' height='60' width='90%' trackThickness=24             progressThickness=24  value = 50  progressColor='#E3165B' trackColor='#F8C7D8' [labelStyle]='labelStyle'    [textRender]='textRender'   [showProgressValue]='showProgressValue' [animation]='animation'>
    </ejs-progressbar>`
})
export class AppComponent implements OnInit {
    public animation: AnimationModel;
    public labelStyle: FontModel;
    public showProgressValue: boolean;
    public textRender2(args: ITextRenderEventArgs): void {
        args.text = '50';
    }
    ngOnInit(): void {
        this.animation = { enable: true, duration: 2000, delay: 0 };
        this.labelStyle = { color: '#FFFFFF' };
        this.showProgressValue = true;

}
```
