# Change animation settings

To change the animation of the ContextMenu,
[`animationSettings`](https://ej2.syncfusion.com/angular/documentation/api/context-menu/menuAnimationSettingsModel/) property is used.
The supported effects for ContextMenu are,

| Effect | Functionality |
| ------------ | ----------------------- |
| None | Specifies the sub menu transform with no animation effect. |
| SlideDown | Specifies the sub menu transform with slide down effect. |
| ZoomIn | Specifies the sub menu transform with zoom in effect. |
| FadeIn | Specifies the sub menu transform with fade in effect. |

The following sample illustrates how to open ContextMenu with `FadeIn` effect with the `duration` of `800ms`.

{% tab template= "context-menu/template", sourceFiles="app/**/*.ts", isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';
import { MenuItemModel } from '@syncfusion/ej2-navigations';

@Component({
  selector: 'app-root',
  template: `<!--target element-->
            <div id="target">Right click / Touch hold to open the ContextMenu</div>
            <!-- To Render ContextMenu. -->
            <ejs-contextmenu id='contextmenu' #contextmenu target='#target' [items]='menuItems' [animationSettings]='animation'></ejs-contextmenu>`
})

export class AppComponent {
    public animation = {
        effect: 'FadeIn',
        duration: 800
    };
    public menuItems: MenuItemModel[] = [
        {
            text: 'Show All Bookmarks'
        },
        {
            text: 'Bookmarks Toolbar',
            items: [
                {
                    text: 'Most Visited',
                    items:[
                        {
                            text: 'Gmail'
                        },
                        {
                            text: 'Google'
                        }
                    ]
                },
                {
                    text: 'Recently Added'
                }
            ]
        }];

}
```

{% endtab %}
