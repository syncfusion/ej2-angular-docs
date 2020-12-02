---
title: "Tooltip Content"
component: "Tooltip"
description: "Angular tooltip component's content can be assigned with static text, template, or loaded dynamically via AJAX."
---

# Content

A text or a piece of information assigned to the Tooltip's `content` property will be displayed as the main text stream of the Tooltip.
 It can be a string or a template content. If the `content` property is not provided with any specific value, then it takes the value
  assigned to the `title` attribute of the target element on which the Tooltip was initialized. The content can also dynamically be
   assigned to the Tooltip via AJAX.

## Template content

Any text or image can be added to the Tooltip, by default. To customize the Tooltip layout or to create your own
visualized element on the Tooltip, `template` can be used.

Tooltip template content can be rendered using the `ng-template`. If needed it can be rendered using the `HTML` elements also.

The following sample demonstrates how to add content template in tooltip.

{% tab template="tooltip/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts,index.css"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `
    <span>Using ng-template</span>
    <p>A green home is a type of house designed to be
        <ejs-tooltip id='tooltip_1'>
            <ng-template #content>
                <h3>Template Content</h3>
                <p><strong>Environmentally friendly</strong> or <strong>environment-friendly</strong>, <i>(also referred to as eco-friendly, nature-friendly, and green)</i> are marketing and sustainability terms referring to goods and services, laws, guidelines and policies that inflict reduced, minimal, or no harm upon ecosystems or the environment.</p>
            </ng-template>
            <a><u>environmentally friendly</u></a>
        </ejs-tooltip> and sustainable. And also focuses on the efficient use of "energy, water, and building materials."
    </p>
    <span>Using HTML Elements</span>
    <p>
        As
        <ejs-tooltip id='tooltip_2' [content]='tooltipContent'>
            <a><u>green homes</u></a>
        </ejs-tooltip>
        have become more prevalent we have also seen the emergence of green affordable housing.
    </p>
    `
})

export class AppComponent {
    tooltipContent: HTMLElement = document.createElement('div');
    constructor() {
        this.tooltipContent = '<h3>HTML Content</h3><p><strong>Environmentally friendly</strong> or <strong>environment-friendly</strong>, <i>(also referred to as eco-friendly, nature-friendly, and green)</i> are marketing and sustainability terms referring to goods and services, laws, guidelines and policies that inflict reduced, minimal, or no harm upon ecosystems or the environment.</p>'
    }
}

```

{% endtab %}

## Dynamic content via AJAX

The Tooltip content can be dynamically loaded  by making use of the AJAX call. The AJAX request is usually made within the `beforeRender`
 event of the Tooltip, and then the Tooltip's `content` is assigned the value retrieved on it's success.

{% tab template="tooltip/ajax-content", isDefaultActive=true, sourceFiles="app/**/*.ts,tooltipdata.json"  %}

```typescript
import { Component, ViewChild, Inject } from '@angular/core';
import { TooltipComponent, TooltipEventArgs } from '@syncfusion/ej2-angular-popups';
import { Http } from '@angular/http';
import 'rxjs/add/operator/map';

@Component({
    selector: 'my-app',
    template: `
        <div id="tool">
        <h4>National Sports</h4>
        <ejs-tooltip #tooltip id="tooltip" class="e-prevent-select" content='Loading...' target="#countryList [title]"
         position='RightCenter' (beforeRender)="onBeforeRender($event)">
            <div id="countryList">
                <ul>
                    <li class="target" title="1"><span>Australia</span></li>
                    <li class="target" title="2"><span>Bhutan</span></li>
                    <li class="target" title="3"><span>China</span></li>
                    <li class="target" title="4"><span>Cuba</span></li>
                    <li class="target" title="5"><span>India</span></li>
                    <li class="target" title="6"><span>Switzerland</span></li>
                    <li class="target" title="7"><span>United States</span></li>
                </ul>
            </div>
        </ejs-tooltip>
        </div>
        `,
    styles: [`
        #countryList {
          padding: 5px;
        }

        #countryList ul {
          list-style-type: none;
          margin: 0;
          padding: 0;
          width: 100px;
          border: 1px solid #c4c4c4;
        }

        #countryList li {
          padding: 10px;
        }

        #countryList li:hover {
          background-color: #ececec;
        }

        .contentWrap {
          padding: 3px 0;
          line-height: 16px;
        }

        .def {
          float: right;
        }
        #tool {
          width: 350px;
          position: relative;
          left: 50%;
          transform: translateX(-25%);
        }
        `]
})

export class AppComponent {
    @ViewChild('tooltip')
    public tooltipControl: TooltipComponent;
    constructor( @Inject(Http) public http: Http) { }

    onBeforeRender(args: TooltipEventArgs) {
        this.http.get('tooltipdata.json')
            .map(res => res.json())
            .subscribe(
            (result: any) => {
                for (let i: number = 0; i < result.length; i++) {
                    if (result[i].Id === args.target.getAttribute('data-content')) {
                        this.tooltipControl.content = "<div class='contentWrap'><div class='def'>" + result[i].Sports + "</div></div>";
                    }
                }
                this.tooltipControl.dataBind();
            },
            (err: Response) => {
                this.tooltipControl.content = err.statusText;
                this.tooltipControl.dataBind();
            });
    }
}

```

{% endtab %}
