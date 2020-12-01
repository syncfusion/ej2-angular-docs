# Theming

THe Essential JS 2 has provided the below list of in-built themes those are,

1. Google’s Material
2. Microsoft Office’s Fabric
3. Bootstrap
4. High Contrast

> The Essential JS 2 Bootstrap theme is designed based on `Bootstrap v3`, however it can be compatible in `Bootstrap v4` applications. In addition to these four built-in themes, [ThemeStudio](https://ej2.syncfusion.com/angular/documentation/appearance/theme-studio/) provides support for the Fusion Theme that can only be downloaded from [ThemeStudio](https://ej2.syncfusion.com/themestudio/?theme=fusion).

Themes are shipped as individual and combined CSS files. Combined CSS file can be referred from the npm package `@syncfusion/ej2` and individual CSS files are available within same component repository’s `style` folder. In ej2 npm packages, we have shipped both CSS and SCSS files for all components.

Referring All components CSS

```css
@import "./node_modules/@syncfusion/ej2/<theme_name>.css";
```

Referring All components SCSS

```scss
@import "ej2/<theme_name>.scss";
```

## Referring Individual Component Theme

We can get the individual theme from [individual package](#anatomy-of-npm-packages) or from ej2 package.

Referring individual Component from individual package

```scss
@import "ej2-buttons/button/<theme_name>.scss";
```

## Common Variables

The below list of common variables used in the Essential JS 2 themes for all components. You can change these variables to customize the corresponding theme.

### Google's Material

| Name | Value |
| ------------- | ------------- |
| `$accent` | ![#e3165b](https://ej2.syncfusion.com/download/documentation/svg/e3165b.svg) `#e3165b` |
| `$accent-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$primary` | ![#3f51b5](https://ej2.syncfusion.com/download/documentation/svg/3f51b5.svg) `#3f51b5` |
| `$primary-50` | ![#e8eaf6](https://ej2.syncfusion.com/download/documentation/svg/e8eaf6.svg) `#e8eaf6` |
| `$primary-100` | ![#c5cae9](https://ej2.syncfusion.com/download/documentation/svg/c5cae9.svg) `#c5cae9` |
| `$primary-200` | ![#9fa8da](https://ej2.syncfusion.com/download/documentation/svg/9fa8da.svg) `#9fa8da` |
| `$primary-300` | ![#7986cb](https://ej2.syncfusion.com/download/documentation/svg/7986cb.svg) `#7986cb` |
| `$primary-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$primary-50-font` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$primary-100-font` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$primary-200-font` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$primary-300-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$grey-white` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$grey-black` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$grey-50` | ![#fafafa](https://ej2.syncfusion.com/download/documentation/svg/fafafa.svg) `#fafafa` |
| `$grey-100` | ![#f5f5f5](https://ej2.syncfusion.com/download/documentation/svg/f5f5f5.svg) `#f5f5f5` |
| `$grey-200` | ![#eeeeee](https://ej2.syncfusion.com/download/documentation/svg/eeeeee.svg) `#eeeeee` |
| `$grey-300` | ![#e0e0e0](https://ej2.syncfusion.com/download/documentation/svg/e0e0e0.svg) `#e0e0e0` |
| `$grey-400` | ![#bdbdbd](https://ej2.syncfusion.com/download/documentation/svg/bdbdbd.svg) `#bdbdbd` |
| `$grey-500` | ![#9e9e9e](https://ej2.syncfusion.com/download/documentation/svg/9e9e9e.svg) `#9e9e9e` |
| `$grey-600` | ![#757575](https://ej2.syncfusion.com/download/documentation/svg/757575.svg) `#757575` |
| `$grey-700` | ![#616161](https://ej2.syncfusion.com/download/documentation/svg/616161.svg) `#616161` |
| `$grey-800` | ![#424242](https://ej2.syncfusion.com/download/documentation/svg/424242.svg) `#424242` |
| `$grey-900` | ![#212121](https://ej2.syncfusion.com/download/documentation/svg/212121.svg) `#212121` |
| `$grey-dark` | ![#303030](https://ej2.syncfusion.com/download/documentation/svg/303030.svg) `#303030` |
| `$grey-light-font` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$grey-dark-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$base-font` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$error-font` | ![#f44336](https://ej2.syncfusion.com/download/documentation/svg/f44336.svg) `#f44336` |

### Microsoft Office’s Fabric

| Name | Value |
| ------------- | ------------- |
| `$theme-primary` | ![#0078d7](https://ej2.syncfusion.com/download/documentation/svg/f44336.svg) `#0078d7` |
| `$theme-dark-alt` | ![#006fc7](https://ej2.syncfusion.com/download/documentation/svg/006fc7.svg) `darken($theme-primary, 3%)` |
| `$theme-dark` | ![#005ba3](https://ej2.syncfusion.com/download/documentation/svg/005ba3.svg) `darken($theme-primary, 10%)` |
| `$theme-darker` | ![#00457a](https://ej2.syncfusion.com/download/documentation/svg/00457a.svg) `darken($theme-primary, 18%)` |
| `$theme-secondary` | ![#0081e5](https://ej2.syncfusion.com/download/documentation/svg/0081e5.svg) `lighten($theme-primary, 3%)` |
| `$theme-tertiary` | ![#42acff](https://ej2.syncfusion.com/download/documentation/svg/42acff.svg) `lighten($theme-primary, 21%)` |
| `$theme-light` | ![#b7e0ff](https://ej2.syncfusion.com/download/documentation/svg/b7e0ff.svg) `lighten($theme-primary, 44%)` |
| `$theme-lighter` | ![#d1ebff](https://ej2.syncfusion.com/download/documentation/svg/d1ebff.svg) `lighten($theme-primary, 49%)` |
| `$theme-lighter-alt` | ![#aliceblue](https://ej2.syncfusion.com/download/documentation/svg/aliceblue.svg) `lighten($theme-primary, 55%)` |
| `$neutral-white` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$neutral-lighter-alt` | ![#f8f8f8](https://ej2.syncfusion.com/download/documentation/svg/f8f8f8.svg) `#f8f8f8` |
| `$neutral-lighter` | ![#f4f4f4](https://ej2.syncfusion.com/download/documentation/svg/f4f4f4.svg) `#f4f4f4` |
| `$neutral-light` | ![#eaeaea](https://ej2.syncfusion.com/download/documentation/svg/eaeaea.svg) `#eaeaea` |
| `$neutral-quintenaryalt` | ![#dadada](https://ej2.syncfusion.com/download/documentation/svg/dadada.svg) `#dadada` |
| `$neutral-quintenary` | ![#d0d0d0](https://ej2.syncfusion.com/download/documentation/svg/d0d0d0.svg) `#d0d0d0` |
| `$neutral-tertiary-alt` | ![#c8c8c8](https://ej2.syncfusion.com/download/documentation/svg/c8c8c8.svg) `#c8c8c8` |
| `$neutral-tertiary` | ![#a6a6a6](https://ej2.syncfusion.com/download/documentation/svg/a6a6a6.svg) `#a6a6a6` |
| `$neutral-secondary-alt` | ![#767676](https://ej2.syncfusion.com/download/documentation/svg/767676.svg) `#767676` |
| `$neutral-secondary` | ![#666666](https://ej2.syncfusion.com/download/documentation/svg/666666.svg) `#666666` |
| `$neutral-primary` | ![#333333](https://ej2.syncfusion.com/download/documentation/svg/333333.svg) `#333333` |
| `$neutral-dark` | ![#212121](https://ej2.syncfusion.com/download/documentation/svg/212121.svg) `#212121` |
| `$neutral-black` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$alert-bg` | ![#deecf9](https://ej2.syncfusion.com/download/documentation/svg/deecf9.svg) `#deecf9` |
| `$error-bg` | ![#fde7e9](https://ej2.syncfusion.com/download/documentation/svg/fde7e9.svg) `#fde7e9` |
| `$success-bg` | ![#dff6dd](https://ej2.syncfusion.com/download/documentation/svg/dff6dd.svg) `#dff6dd` |
| `$theme-dark-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$theme-primary-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$theme-light-font` | ![#333333](https://ej2.syncfusion.com/download/documentation/svg/333333.svg) `#333333` |
| `$neutral-light-font` | ![#333333](https://ej2.syncfusion.com/download/documentation/svg/333333.svg) `#333333` |
| `$neutral-light-fontalt` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$grey-dark-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$base-font` | ![#333333](https://ej2.syncfusion.com/download/documentation/svg/333333.svg) `#333333` |
| `$message-font` | ![#333333](https://ej2.syncfusion.com/download/documentation/svg/333333.svg) `#333333` |
| `$alert-font` | ![#d83b01](https://ej2.syncfusion.com/download/documentation/svg/d83b01.svg) `#d83b01` |
| `$error-font` | ![#a80000](https://ej2.syncfusion.com/download/documentation/svg/a80000.svg) `#a80000` |
| `$success-font` | ![#107c10](https://ej2.syncfusion.com/download/documentation/svg/107c10.svg) `#107c10` |

### Bootstrap

| Name | Value |
| ------------- | ------------- |
| `$brand-primary` | ![#317ab9](https://ej2.syncfusion.com/download/documentation/svg/317ab9.svg) `#317ab9` |
| `$brand-primary-darken-10` | ![#3071a9](https://ej2.syncfusion.com/download/documentation/svg/3071a9.svg) `#3071a9` |
| `$brand-primary-darken-15` | ![#2a6496](https://ej2.syncfusion.com/download/documentation/svg/2a6496.svg) `#2a6496` |
| `$brand-primary-darken-25` | ![#1f496e](https://ej2.syncfusion.com/download/documentation/svg/1f496e.svg) `#1f496e` |
| `$brand-primary-darken-35` | ![#142f46](https://ej2.syncfusion.com/download/documentation/svg/142f46.svg) `#142f46` |
| `$brand-primary-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$grey-base` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$grey-darker` | ![#222222](https://ej2.syncfusion.com/download/documentation/svg/222222.svg) `#222222` |
| `$grey-dark` | ![#333333](https://ej2.syncfusion.com/download/documentation/svg/333333.svg) `#333333` |
| `$grey` | ![#555555](https://ej2.syncfusion.com/download/documentation/svg/555555.svg) `#555555` |
| `$grey-light` | ![#777777](https://ej2.syncfusion.com/download/documentation/svg/777777.svg) `#777777` |
| `$grey-44` | ![#444444](https://ej2.syncfusion.com/download/documentation/svg/444444.svg) `#444444` |
| `$grey-88` | ![#888888](https://ej2.syncfusion.com/download/documentation/svg/888888.svg) `#888888` |
| `$grey-99` | ![#999999](https://ej2.syncfusion.com/download/documentation/svg/999999.svg) `#999999` |
| `$grey-8c` | ![#8c8c8c](https://ej2.syncfusion.com/download/documentation/svg/8c8c8c.svg) `#8c8c8c` |
| `$grey-ad` | ![#adadad](https://ej2.syncfusion.com/download/documentation/svg/adadad.svg) `#adadad` |
| `$grey-dark-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$grey-white` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$grey-lighter` | ![#eeeeee](https://ej2.syncfusion.com/download/documentation/svg/eeeeee.svg) `#eeeeee` |
| `$grey-f9` | ![#f9f9f9](https://ej2.syncfusion.com/download/documentation/svg/f9f9f9.svg) `#f9f9f9` |
| `$grey-f8` | ![#f8f8f8](https://ej2.syncfusion.com/download/documentation/svg/f8f8f8.svg) `#f8f8f8` |
| `$grey-f5` | ![#f5f5f5](https://ej2.syncfusion.com/download/documentation/svg/f5f5f5.svg) `#f5f5f5` |
| `$grey-e6` | ![#e6e6e6](https://ej2.syncfusion.com/download/documentation/svg/e6e6e6.svg) `#e6e6e6` |
| `$grey-dd` | ![#dddddd](https://ej2.syncfusion.com/download/documentation/svg/dddddd.svg) `#dddddd` |
| `$grey-d4` | ![#d4d4d4](https://ej2.syncfusion.com/download/documentation/svg/d4d4d4.svg) `#d4d4d4` |
| `$grey-cc` | ![#cccccc](https://ej2.syncfusion.com/download/documentation/svg/cccccc.svg) `#cccccc` |
| `$grey-light-font` | ![#333333](https://ej2.syncfusion.com/download/documentation/svg/333333.svg) `#333333` |
| `$brand-success` | ![#5cb85c](https://ej2.syncfusion.com/download/documentation/svg/5cb85c.svg) `#5cb85c` |
| `$brand-success-dark` | ![#3c763d](https://ej2.syncfusion.com/download/documentation/svg/3c763d.svg) `#3c763d` |
| `$brand-info` | ![#5bc0de](https://ej2.syncfusion.com/download/documentation/svg/5bc0de.svg) `#5bc0de` |
| `$brand-info-dark` | ![#31708f](https://ej2.syncfusion.com/download/documentation/svg/31708f.svg) `#31708f` |
| `$brand-warning` | ![#f0ad4e](https://ej2.syncfusion.com/download/documentation/svg/f0ad4e.svg) `#f0ad4e` |
| `$brand-warning-dark` | ![#8a6d3b](https://ej2.syncfusion.com/download/documentation/svg/8a6d3b.svg) `#8a6d3b` |
| `$brand-danger` | ![#d9534f](https://ej2.syncfusion.com/download/documentation/svg/d9534f.svg) `#d9534f` |
| `$brand-danger-dark` | ![#a94442](https://ej2.syncfusion.com/download/documentation/svg/a94442.svg) `#a94442` |
| `$brand-success-light` | ![#dff0d8](https://ej2.syncfusion.com/download/documentation/svg/dff0d8.svg) `#dff0d8` |
| `$brand-info-light` | ![#d9edf7](https://ej2.syncfusion.com/download/documentation/svg/d9edf7.svg) `#d9edf7` |
| `$brand-warning-light` | ![#fcf8e3](https://ej2.syncfusion.com/download/documentation/svg/fcf8e3.svg) `#fcf8e3` |
| `$brand-danger-light` | ![#f2dede](https://ej2.syncfusion.com/download/documentation/svg/f2dede.svg) `#f2dede` |
| `$input-border-focus` | ![#66afe9](https://ej2.syncfusion.com/download/documentation/svg/66afe9.svg) `#66afe9` |
| `$brand-success-font` | ![#3c763d](https://ej2.syncfusion.com/download/documentation/svg/3c763d.svg) `#3c763d` |
| `$brand-info-font` | ![#31708f](https://ej2.syncfusion.com/download/documentation/svg/31708f.svg) `#31708f` |
| `$brand-warning-font` | ![#8a6d3b](https://ej2.syncfusion.com/download/documentation/svg/8a6d3b.svg) `#8a6d3b` |
| `$brand-danger-font` |![#a94442](https://ej2.syncfusion.com/download/documentation/svg/a94442.svg) `#a94442` |
| `$base-font` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |

### High Contrast

| Name | Value |
| ------------- | ------------- |
| `$selection-bg` | ![#ffd939](https://ej2.syncfusion.com/download/documentation/svg/ffd939.svg) `#ffd939` |
| `$selection-font` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$selection-border` | ![#ffd939](https://ej2.syncfusion.com/download/documentation/svg/ffd939.svg) `#ffd939` |
| `$hover-bg` | ![#685708](https://ej2.syncfusion.com/download/documentation/svg/685708.svg) `#685708` |
| `$hover-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$hover-border` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$border-default` | ![#969696](https://ej2.syncfusion.com/download/documentation/svg/969696.svg) `#969696` |
| `$border-alt` | ![#757575](https://ej2.syncfusion.com/download/documentation/svg/757575.svg) `#757575` |
| `$border-fg` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$border-fg-alt` | ![#ffd939](https://ej2.syncfusion.com/download/documentation/svg/ffd939.svg) `#ffd939` |
| `$bg-base-0` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$bg-base-5` | ![#0d0d0d](https://ej2.syncfusion.com/download/documentation/svg/0d0d0d.svg) `#0d0d0d` |
| `$bg-base-10` | ![#1a1a1a](https://ej2.syncfusion.com/download/documentation/svg/1a1a1a.svg) `#1a1a1a` |
| `$bg-base-15` | ![#262626](https://ej2.syncfusion.com/download/documentation/svg/262626.svg) `#262626` |
| `$bg-base-20` | ![#333333](https://ej2.syncfusion.com/download/documentation/svg/333333.svg) `#333333` |
| `$bg-base-75` | ![#bfbfbf](https://ej2.syncfusion.com/download/documentation/svg/bfbfbf.svg) `#bfbfbf` |
| `$bg-base-100` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$header-font` | ![#ffd939](https://ej2.syncfusion.com/download/documentation/svg/ffd939.svg) `#ffd939` |
| `$header-font-alt` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$content-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$content-font-alt` | ![#969696](https://ej2.syncfusion.com/download/documentation/svg/969696.svg) `#969696` |
| `$link` | ![#8a8aff](https://ej2.syncfusion.com/download/documentation/svg/8a8aff.svg) `#8a8aff` |
| `$invert-font` | ![#000000](https://ej2.syncfusion.com/download/documentation/svg/000000.svg) `#000000` |
| `$success-bg` | ![#166600](https://ej2.syncfusion.com/download/documentation/svg/166600.svg) `#166600` |
| `$error-bg` | ![#b30900](https://ej2.syncfusion.com/download/documentation/svg/b30900.svg) `#b30900` |
| `$message-font` | ![#ffffff](https://ej2.syncfusion.com/download/documentation/svg/ffffff.svg) `#ffffff` |
| `$alert-bg` | ![#944000](https://ej2.syncfusion.com/download/documentation/svg/944000.svg) `#944000` |
| `$info-bg` | ![#0056b3](https://ej2.syncfusion.com/download/documentation/svg/0056b3.svg) `#0056b3` |
| `$success-alt` | ![#2bc700](https://ej2.syncfusion.com/download/documentation/svg/2bc700.svg) `#2bc700` |
| `$error-alt` | ![#ff6161](https://ej2.syncfusion.com/download/documentation/svg/ff6161.svg) `#ff6161` |
| `$alert-alt` | ![#ff7d1a](https://ej2.syncfusion.com/download/documentation/svg/ff7d1a.svg) `#ff7d1a` |
| `$info-alt` | ![#66b0ff](https://ej2.syncfusion.com/download/documentation/svg/66b0ff.svg) `#66b0ff` |
| `$disable` | ![#757575](https://ej2.syncfusion.com/download/documentation/svg/757575.svg) `#757575` |