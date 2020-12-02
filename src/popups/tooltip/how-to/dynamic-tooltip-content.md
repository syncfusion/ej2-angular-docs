# Dynamic tooltip content

The tooltip content can be changed dynamically using the [AJAX](https://ej2.syncfusion.com/documentation/api/base/ajax/) request.

The AJAX request should be made within the [`beforeRender`](https://ej2.syncfusion.com/angular/documentation/api/tooltip/#beforerender) event of the tooltip. On every success, the corresponding retrieved data will be set to the [content](https://ej2.syncfusion.com/angular/documentation/api/tooltip/#content) property of the tooltip.

When you hover over the icons, its respective data will be retrieved dynamically and then assigned to the tooltip’s content.

Refer to the following code snippet to change the tooltip content dynamically.

```typescript

onBeforeRender(args: TooltipEventArgs): void {
    this.content = 'Loading...';
    this.dataBind();
    let ajax: Ajax = new Ajax('./tooltip.json', 'GET', true);
    ajax.send().then(
        (result: any) => {
            result = JSON.parse(result);
            for (let i: number = 0; i < result.length; i++) {
                if (result[i].Id == args.target.id) {
                    /* tslint:disable */
                    this.content = result[i].Name;
                    /* tslint:enable */
                }
            }
            this.dataBind();
        },
        (reason: any) => {
            this.content = reason.message;
            this.dataBind();
        });
}

```

{% tab template="tooltip/dynamic-content", isDefaultActive=true, sourceFiles="app/**/*.ts,index.css,tooltipdata.json"  %}

```typescript

import { Component, ViewChild } from '@angular/core';
import { Ajax } from '@syncfusion/ej2-base';
import {TooltipEventArgs } from '@synfusion/ej2-popus';
@Component({
    selector: 'my-app',
    template: `
    <div id="tool">
     <h2> Dynamic Tooltip content </h2>
      <ejs-tooltip #tooltip id='tooltip' content='Loading...' target=".circletool" [showTipPointer]='false' (beforeRender)="onBeforeRender($event)">
              <div id="box">
                <div id='1' class="circletool bold-01"></div>
                <div id='2' class="circletool italic"></div>
                <div id='3' class="circletool underline-02"></div>
                <div id='4' class="circletool cut-02"></div>
                <div id='5' class="circletool copy"></div>
                <div id='6' class="circletool paste"></div>
              </div>
      </ejs-tooltip>
    </div>
    `,
})

export class AppComponent  {
   @ViewChild('tooltip')
    public tooltipControl: TooltipComponent;
  constructor(){}
  onBeforeRender(args: TooltipEventArgs): void {
    this.tooltipControl.content = 'Loading...';
    this.tooltipControl.dataBind();
    let ajax: Ajax = new Ajax('./tooltipdata.json', 'GET', true);
    ajax.send().then(
        (result: any) => {
            result = JSON.parse(result);
            for (let i: number = 0; i < result.length; i++) {
                if (result[i].Id == args.target.id) {
                    /* tslint:disable */
                    this.tooltipControl.content = result[i].Name;
                    /* tslint:enable */
                }
            }
            this.tooltipControl.dataBind();
        },
        (reason: any) => {
            this.tooltipControl.content = reason.message;
            this.tooltipControl.dataBind();
        });
}
}

```

{% endtab %}
