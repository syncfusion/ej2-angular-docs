---
title: " Bullet Chart Data Labels | Angular"

component: "Bullet Chart"

description: "Bullet Chart can be rendered by using different types of data source. They are called local data, remote data. "
---
<!-- markdownlint-disable MD036 -->

# Data Label

Data label can be added to a bullet-chart feature bars by enabling the `enable` option in the dataLabel. By default,the labels will arrange smartly without overlapping.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart id='localData' valueField='completedStories' targetField='requiredStories'
category='name' height='400px' [minimum]='minimum' [maximum]='maximum' [interval]='interval'
title='Sprint Planning' titlePosition='Top' [dataSource]='data' [animation]='animation' [dataLabel]='dataLabel'>
<e-bullet-range-collection>
    <e-bullet-range end='25' color='#ebebeb'></e-bullet-range>
    <e-bullet-range end='37' color='#d8d8d8'></e-bullet-range>
    <e-bullet-range end='45' color='#7f7f7f'></e-bullet-range>
</e-bullet-range-collection>
</ejs-bulletchart>`
})
export class AppComponent {
    public minimum: number = 5;
    public maximum: number = 45;
    public interval: number = 5;
    public animation: AnimationModel = { enable: false };
    public dataLabel: Object = { enable: true };
    public data: Object[] = [
        {
            requiredStories: 20,
            completedStories: 25,
            name: 'David'
        },
        {
            requiredStories: 25,
            completedStories: 20,
            name: 'Asif'
        },
        {
            requiredStories: 15,
            completedStories: 10,
            name: 'Thomas'
        },
        {
            requiredStories: 40,
            completedStories: 39,
            name: 'Rohit'
        },
        {
            requiredStories: 35,
            completedStories: 40,
            name: 'Virat'
        },
        {
            requiredStories: 28,
            completedStories: 25,
            name: 'Jude'
        },
        {
            requiredStories: 10,
            completedStories: 18,
            name: 'Warner'
        },
        {
            requiredStories: 30,
            completedStories: 28,
            name: 'Malik'
        }
    ];
}
```

{% endtab %}

## Customization

By using `labelStyle` property in data label, you can customize the `color`, `size` and `font`.

{% tab template="bullet-chart/getting-started/range", sourceFiles="app/**/*.ts" %}

```typescript

import { Component } from '@angular/core';
import { AnimationModel } from '@syncfusion/ej2-charts';

@Component({
    selector: 'app-container',
    template: `<ejs-bulletchart id='localData' valueField='completedStories' targetField='requiredStories'
category='name' height='400px' [minimum]='minimum' [maximum]='maximum' [interval]='interval'
title='Sprint Planning' titlePosition='Top' [dataSource]='data' [animation]='animation' [dataLabel]='dataLabel'>
<e-bullet-range-collection>
    <e-bullet-range end='25' color='#ebebeb'></e-bullet-range>
    <e-bullet-range end='37' color='#d8d8d8'></e-bullet-range>
    <e-bullet-range end='45' color='#7f7f7f'></e-bullet-range>
</e-bullet-range-collection>
</ejs-bulletchart>`
})
export class AppComponent {
    public minimum: number = 5;
    public maximum: number = 45;
    public interval: number = 5;
    public animation: AnimationModel = { enable: false };
    public dataLabel: Object = { enable: true, labelStyle:{ color: 'yellow', size: '20'} };
    public data: Object[] = [
        {
            requiredStories: 20,
            completedStories: 25,
            name: 'David'
        },
        {
            requiredStories: 25,
            completedStories: 20,
            name: 'Asif'
        },
        {
            requiredStories: 15,
            completedStories: 10,
            name: 'Thomas'
        },
        {
            requiredStories: 40,
            completedStories: 39,
            name: 'Rohit'
        },
        {
            requiredStories: 35,
            completedStories: 40,
            name: 'Virat'
        },
        {
            requiredStories: 28,
            completedStories: 25,
            name: 'Jude'
        },
        {
            requiredStories: 10,
            completedStories: 18,
            name: 'Warner'
        },
        {
            requiredStories: 30,
            completedStories: 28,
            name: 'Malik'
        }
    ];
}
```

{% endtab %}