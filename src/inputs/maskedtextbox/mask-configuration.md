---
title: "Mask Configuration"
component: "MaskedTextBox"
description: "This section explains about different standard mask formats. You can also configure a masked text box with the custom characters or regular expression to define a custom behavior."
---

# Mask Configuration

The mask is a combination of standard and custom mask elements that validates the user input based on its behavior.

> When the mask value is empty, the MaskedTextBox behaves as an input element with text type.

## Standard mask elements

The following table shows the list of mask elements and its behavior based on
[MSDN](https://msdn.microsoft.com/en-us/library/system.windows.forms.maskedtextbox.mask.aspx) standard.

The mask can be formed by combining any one or more of these mask elements.

| Mask Element | Description |
| ------------- | ------------- |
| 0 | Digit required. This element will accept any single digit from **0** to **9**. |
| 9 | Digit or space, optional. |
| # | Digit or space, optional, Plus(**+**) and minus(**-**) signs are allowed. |
| L | Letter required. It will accept letters **a-z** and **A-Z**. |
| ? | Letter or space, optional. |
| & | Requires a character. |
| C | Character or space, optional. |
| A | Alphanumeric **(A-Za-z0-9)** required.|
| a | Alphanumeric **(A-Za-z0-9)** or space, optional. |
| < | Shift down. Converts all characters to lower case. |
| > | Shift up. Converts all characters to upper case. |
| &#124; | Disable a previous shift up or shift down. |
| \\\\ | Escapes a mask character, turning it into a literal. |
| All other characters | Literals. All non-mask elements (literals) will appear as themselves within MaskedTextBox. |

The following example demonstrates the usage of standard mask elements.

{% tab template="maskedtextbox/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // sets different types of standard masks to the MaskedTextBox component
    template: `
             <div class='wrap'>
                 <ejs-maskedtextbox mask='#####' placeholder='Mask ##### (ex: 012+-)' floatLabelType= 'Always'></ejs-maskedtextbox>
             </div>
             <div class='wrap'>
                 <ejs-maskedtextbox mask='LLLLLL' placeholder='Mask LLLLLL (ex: Sample)' floatLabelType= 'Always'></ejs-maskedtextbox>
             </div>
             <div class='wrap'>
                 <ejs-maskedtextbox mask='&&&&&' placeholder='Mask &&&&& (ex: A12@#)' floatLabelType= 'Always'></ejs-maskedtextbox>
             </div>
             <div class='wrap'>
                 <ejs-maskedtextbox mask='>LLL<LLL' placeholder='Mask >LLL<LL (ex: SAMple)' floatLabelType= 'Always'></ejs-maskedtextbox>
             </div>
             <div class='wrap'>
                 <ejs-maskedtextbox mask='\\A999' placeholder='Mask \\A999 (ex: A321)' floatLabelType= 'Always'></ejs-maskedtextbox>
             </div>`
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}

## Custom mask elements

Other than the above standard mask elements, the mask can be configured with the custom characters or regular expression to define a custom behavior.

### Custom characters

You can define any of the non-mask element as the mask element
and its behavior through the [`customCharacters`](../api/maskedtextbox#customcharacters) property.

In the following example, non-mask element `P` accepts the values `P, A, p, a` and `M` accepts the values `M, m`
as mentioned in the custom characters collection.

{% tab template="maskedtextbox/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // sets mask format to the MaskedTextBox
    template: `
            <ejs-maskedtextbox [customCharacters]="customMaskChar" mask='00:00 >PM' placeholder='Time (ex: 10:00 PM, 10:00 AM)' floatLabelType= 'Always'></ejs-maskedtextbox>
            `
})
export class AppComponent {
    // sets custom characters collection for non-mask elements 'P' and 'M'
    public customMaskChar: Object = { P: 'P,A,p,a', M: 'M,m'};
    constructor() {
    }
}
```

{% endtab %}

### Regular expression

Instead of the mask element, you can define your own regular expression to validate the input of a particular input place.
The regular expressions should be wrapped by the square brackets (e.g., [`Regex`]).

In the following example, regular expression has been set for each input places.

{% tab template="maskedtextbox/regularExpression", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // sets set of regular expression for each input place as mask
    template: `
            <ejs-maskedtextbox name="mask_value" #mask="" mask='[0-2][0-9][0-9].[0-2][0-9][0-9].[0-2][0-9][0-9].[0-2][0-9][0-9]' placeholder='IP Address (ex: 212.212.111.222)' floatLabelType= 'Always'></ejs-maskedtextbox>
            `
})
export class AppComponent {
     constructor() {
    }
}

```

{% endtab %}

## Prompt character

The Prompt character is a prompting symbol in the MaskedTextBox for the mask elements. The symbol is used to show the
input positions in the MaskedTextBox.
You can customize the prompt character of MaskedTextBox by using the [`promptChar`](../api/maskedtextbox#promptchar) property.

The following example demonstrates the MaskedTextBox with customized prompt character as `*`.

{% tab template="maskedtextbox/getting-started", sourceFiles="app/**/*.ts,index.html,index.css"  %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-root',
    // sets the prompting symbol to the MaskedTextBox
    // sets mask format to the MaskedTextBox
    template: `
            <ejs-maskedtextbox promptChar="#" mask='999-999-9999'></ejs-maskedtextbox>
            `
})
export class AppComponent {
    constructor() {
    }
}
```

{% endtab %}