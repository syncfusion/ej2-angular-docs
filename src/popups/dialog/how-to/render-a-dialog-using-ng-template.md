---
title: "Render a dialog using ng-template"
component: "Dialog"
description: "Covers customization features such as load content to the dialog from external sources, built-in alert, and confirmation model dialog."
---

# Render a Dialog using ng-template

You can provide the HTML elements as header, footer, and content of the dialog using ng-template directives. For more details, refer to the [Angular Documentation](https://angular.io/guide/structural-directives#the-ng-template).

In this [example](https://ej2.syncfusion.com/angular/demos/#/material/dialog/template), dialog header, footer, and content are rendered using ng-template directives

## How to destroy the dialog component when navigate pages using Angular routing

By default, the dialog component appends into the body element when you did not specify any target to the dialog.  When navigate pages using Angular routing, the elements inside the routing pages gets destroyed. So, the dialog elements are not destroyed properly while routing. It will cause the memory leak problem in DOM when continuously navigating the pages.

You can avoid this problem using one of the following solutions:

### Solution 1

Set the target to the dialog component to solve the destroy related issue in the DOM.  If you set the target property to dialog component, the dialog appends inside the target element that is placed on the routing partial page. It destroys both dialog component and it’s all elements when switching between the routing component page.  

Refer to this [sample](https://stackblitz.com/edit/angular-router-example-fcrp53?file=app/app.component.html).

### Solution 2

If you do not want to set the target property to dialog, use this solution.  Destroy the dialog elements using the ngOnDestroy method from your application. The ngOnDestroy method is called before the component/directive destroy by Angular.

Refer to this [sample](https://stackblitz.com/edit/angular-router-example-9yc2on?file=app/app.component.html).