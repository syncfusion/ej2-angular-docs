---
title: "Set the nested accordion"
component: "Accordion"
description: "This example demonstrates how to create an Essential JS 2 Accordion control inside another Essential JS 2 Accordion control."
---

# Set the nested Accordion

You can render Accordion components inside the parent Accordion content using Angular **ng-template**. Through this, we can add content as Accordion components directly with all their functionalities to our Accordion. We need to use `ng-template` inside the each `e-accordionitem` tag with `#content` attribute, which is mandatory to render content. And now use `ng-template` tag with select attribute of id or class name for mapping required content.

{% tab template="accordion/accordion", sourceFiles="app/**/*.ts"   %}

```typescript
import { Component, ViewChild } from '@angular/core';
import { AccordionComponent } from '@syncfusion/ej2-angular-navigations';
import { ExpandEventArgs, Accordion, AccordionClickArgs} from '@syncfusion/ej2-navigations';

@Component({
    selector: 'app-container',
    template: `
      <ejs-accordion>
        <e-accordionitems>
          <e-accordionitem expanded="true">
            <ng-template #header>
              <div>Video</div>
            </ng-template>
            <ng-template #content>
              <ejs-accordion>
                <e-accordionitems>
                  <e-accordionitem>
                    <ng-template #header>
                      <div>Video Track 1</div>
                    </ng-template>
                  </e-accordionitem>
                  <e-accordionitem>
                    <ng-template #header>
                      <div>Video Track 2</div>
                    </ng-template>
                  </e-accordionitem>
                </e-accordionitems>
              </ejs-accordion>
            </ng-template>
          </e-accordionitem>
          <e-accordionitem>
            <ng-template #header>
              <div>Music</div>
            </ng-template>
            <ng-template #content>
              <ejs-accordion>
                <e-accordionitems>
                  <e-accordionitem>
                    <ng-template #header>
                      <div>Music Track 1</div>
                    </ng-template>
                  </e-accordionitem>
                  <e-accordionitem>
                    <ng-template #header>
                      <div>Music Track 2</div>
                    </ng-template>
                  </e-accordionitem>
                  <e-accordionitem>
                    <ng-template #header>
                      <div>Music New</div>
                    </ng-template>
                    <ng-template #content>
                      <ejs-accordion>
                        <e-accordionitems>
                          <e-accordionitem>
                            <ng-template #header>
                              <div>New Track 1</div>
                            </ng-template>
                          </e-accordionitem>
                          <e-accordionitem>
                            <ng-template #header>
                              <div>New Track 2</div>
                            </ng-template>
                          </e-accordionitem>
                        </e-accordionitems>
                      </ejs-accordion>
                    </ng-template>
                  </e-accordionitem>
                </e-accordionitems>
              </ejs-accordion>
            </ng-template>
          </e-accordionitem>
          <e-accordionitem>
            <ng-template #header>
              <div>Images</div>
            </ng-template>
            <ng-template #content>
              <ejs-accordion>
                <e-accordionitems>
                  <e-accordionitem>
                    <ng-template #header>
                      <div>Track 1</div>
                    </ng-template>
                  </e-accordionitem>
                  <e-accordionitem>
                    <ng-template #header>
                      <div>Track 2</div>
                    </ng-template>
                  </e-accordionitem>
                </e-accordionitems>
              </ejs-accordion>
            </ng-template>
          </e-accordionitem>
        </e-accordionitems>
      </ejs-accordion>
      `
})

export class AppComponent {
}
```

{% endtab %}