---
title: "Animation"
component: "ProgressBar"
description: "ProgressBar support to animate the track."
---
# Animation

<!-- markdownlint-disable MD033 -->

Progress Bar support to animate the progress by using `animation` property. Enable the animation by setting **enable** property and also you can control the speed by using **duration** property.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-progressbar';

@Component({
    selector: 'app-container',
    template: `
    <ejs-progressbar  id='percentage' type='Linear' value=100  [animation]='animation'>
    </ejs-progressbar>
    `
})
export class AppComponent implements OnInit {
   public animation: AnimationModel;
    ngOnInit(): void {
        this.animation = { enable: true, duration: 2000, delay: 0 };
}
}
```
