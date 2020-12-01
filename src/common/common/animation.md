# Animation

The **Animation** library is used to perform animation effects on HTML elements by running sequence of frames.

## Animate HTML Element

The [`animate`](https://ej2.syncfusion.com/documentation/api/base/animation#animate) method of `Animation` library
can be used to animate the HTML elements. This method can also take additional
[`AnimationModel`](https://ej2.syncfusion.com/documentation/api/base/animationModel). Refer the following code snippet
to animate a multiple DOM element.

{% tab template="common/animation-multiple", sourceFiles="app/**/*.ts,index.html" %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { Animation } from '@syncfusion/ej2-base';

@Component({
  selector: 'app-root',
  template: `
    <div #element1 class='animation1'></div>
    <div #element2 class='animation2'></div>
    `
})

export class AppComponent {
  @ViewChild('element1',{static: false})element1: any;
  @ViewChild('element2',{static: false})element2: any;

  ngAfterViewInit() {
    let animation: Animation = new Animation({ name: 'FadeIn', duration: 5000 });
    animation.animate(this.element1.nativeElement, { name: 'FadeOut' });
    animation.animate(this.element2.nativeElement, { name: 'ZoomOut' });
  }
}
```

{% endtab %}