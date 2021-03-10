---
title: "Render Accordion content using ng-content"
component: "Accordion"
description: "This example demonstrates how to render other Essential JS 2 components into Essential JS 2 Accordion component content using ng-template."
---

# Render Accordion content using ng-content

To render the Accordion contents using ng-content, we need to use ng-template inside the each `e-accordionitem`
tag with `#content` attribute, which is mandatory to render content. Now include `ng-content` inside the
`ng-template` tag with select attribute of id or class name for mapping required content.

```javascript
  <e-accordionitem expanded='true' header='Athletics'>
    <ng-template #content>
      <ng-content select='div.content0'></ng-content>
    </ng-template>
  </e-accordionitem>
```

> Here `div.content0` mapped to ng-content is reusable content. It can be used in multiple scenarios within the application.

{% tab template="accordion/accordion-ng-content", sourceFiles="app/**/*.html,app/**/*.ts" %}

```typescript

import { Component, ViewEncapsulation, Inject } from '@angular/core';

@Component({
  selector: 'my-thing',
  templateUrl: 'app/app.component.html'
})
export class AccordionComponent {}

@Component({
  selector: 'control-content',
  templateUrl: 'app/reusable-content.html',
  styleUrls: ['app/app.component.css'],
  encapsulation: ViewEncapsulation.None
})
export class MyApp {}

```

{% endtab %}
