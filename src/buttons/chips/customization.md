# Chip Customization

This section explains the customization of styles, leading icons, avatar, and trailing icons in Chip control.

## Styles

The Chip control has the following predefined styles that can be defined using the `cssClass` property.

| Class | Description |
| -------- | -------- |
| e-primary | Represents a primary chip. |
| e-success | Represents a positive chip. |
| e-info |  Represents an informative chip. |
| e-warning | Represents a chip with caution. |
| e-danger | Represents a negative chip. |

{% tab template= "chips/customization/styles", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the Chip component
  template: `
    <ejs-chiplist id="chip">
        <e-chips>
            <e-chip text="Primary" cssClass="e-primary"></e-chip>
            <e-chip text="Success" cssClass="e-success"></e-chip>
            <e-chip text="Info" cssClass="e-info"></e-chip>
            <e-chip text="Warning" cssClass="e-warning"></e-chip>
             <e-chip text="Danger" cssClass="e-danger"></e-chip>
        </e-chips>
    </ejs-chiplist>
  `
})
export class AppComponent {

}

```

{% endtab %}

## Leading Icon

You can add and customize the leading icon of chip using the `leadingIconCss` property.

{% tab template= "chips/customization/styles", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the Chip component
  template: `
  <ejs-chiplist id="chip">
        <e-chips>
            <e-chip text="Andrew" leadingIconCss='andrew'></e-chip>
            <e-chip text="Janet" leadingIconCss='janet'></e-chip>
            <e-chip text="Laura" leadingIconCss='laura'></e-chip>
            <e-chip text="Margaret" leadingIconCss='margaret'></e-chip>
        </e-chips>
  </ejs-chiplist>
  `
})
export class AppComponent {

}

```

{% endtab %}

## Avatar

You can add and customize the avatar of chip using the `avatarIconCss` property.

{% tab template= "chips/customization/styles", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the Chip component
  template: `
  <ejs-chiplist id="chip">
        <e-chips>
            <e-chip text="Andrew" avatarIconCss='andrew'></e-chip>
            <e-chip text="Janet" avatarIconCss='janet'></e-chip>
            <e-chip text="Laura" avatarIconCss='laura'></e-chip>
            <e-chip text="Margaret" avatarIconCss='margaret'></e-chip>
        </e-chips>
  </ejs-chiplist>`
})
export class AppComponent {

}

```

{% endtab %}

## Avatar Content

You can add and customize the avatar content of chip using the `avatarText` property.

{% tab template= "chips/customization/styles", sourceFiles="app/**/*.ts,styles.css", isDefaultActive=true %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the Chip component
  template: `
  <ejs-chiplist id="chip">
        <e-chips>
            <e-chip text="Andrew" avatarText= 'A'></e-chip>
            <e-chip text="Janet" avatarText= 'J'></e-chip>
            <e-chip text="Laura" avatarText= 'L'></e-chip>
            <e-chip text="Margaret" avatarText= 'M'></e-chip>
        </e-chips>
  </ejs-chiplist>`
})
export class AppComponent {

}

```

{% endtab %}

## Trailing Icon

You can add and customize the trailing icon of chip using the `trailingIconCss` property.

{% tab template= "chips/customization/styles", sourceFiles="app/**/*.ts, styles.css", isDefaultActive=true %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the Chip component
  template: `
  <ejs-chiplist id="chip">
        <e-chips>
            <e-chip text="Andrew" trailingIconCss= 'e-dlt-btn'></e-chip>
            <e-chip text="Janet" trailingIconCss= 'e-dlt-btn'></e-chip>
            <e-chip text="Laura" trailingIconCss= 'e-dlt-btn'></e-chip>
            <e-chip text="Margaret" trailingIconCss= 'e-dlt-btn'></e-chip>
        </e-chips>
  </ejs-chiplist>`
})
export class AppComponent {

}

```

{% endtab %}

## Outline Chip

Outline chip has the border with the background transparent. It can be set using the `cssClass` property.

{% tab template= "chips/customization/styles", sourceFiles="app/**/*.ts, styles.css", isDefaultActive=true %}

```typescript

import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'my-app',
  // specifies the template string for the Chip component
  template: `
  <ejs-chiplist id="chip" cssClass="e-outline">
        <e-chips>
            <e-chip text="Chai"></e-chip>
            <e-chip text="Chang"></e-chip>
            <e-chip text="Aniseed Syrup"></e-chip>
            <e-chip text="Ikura"></e-chip>
        </e-chips>
  </ejs-chiplist>
  <ejs-chiplist id="chipset" cssClass="e-outline" enableDelete="true">
        <e-chips>
            <e-chip text="Andrew"></e-chip>
            <e-chip text="Janet"></e-chip>
            <e-chip text="Laura"></e-chip>
            <e-chip text="Margaret"></e-chip>
        </e-chips>
  </ejs-chiplist>`
})
export class AppComponent {

}

```

{% endtab %}
