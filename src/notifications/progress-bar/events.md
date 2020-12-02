---
title: "Events"
component: "ProgressBar"
description: "Visualize progress events"
---

# Events

## Value Change

<!-- markdownlint-disable MD033 -->

**valueChanged** event is triggered when the progress value is changed.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
import { ProgressBar, FontModel, AnimationModel, IProgressValueEventArgs } from '@syncfusion/ej2-progressbar';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-progressbar #event id='percentage' type='Linear'  trackThickness=24  progressThickness=24  value = 90 [labelStyle]='labelStyle' [valueChanged]='valueChanged' [showProgressValue]='showProgressValue' [animation]='animation'>
    </ejs-progressbar>
    <button id="reLoad" (click)="onClick()">ValueChanged</button>`
})
export class AppComponent implements OnInit {
    public animation: AnimationModel;
    public labelStyle: FontModel;
    public showProgressValue: boolean;
    @ViewChild('event')
    public event: ProgressBar;
    public valueChanged(args: IProgressValueEventArgs): void {
        args.progressColor = '#2BB20E';
    }
    public onClick = () => {
        event.value = 50;
    }
    ngOnInit(): void {
        this.animation = { enable: true, duration: 2000, delay: 0 };
        this.labelStyle = { color: '#FFFFFF' };
        this.showProgressValue = true;
    }

}

```

## ProgressCompleted

<!-- markdownlint-disable MD033 -->
**ProgressCompleted** event is triggered when the progress attains the Maximum value.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
import { FontModel, AnimationModel, IProgressValueEventArgs } from '@syncfusion/ej2-progressbar';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-progressbar id='percentage' type='Linear'  trackThickness=24  progressThickness=24  value = 100 [labelStyle]='labelStyle' [progressCompleted]='progressCompleted' [showProgressValue]='showProgressValue' [animation]='animation'>
    </ejs-progressbar>`
 })
export class AppComponent implements OnInit {
    public animation: AnimationModel;
    public labelStyle: FontModel;
    public showProgressValue: boolean;
    public progressCompleted(args: IProgressValueEventArgs): void {
        args.progressColor = '#2BB20E';
    }
    ngOnInit(): void {
        this.animation = { enable: true, duration: 2000, delay: 0 };
        this.labelStyle = { color: '#FFFFFF' };
        this.showProgressValue = true;
    }
}

```
