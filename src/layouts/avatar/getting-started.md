---
title: "Avatar Getting Started"
component: "Avatar"
description: "Angular getting started with Avatar, a pure CSS component."
---

# Getting Started

The following section explains the steps required to create a simple avatar component using styles and its basic usage.

## Dependencies

The `Avatar` component is pure CSS component which doesn't need specific dependencies to render.

```javascript
|-- @syncfusion/ej2-layouts
```

## Installation and configuration

* To setup basic `Angular` sample use the following commands.

```cmd
git clone https://github.com/angular/quickstart.git quickstart
cd quickstart
npm install
```

For more information, refer to [Angular sample setup](https://angular.io/guide/setup-local).

* Install Syncfusion notifications package using below command.

```cmd
npm install @syncfusion/ej2-layouts --save
```

* The Avatar component CSS files are available in the `ej2-layouts` package folder.
This can be referenced in your application using the following code.

`[src/styles.css]`

```css
@import '../node_modules/@syncfusion/ej2-base/styles/material.css';
@import '../node_modules/@syncfusion/ej2-layouts/styles/material.css';
```

> We can also use [CRG](https://crg.syncfusion.com/) to generate combined component styles.

## Add avatar into application

Modify the `template` in `app.component.ts` file to render avatar component.

`[src/app/app.component.ts]`

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'my-app',
    template: `<div id='element'><span class="e-avatar">GR</span></div>`
})

export class AppComponent {}
```

## Run the application

Run the application in the browser using the following command.

```html
npm start
```

The following example shows a basic avatar component.

{% tab template="avatar/getting-started", isDefaultActive = "true", sourceFiles="app/**/*.ts,index.css"  %}

```typescript

```

{% endtab %}

## See Also

[Types of Avatar](./types)