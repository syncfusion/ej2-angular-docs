# NgModule

Syncfusion Angular has NgModule for each component with two implementation as given below.

1. Component Module
2. Component All Module

## Component Module

This module contains particular Component and all of its child properties directives
available excluding feature-wise modules. For ex., `GridModule` is only included with
`GridComponent` and `ColumnDirective`. This is always advised to use this module,
as you can control what are features of a component you are using and also it much
helpful reducing bundle size when you are using `Webpack` or `Rollup.js`

## Component All Module

This module contains particular component and all of its directives with addition of
all the feature-wise Modules of that component. For ex., `GridAllModule` is included
with `GridComponent`, `ColumnDirective`, `FilterService`, `PageService`, `GroupService`
and all other feature-wise module services it is supporting.
