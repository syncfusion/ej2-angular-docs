---
title: "Tab Adaptive"
component: "Tab"
description: "Tab control has an adaptive support to adapt the Tab control width based on devices like mobile and tablet."
---

# Responsive Modes

The following section explains about rendering Tab when its width exceeds the viewable area or particularly in a given [`width`](../api/tab#width).

The available modes are as follows:

* Scrollable
* Popup

## Scrollable

The default overflow mode is Scrollable. Scrollable display mode supports displaying the Tab header items in a single line with horizontal scrolling
enabled, when the item overflows to the available space.

* The right and left navigation arrow is added at the start and end of the Tab header through which user can
  navigate towards overflowed items of the Tab header.
* You can also see the overflowed items using touch and swipe action on the header and content section.
* By default, navigation icon in the left direction is disabled, you can see the overflowed items by moving in the right direction.
* By clicking the arrow or by holding the arrow continuously, you can see the overflowed items.

![Scrollable tab](./images/tabscroll.gif)

* In devices the navigation icons are not available. You can touch and swipe to see the overflowed items of the Tab header.

![Touch scroll](./images/touchscroll.gif)

{% tab template="tab/basic", sourceFiles="app/**/*.ts,responsivemode.html"%}

```typescript

import { Component, ViewChild } from '@angular/core';
import { TabComponent } from '@syncfusion/ej2-angular-navigations';

/**
 * Adaptive Tab Component
 */

@Component({
    selector: 'app-container',
    template: `<ejs-tab id="element" heightAdjustMode='Auto' overflowMode='Scrollable' width='300px'>
           <e-tabitems>
                        <e-tabitem [header]='headerText[0]'>
                            <ng-template #content>
                                HyperText Markup Language, commonly referred to as HTML, is the standard markup language used to create web pages. Along
                                with CSS, and JavaScript, HTML is a cornerstone technology, used by most websites to create visually engaging web
                                pages, user interfaces for web applications, and user interfaces for many mobile applications. Web browsers can read
                                HTML files and render them into visible or audible web pages. HTML describes the structure of a website semantically
                                along with cues for presentation, making it a markup language, rather than a programming language.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[1]'>
                            <ng-template #content>
                                C# is intended to be a simple, modern, general-purpose, object-oriented programming language. Its development team is led
                                by Anders Hejlsberg. The most recent version is C# 5.0, which was released on August 15, 2012.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[2]'>
                            <ng-template #content>
                                Java is a set of computer software and specifications developed by Sun Microsystems, later acquired by Oracle Corporation,
                                that provides a system for developing application software and deploying it in a cross-platform computing environment.
                                Java is used in a wide variety of computing platforms from embedded devices and mobile phones to enterprise servers
                                and supercomputers. While less common, Java applets run in secure, sandboxed environments to provide many features
                                of native applications and can be embedded in HTML pages.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[3]'>
                            <ng-template #content>
                                The command-line compiler, VBC.EXE, is installed as part of the freeware .NET Framework SDK. Mono also includes a command-line
                                VB.NET compiler. The most recent version is VB 2012, which was released on August 15, 2012.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[4]'>
                            <ng-template #content>
                                Xamarin is a San Francisco, California based software company created in May 2011[3] by the engineers that created Mono,[4]
                                Mono for Android and MonoTouch that are cross-platform implementations of the Common Language Infrastructure (CLI)
                                and Common Language Specifications (often called Microsoft .NET). With a C#-shared codebase, developers can use Xamarin
                                tools to write native Android, iOS, and Windows apps with native user interfaces and share code across multiple platforms.[5]
                                Xamarin has over 1 million developers in more than 120 countries around the World as of May 2015.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[5]'>
                            <ng-template #content>
                                ASP.NET is an open-source server-side web application framework designed for web development to produce dynamic web pages.
                                It was developed by Microsoft to allow programmers to build dynamic web sites, web applications and web services.
                                It was first released in January 2002 with version 1.0 of the .NET Framework, and is the successor to Microsoft\'\s
                                Active Server Pages (ASP) technology. ASP.NET is built on the Common Language Runtime (CLR), allowing programmers
                                to write ASP.NET code using any supported .NET language. The ASP.NET SOAP extension framework allows ASP.NET components
                                to process SOAP messages.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[6]'>
                            <ng-template #content>
                                The ASP.NET MVC is a web application framework developed by Microsoft, which implements the model–view–controller (MVC) pattern.
                                It is open-source software, apart from the ASP.NET Web Forms component which is proprietary. In the later versions
                                of ASP.NET, ASP.NET MVC, ASP.NET Web API, and ASP.NET Web Pages (a platform using only Razor pages) will merge into
                                a unified MVC 6.The project is called ASP.NET vNext.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[7]'>
                            <ng-template #content>
                                JavaScript (JS) is an interpreted computer programming language. It was originally implemented as part of web browsers so
                                that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter
                                the document content that was displayed.[5] More recently, however, it has become common in both game development
                                and the creation of desktop applications.
                            </ng-template>
                        </e-tabitem>
                    </e-tabitems>
                </ejs-tab>`
})
export class AppComponent {
    public headerText: Object = [{ text: 'HTML' }, { text: 'C Sharp(C#)' }, { text: 'Java' }, { text: 'VB.Net' },
        { text: 'Xamarin' }, { text: 'ASP.NET' }, { text: 'ASP.NET MVC' }, { text: 'JavaScript' }];

}

```

{% endtab %}

## Popup

The Popup is the another type of [`overflowMode`](../api/tab#overflowmode) in which the Tab container
holds the items that can be placed within the available space. The rest of the overflowing items for
which there is no space to fit within the viewing area are moved to overflow popup container.

* The items placed in popup can be viewed by opening the popup with the help of drop-down icon given at the end of the Tab header.

* If the popup height exceeds the height of the visible area, you can scroll through the popup items and select one.

![Tab with popup](images/popup.gif)

{% tab template="tab/basic", sourceFiles="app/**/*.ts,index.html"%}

```typescript

import { Component, ViewChild } from '@angular/core';
import { TabComponent } from '@syncfusion/ej2-angular-navigations';

/**
 * Adaptive Tab Component
 */

@Component({
    selector: 'app-container',
    template: `<ejs-tab id="element" heightAdjustMode='Auto' overflowMode='Popup' width='300px'>
            <e-tabitems>
                        <e-tabitem [header]='headerText[0]'>
                            <ng-template #content>
                                HyperText Markup Language, commonly referred to as HTML, is the standard markup language used to create web pages. Along
                                with CSS, and JavaScript, HTML is a cornerstone technology, used by most websites to create visually engaging web
                                pages, user interfaces for web applications, and user interfaces for many mobile applications. Web browsers can read
                                HTML files and render them into visible or audible web pages. HTML describes the structure of a website semantically
                                along with cues for presentation, making it a markup language, rather than a programming language.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[1]'>
                            <ng-template #content>
                                C# is intended to be a simple, modern, general-purpose, object-oriented programming language. Its development team is led
                                by Anders Hejlsberg. The most recent version is C# 5.0, which was released on August 15, 2012.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[2]'>
                            <ng-template #content>
                                Java is a set of computer software and specifications developed by Sun Microsystems, later acquired by Oracle Corporation,
                                that provides a system for developing application software and deploying it in a cross-platform computing environment.
                                Java is used in a wide variety of computing platforms from embedded devices and mobile phones to enterprise servers
                                and supercomputers. While less common, Java applets run in secure, sandboxed environments to provide many features
                                of native applications and can be embedded in HTML pages.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[3]'>
                            <ng-template #content>
                                The command-line compiler, VBC.EXE, is installed as part of the freeware .NET Framework SDK. Mono also includes a command-line
                                VB.NET compiler. The most recent version is VB 2012, which was released on August 15, 2012.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[4]'>
                            <ng-template #content>
                                Xamarin is a San Francisco, California based software company created in May 2011[3] by the engineers that created Mono,[4]
                                Mono for Android and MonoTouch that are cross-platform implementations of the Common Language Infrastructure (CLI)
                                and Common Language Specifications (often called Microsoft .NET). With a C#-shared codebase, developers can use Xamarin
                                tools to write native Android, iOS, and Windows apps with native user interfaces and share code across multiple platforms.[5]
                                Xamarin has over 1 million developers in more than 120 countries around the World as of May 2015.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[5]'>
                            <ng-template #content>
                                ASP.NET is an open-source server-side web application framework designed for web development to produce dynamic web pages.
                                It was developed by Microsoft to allow programmers to build dynamic web sites, web applications and web services.
                                It was first released in January 2002 with version 1.0 of the .NET Framework, and is the successor to Microsoft\'\s
                                Active Server Pages (ASP) technology. ASP.NET is built on the Common Language Runtime (CLR), allowing programmers
                                to write ASP.NET code using any supported .NET language. The ASP.NET SOAP extension framework allows ASP.NET components
                                to process SOAP messages.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[6]'>
                            <ng-template #content>
                                The ASP.NET MVC is a web application framework developed by Microsoft, which implements the model–view–controller (MVC) pattern.
                                It is open-source software, apart from the ASP.NET Web Forms component which is proprietary. In the later versions
                                of ASP.NET, ASP.NET MVC, ASP.NET Web API, and ASP.NET Web Pages (a platform using only Razor pages) will merge into
                                a unified MVC 6.The project is called ASP.NET vNext.
                            </ng-template>
                        </e-tabitem>
                        <e-tabitem [header]='headerText[7]'>
                            <ng-template #content>
                                JavaScript (JS) is an interpreted computer programming language. It was originally implemented as part of web browsers so
                                that client-side scripts could interact with the user, control the browser, communicate asynchronously, and alter
                                the document content that was displayed.[5] More recently, however, it has become common in both game development
                                and the creation of desktop applications.
                            </ng-template>
                        </e-tabitem>
                    </e-tabitems>
                </ejs-tab>`
})
export class AppComponent {
    public headerText: Object = [{ text: 'HTML' }, { text: 'C Sharp(C#)' }, { text: 'Java' }, { text: 'VB.Net' },
        { text: 'Xamarin' }, { text: 'ASP.NET' }, { text: 'ASP.NET MVC' }, { text: 'JavaScript' }];

}

```

{% endtab %}

## See Also

* [How to prevent content swipe selection](./how-to/prevent-content-swipe-selection/)
* [Collapsible Tab](./how-to/create-collapsible-tabs/)