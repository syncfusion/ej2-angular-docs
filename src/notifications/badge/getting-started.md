---
title: "Getting Started For Badge"
component: "Badge"
description: "Angular getting started with Badge, a pure CSS component."
---

# Getting Started

The following section explains the steps required to create a simple badge component using styles and its basic usage.

## Dependencies

The `Badge` component is pure CSS component which doesn't need specific dependencies to render.

```javascript
|-- @syncfusion/ej2-notifications
```

## Installation and configuration

* To setup basic `Angular` sample use the following commands.

```javascript
git clone https://github.com/angular/quickstart.git quickstart
cd quickstart
npm install
```

For more information, refer to [Angular sample setup](https://angular.io/guide/setup-local).

* Install Syncfusion notifications package using below command.

```javascript
npm install @syncfusion/ej2-notifications --save
```

* The Badge component CSS files are available in the `ej2-notifications` package folder. This can
be referenced in your application using the following code.

`[src/styles.css]`

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-notifications/styles/material.css';
```

## Add badge into application

Modify the `template` in `app.component.ts` file to render the Badge component.

`[src/app/app.component.ts]`

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<div id='element'><h1>Badge Component <span class="e-badge">New</span></h1></div>`
})

export class AppComponent {}
```

## Run the application

Run the application in the browser using the following command.

```html
npm start
```

The following example shows a basic badge component.

{% tab template="badge/getting-started", isDefaultActive=true, sourceFiles="app/**/*.ts", index.css" %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<div id='element'><h1>Badge Component <span class="e-badge">New</span></h1></div>`
})

export class AppComponent {}
```

{% endtab %}

## See Also

[Types of Badge](./types)