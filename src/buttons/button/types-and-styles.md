---
title: "Button Types and Styles"
component: "Button"
description: "Angular Button component supports different types, predefined styles, sizes and also has support for icons."
---

# Types and Styles

This section explains the different styles and types of Buttons.

## Button styles

The Essential JS 2 Button has the following predefined styles that can be defined using the [`cssClass`](../api/button#cssclass) property.

| Class | Description |
| -------- | -------- |
| e-primary | Used to represent a primary action. |
| e-success | Used to represent a positive action. |
| e-info |  Used to represent an informative action. |
| e-warning | Used to represent an action with caution. |
| e-danger | Used to represent a negative action. |
| e-link |  Changes the appearance of the Button like a hyperlink. |

{% tab template="button/button-style", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template:  `<!-- Primary Button - Used to represent a primary action. -->
                <button ejs-button cssClass="e-primary">Primary</button>

                <!-- Success Button - Used to represent a positive action. -->
                <button ejs-button cssClass="e-success">Success</button>

                <!-- Info Button - Used to represent an informative action -->
                <button ejs-button cssClass="e-info">Info</button>

                <!-- Warning Button - Used to represent an action with caution. -->
                <button ejs-button cssClass="e-warning">Warning</button>

                <!-- Danger Button - Used to represent a negative action. -->
                <button ejs-button cssClass="e-danger">Danger</button>

                <!-- Link Button - Changes the appearance of the Button like a hyperlink. -->
                <button ejs-button cssClass="e-link">Link</button>`
})

export class AppComponent { }
```

{% endtab %}

> Predefined Button styles provide only the visual indication. So, Button content should define the Button
style for the users of assistive technologies such as screen readers.
> Primary action button can also be achieved by setting [`isPrimary`](../api/button#isprimary) property as `true`.

## Button types

The types of Essential JS 2 Button are as follows:

* Basic types
* Flat Button
* Outline Button
* Round Button
* Toggle Button

### Basic types

The basic Button types are explained below.

| Type | Description |
| -------- | -------- |
| Button | Defines a click Button. |
| Submit | This Button submits the form data to the server. |
| Reset |  This Button resets all the controls in the form elements to their initial values. |

{% tab template="button/basic-types", sourceFiles="app/**/*.ts", isDefaultActive=true  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template:   `<form>
                    <!-- Submit type button -->
                    <button type="submit" ejs-button>Submit</button>

                    <!-- Reset type button -->
                    <button type="reset" ejs-button>Reset</button>
                </form>`
})

export class AppComponent { }
```

{% endtab %}

### Flat Button

The Flat Button is styled with no background color. To create a flat Button,
set the [`cssClass`](../api/button#cssclass) property to `e-flat`.

### Outline Button

An outline Button has a border with transparent background. To create an outline Button,
set the [`cssClass`](../api/button#cssclass) property to `e-outline`.

### Round Button

A round Button is shaped like a circle. Usually, it contains an icon representing its action.
To create a round Button, set the [`cssClass`](../api/button#cssclass) property to `e-round`.

{% tab template="button/button-type", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template:   `<!-- Flat Button. -->
                <button ejs-button cssClass="e-flat">Flat</button>

                <!-- Outline Button. -->
                <button ejs-button cssClass="e-outline">Outline</button>

                <!-- Round Button - Icon can be loaded by setting "e-icons e-plus-icon" in "iconCss" property.-->
                <!-- Use "e-icons" class name to load Essential JS 2 built-in icons.-->
                <!-- Use "e-plus-icon" class name to load plus icon that you can refer in "styles.css" -->
                <button ejs-button cssClass="e-round" iconCss="e-icons e-plus-icon" [isPrimary]="true"></button>`
})

export class AppComponent { }
```

{% endtab %}

### Toggle Button

A toggle Button allows you to change between the two states. The Button is active in toggled state and
can be recognized through the `e-active` class. The functionality of the toggle Button is handled by
by click event. To create a toggle Button, set the [`isToggle`](../api/button#istoggle)
property to `true`. In the following code snippet, the toggle Button text changes to play/pause based on the
state of the Button with the use of click event.

{% tab template="button/toggle-button", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true  %}

```typescript
import { Component, ViewChild, HostListener } from '@angular/core';
import { ButtonComponent } from '@syncfusion/ej2-angular-buttons';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template: ` <!-- Button is active in toggled state. -->
                <button #togglebtn ejs-button cssClass="e-flat" iconCss="e-btn-sb-icon e-play-icon" [isToggle]="true" content="Play"></button>`
})
// Click event handled using HostListener.
export class AppComponent {
    @ViewChild('togglebtn') togglebtn: ButtonComponent;
    @HostListener('click', ['togglebtn'])
    btnClick() {
        if(this.togglebtn.element.classList.contains('e-active')){
            this.togglebtn.content = 'Pause';
            this.togglebtn.iconCss = 'e-btn-sb-icon e-pause-icon';
        }
        else {
            this.togglebtn.content = 'Play';
            this.togglebtn.iconCss = 'e-btn-sb-icon e-play-icon';
        }
    }
 }
```

{% endtab %}

## Icons

### Button with font icons

The Button can have an icon to provide the visual representation of the action. To place the icon on a Button,
set the [`iconCss`](../api/button#iconcss) property with the required icon CSS.
By default, the icon is positioned to the left side of the Button. You can customize the icon's position
by using the [`iconPosition`](../api/button#iconposition) property.

{% tab template="button/icon", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template:  `<!-- To position the icon to the left of the text on a Button. -->
                <button ejs-button iconCss="e-btn-sb-icon e-prev-icon">Previous</button>

                <!-- To position the icon to the right of the text on a Button. -->
                <button ejs-button iconCss= "e-btn-sb-icon e-stop-icon" iconPosition="Right">Stop</button>`
})

export class AppComponent { }
```

{% endtab %}

### Button with SVG image

SVG image can be added to the Button using [`iconCss`](../api/button#iconcss) property.

In the following example, SVG image is added using the iconCss class `e-search-icon` by setting `height` and `width`.

{% tab template="button/svg", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    styleUrls: ['styles.css'],
    template:  `<button ejs-button iconCss= "e-search-icon"></button>`
})

export class AppComponent { }
```

{% endtab %}

> The Essential JS 2 provides a set of icons that can be loaded by applying `e-icons` class name to the
element. You can also use third party icons on the Button using the [`iconCss`](../api/button#iconcss) property.

## Button size

The two types of Button sizes are default and small. To change the size of the default Button
to small Button, set the [`cssClass`](../api/button#cssclass) property to `e-small`.

{% tab template="button/size", sourceFiles="app/**/*.ts", isDefaultActive=true  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector:  'app-root',
    styleUrls: ['styles.css'],
    template:  `<!-- Small Button. -->
                <button ejs-button cssClass="e-small">Small</button>

                <!-- Normal Button. -->
                <button ejs-button>Normal</button>`
})

export class AppComponent { }
```

{% endtab %}

## See Also

* [Customize Button appearance](./how-to/customize-button-appearance)
* [How to create block button](./how-to/create-a-block-button)
* [How to create repeat button](./how-to/repeat-button)