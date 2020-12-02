---
title: "ProgressButton Spinner and Progress"
component: "ProgressButton"
description: "Angular ProgressButton allows the user to change size & position of the spinner, customize spinner using template and to change the progress."
---

<!-- markdownlint-disable MD002 MD022 -->
## Spinner

### Change spinner position

Spinner position can be changed by modifying the [`position`](../api/progress-button/spinSettingsModel#position) property of [`spinSettingsModel`](../api/progress-button/spinSettingsModel). By default, the spinner is positioned at the left of the ProgressButton. You can position it at the `left`, `right`, `top`, `bottom`, or `center` of the text content.

### Change spinner size

Spinner size can be changed by modifying the [`width`](../api/progress-button/spinSettingsModel#width) property of [`spinSettingsModel`](../api/progress-button/spinSettingsModel). In this demo, the `width` is set to `20` to change the spinner size.

### Spinner template

You can use custom spinner by specifying the [`template`](../api/progress-button/spinSettingsModel#template) property of [`spinSettingsModel`](../api/progress-button/spinSettingsModel) with custom styles.

The following sample demonstrates the above functionalities of the spinner.

{% tab template="progress-button/default", sourceFiles="app/**/*.ts,spinner.css", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { SpinSettingsModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<!-- To render progress button. -->
               <button ejs-progressbutton content='Submit' [spinSettings]='spinSettings'></button>`
})

export class AppComponent {
    private spinSettings : SpinSettingsModel = { position: 'Right', width: 20, template: '<div class="template"></div>'  };
}
```

{% endtab %}

## Progress

### Content animation

The [`content`](../api/progress-button#content) of the ProgressButton can be animated during progress using the [`effect`](../api/progress-button/animationSettingsModel#effect) property of [`animationSettingsModel`](../api/progress-button/animationSettingsModel). You can also set custom duration and timing function using the [`duration`](../api/progress-button/animationSettingsModel#duration) and [`easing`](../api/progress-button/animationSettingsModel#easing) properties. The possible `effect` values are `None`, `SlideLeft`, `SlideRight`, `SlideUp`, `SlideDown`, `ZoomIn`, and `ZoomOut`.

{% tab template="progress-button/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { SpinSettingsModel, AnimationSettingsModel } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<button ejs-progressbutton content='Slide Left' [enableProgress]='true' [animationSettings]= 'animationSettings' [spinSettings]='spinSettings'></button>`
})

export class AppComponent {
    private spinSettings : SpinSettingsModel = { position: 'Center' };
    private animationSettings : AnimationSettingsModel = { effect:'SlideLeft', duration: 500, easing: 'linear' };
}
```

{% endtab %}

### Change step of the ProgressButton

The progress can be visualized at the specified interval by changing the [`step`](../api/progress-button/progressEventArgs#step) property in the [`begin`](../api/progress-button#begin) event of the ProgressButton. In this demo, the `step` property is set to `20` to show progress at every 20% increment.

{% tab template="progress-button/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ProgressEventArgs } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<button ejs-progressbutton content='Progress Step' [enableProgress]='true' (begin)='begin($event)' cssClass='e-hide-spinner'></button>`
})

export class AppComponent {
    private begin(args: ProgressEventArgs): void {
        args.step = 20;
    }
}
```

{% endtab %}

> The class `e-hide-spinner` hides the spinner in the ProgressButton, For more information, see [hide spinner](./how-to/hide-spinner) section.

### Change progress dynamically

The progress can be changed dynamically by modifying the [`percent`](../api/progress-button/progressEventArgs#percent) property in the ProgressButton events. In this demo, on 40% completion of progress, the `percent` property is set to `90` to show dynamic change of the progress.

{% tab template="progress-button/default", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { ProgressEventArgs } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<button ejs-progressbutton [content]='content' [enableProgress]='true' [duration]='15000' (begin)='begin($event)' (progress)='progress($event)' (end)='end($event)' cssClass='e-hide-spinner'></button>`
})

export class AppComponent {
    private content: string = 'Progress';

    private begin(args: ProgressEventArgs): void {
        this.content = 'Progress ' + args.percent + '%';
    }

    private progress(args: ProgressEventArgs): void {
        this.content = 'Progress ' + args.percent + '%';
        if (args.percent === 40) {
            args.percent = 90;
        }
    }

    private end(args: ProgressEventArgs): void {
        this.content = 'Progress ' + args.percent + '%';
    }
}
```

{% endtab %}

> The method [`dataBind`](../api/progress-button#databind) applies the property changes immediately to the component.

### Start and stop methods

You can pause and resume the progress using the [`stop`](../api/progress-button#start) and [`start`](../api/progress-button#stop) methods, respectively. In this demo, clicking the ProgressButton will pause and resume the progress.

{% tab template="progress-button/default", sourceFiles="app/**/*.ts,icon.css", isDefaultActive=true %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { ProgressButtonComponent } from '@syncfusion/ej2-angular-splitbuttons';

@Component({
    selector: 'app-root',
    template: `<button #progressBtn ejs-progressbutton [content]='content' [enableProgress]='true' [duration]='4000' (end)='end()' [iconCss]='iconCss' cssClass='e-hide-spinner' (click)="btnClick()"></button>`
})

export class AppComponent {
    @ViewChild('progressBtn')
    private progressBtn : ProgressButtonComponent;
    private content: string = 'Download';
    private iconCss: string = 'e-btn-sb-icon e-download';

    private end(): void {
        this.content = 'Download';
        this.iconCss = 'e-btn-sb-icon e-download';
    }

    private btnClick(): void {
        if(this.content === 'Download') {
            this.content = 'Pause';
            this.iconCss = 'e-btn-sb-icon e-pause';
        }
        else if(this.content === 'Pause') {
            this.content = 'Resume';
            this.iconCss = 'e-btn-sb-icon e-play';
            this.progressBtn.stop();
        }
        else if(this.content === 'Resume') {
            this.content = 'Pause';
            this.iconCss = 'e-btn-sb-icon e-pause';
            this.progressBtn.start();
        }
    }
}
```

{% endtab %}

## See Also

* [How to hide spinner](./how-to/hide-spinner)
* [Customize ProgressButton using cssClass](how-to/customize-progress-using-cssclass)