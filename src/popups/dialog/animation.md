---
title: "Angular Dialog Animation"
component: "Dialog"
description: "Explains how to open or close the modal dialog component with various animation effects, duration, and delay (animation dialog box)."
---

# Animation

The Dialog can be animated during the open and close actions. Also, user can
customize animation's [`delay`](../api/dialog/animationSettings/#delay),
[`duration`](../api/dialog/animationSettings/#duration)
and [`effect`](../api/dialog/animationSettings/#effect).

<!-- markdownlint-disable MD033 -->
<table>
<tr>
<td>
delay</td><td>
The Dialog animation will start with the mentioned delay</td></tr>
<tr>
<td>
duration</td><td>
Specifies the animation duration to complete with one animation cycle</td></tr>
<tr>
<td>
effect</td><td>
Specifies the animation effects of Dialog open and close actions effect.
<br /><br />
List of supported animation effects:
<br />
'Fade' | 'FadeZoom' | 'FlipLeftDown' | 'FlipLeftUp' | 'FlipRightDown' | 'FlipRightUp' | 'FlipXDown' |
'FlipXUp' | 'FlipYLeft' | 'FlipYRight' | 'SlideBottom' | 'SlideLeft' | 'SlideRight' | 'SlideTop' |
'Zoom'| 'None'
<br /><br />
If the user sets ‘Fade’ effect, then the Dialog will open with ‘FadeIn’ effect and close with ‘FadeOut’ effect
</td></tr>
</table>

In the below sample, `Zoom` effect is enabled. So, The Dialog will open with `ZoomIn`
and close with `ZoomOut` effects.

{% tab template="dialog/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript

import { Component, ViewChild, OnInit, ElementRef } from '@angular/core';
import { DialogComponent } from '@syncfusion/ej2-angular-popups';
import { EmitType } from '@syncfusion/ej2-base';

@Component({
    selector: 'app-root',
    template: `
    <button class="e-control e-btn" style="position: absolute;" id="targetButton" (click)="onOpenDialog($event)">Open Dialog</button>
    <div #container class='root-container'></div>
      <ejs-dialog id='dialog' #ejDialog header='Dialog' content='Dialog enabled with Zoom effect' [target]='targetElement'
      [animationSettings]='animationSettings' width='250px' [buttons]='buttons'>
      </ejs-dialog>
        `
})

export class AppComponent implements OnInit {
    @ViewChild('ejDialog') ejDialog: DialogComponent;
    // Create element reference for dialog target element.
    @ViewChild('container', { read: ElementRef }) container: ElementRef;
    // The Dialog shows within the target element.
    public targetElement: HTMLElement;

    //To get all element of the dialog component after component get initialized.
    ngOnInit() {
      this.initilaizeTarget();
    }

    // Initialize the Dialog component target element.
    public initilaizeTarget: EmitType<object> = () => {
      this.targetElement = this.container.nativeElement.parentElement;
    }

    // Hide the Dialog when click the footer button.
    public hideDialog: EmitType<object> = () => {
        this.ejDialog.hide();
    }
    // Sample level code to handle the button click action
    public onOpenDialog = function(event:any): void {
        // Call the show method to open the Dialog
        this.ejDialog.show();
    }
    //Animation options
    public animationSettings: Object = { effect: 'Zoom', duration: 400, delay: 0 };
    // Enables the footer buttons
    public buttons: Object = [
        {
            'click': this.hideDialog.bind(this),buttonModel:{ content:'OK', isPrimary: true }
        },
        {
            'click': this.hideDialog.bind(this),buttonModel:{ content:'Cancel' }
        }
    ];
}

```

{% endtab %}
