---
title: "Modes"
component: "ProgressBar"
description: "Visualize progress in different modes."
---
# Modes

Visualize progress in different modes.

## Determinate

This is the default state. You can use it when the progress estimation is known.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-progressbar  id='percentage' type='Linear' height='60' value=100>
      </ejs-progressbar>`
})
export class AppComponent implements OnInit {
    ngOnInit(): void {

}
```

## Indeterminate

By enabling the **IsIndeterminate** property, the state of the progress bar can be changed to indeterminate when the progress cannot be estimated or is not being calculated. It can be combined with determinate mode to know that the application is estimating progress before the actual progress starts.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-progressbar';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-progressbar  id='percentage' type='Linear' height='60' value=20 [isIndeterminate]='isIndeterminate'       [animation]='animation'>
      </ejs-progressbar>`
})
export class AppComponent implements OnInit {
    public isIndeterminate: boolean;
    public animation: AnimationModel;
    ngOnInit(): void {
        this.animation = true;
        this.animation = { enable: true, duration: 2000, delay: 0 };

}
```

## Buffer

You can use a secondary progress indicator when the primary progress depends on the secondary progress. This will allow users to visualize both primary and secondary progress simultaneously.

`app.component.ts`

```typescript
import { Component, OnInit } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-progressbar';
@Component({
    selector: 'app-container',
    template:
    ` <ejs-progressbar  id='percentage' type='Linear' height='60' value=40 secondaryProgress=60                     [animation]='animation'>
      </ejs-progressbar>`
})
export class AppComponent implements OnInit {
   public animation: AnimationModel;
    ngOnInit(): void {
    this.animation = { enable: true, duration: 2000, delay: 0 };
}
```
