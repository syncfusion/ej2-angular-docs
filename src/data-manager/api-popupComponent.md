# PopupComponent

## Properties

### collision `CollisionAxis`

Specifies the collision handler settings of the component.

Defaults to *{ X: 'none',Y: 'none' }*

### content `string` &#124;  `HTMLElement`

Specifies the content of the popup element, it can be string or HTMLElement.

Defaults to *null*

### enablePersistence `boolean`

Enable or disable persisting component's state between page reloads.

### enableRtl `boolean`

specifies the rtl direction state of the popup element.

Defaults to *false*

### height `string` &#124;  `number`

Specifies the height of the popup element.

Defaults to *'auto'*

### locale `string`

Overrides the global culture and localization value for this component.

### offsetX `number`

specifies the popup element offset-x value, respective to the relative element.

Defaults to *0*

### offsetY `number`

specifies the popup element offset-y value, respective to the relative element.

Defaults to *0*

### position `PositionData`

Specifies the popup element position, respective to the relative element.

Defaults to *{X:"left", Y:"top"}*

### relateTo `HTMLElement` &#124;  `string`

Specifies the relative container element of the popup element.Based on the relative element, popup element will be positioned.

Defaults to *'body'*

### targetType `TargetType`

Specifies the relative element type of the component.

Defaults to *'container'*

### viewPortElement `HTMLElement`

Specifies the collision detectable container element of the component.

Defaults to *null*

### width `string` &#124;  `number`

Specifies the height of the popup element.

Defaults to *'auto'*

### zIndex `number`

specifies the z-index value of the popup element.

Defaults to *1000*

## Methods

### destroy

To destroy the control.

*Returns void*

### getScrollableParent

Gets scrollable parent elements for the given element.

| Parameter | Type | Description |
|------|------|-------------|
| element |  `HTMLElement` | Specify the element to get the scrollable parents of it.<br> |

*Returns void*

### hide

Hides the popup element from screen.

*Returns void*

### show

Shows the popup element from screen.

*Returns void*

## Events

### close  `EmitType<Object>`

Trigger the event once closed the popup.

### open  `EmitType<Object>`

Triggers the event once opened the popup.
