# Color Mapping

Color mapping is used to customize each group or item colors based on specified types of color mappings.

The following options are available to customize the group and leaf items in the tree map control.

## Range color mapping

Range color mapping is used to apply color to items by giving specific ranges in the dataSource. You should specify the datasource field in the [`rangeColorValuePath`] property.

The following code example shows applying range color mapping.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;'  [dataSource]='data' weightValuePath='count' rangeColorValuePath='count'
    [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [{ fruit:'Apple', count:5000 },
                       { fruit:'Mango', count:3000 },
                       { fruit:'Orange', count:2300 },
                       { fruit:'Banana', count:500 },
                       { fruit:'Grape', count:4300 },
                       { fruit:'Papaya', count:1200 },
                       { fruit:'Melon', count:4500 }
    ];
    public leafItemSettings: object = {
         labelPath: 'fruit',
        colorMapping:[
            {
               from:500,
               to:3000,
               color:'orange'
           },
           {
               from:3000,
               to:5000,
               color:'green'
           }
        ]
    };
}

```

{% endtab %}

## Equal color mapping

Equal color mapping is used to fill colors to each item by specifying equal value present in the datasource field that can be specified in the [`equalColorValuePath`] property.

The following code example shows applying equal color mapping.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;'  [dataSource]='data' weightValuePath='count' equalColorValuePath='Brand'
    [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
        { Car:'Mustang', Brand:'Ford', count:232 },
                       { Car:'EcoSport', Brand:'Ford', count:121 },
                       { Car:'Swift', Brand:'Maruti', count:143 },
                       { Car:'Baleno', Brand:'Maruti', count:454 },
                       { Car:'Vitara Brezza', Brand:'Maruti', count:545 },
                       { Car:'A3 Cabriolet', Brand:'Audi',count:123 },
                       { car:'RS7 Sportback', Brand:'Audi', count:523 }
    ];
    public leafItemSettings: object = {
        labelPath: 'Car',
        colorMapping:[
            {
               value:'Ford',
               color:'green'
           },
           {
               value:'Audi',
               color:'red'
           },
           {
               value:'Maruti',
               color:'orange'
           }
        ]
    };
}

```

{% endtab %}

## Desaturation color mapping

Desaturation color mapping is used to apply colors with opacity to items based on the given values for the [`minOpacity`] and [`maxOpacity`] properties in the tree map control.

The following code example shows applying desaturation color mapping.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;'  [dataSource]='data' weightValuePath='count' rangeColorValuePath='count'
    [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
                      { fruit:'Apple', count:5000 },
                       { fruit:'Mango', count:3000 },
                       { fruit:'Orange', count:2300 },
                       { fruit:'Banana', count:500 },
                       { fruit:'Grape', count:4300 },
                       { fruit:'Papaya', count:1200 },
                       { fruit:'Melon', count:4500 }
    ];
    public leafItemSettings: object = {
        labelPath: 'fruit',
        colorMapping:[
            {
               from:500,
               to:3000,
               minOpacity:0.2,
               maxOpacity:0.5,
               color:'orange'
           },
           {
               from:3000,
               to:5000,
               minOpacity:0.5,
               maxOpacity:0.8,
               color:'green'
           }
        ]
        };
}

```

{% endtab %}

## Palette color mapping

Palette color mapping is used to fill the same color to each group or leaf node by given colors in the [`palette`] property in tree map control.

The following code example shows applying  palette color mapping.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;'  [dataSource]='data' weightValuePath='count' [palette]='palette'
    [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
        { Car:'Mustang', Brand:'Ford', count:232 },
                       { Car:'EcoSport', Brand:'Ford', count:121 },
                       { Car:'Swift', Brand:'Maruti', count:143 },
                       { Car:'Baleno', Brand:'Maruti', count:454 },
                       { Car:'Vitara Brezza', Brand:'Maruti', count:545 },
                       { Car:'A3 Cabriolet', Brand:'Audi',count:123 },
                       { car:'RS7 Sportback', Brand:'Audi', count:523 }
    ];
    public leafItemSettings: object = {
        labelPath: 'Car'
    };
    public palette: object= ['red','green'],
    }

```

{% endtab %}

## Desaturation with multiple colors

Multiple colors are used as gradient effect to specific shapes based on the ranges in datasource.

By using color API, you can set n number of colors.

The following code example shows how to use multiple colors.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;'  [dataSource]='data' weightValuePath='count' rangeColorValuePath='count' [leafItemSettings]='leafItemSettings' [legendSettings] ='legendSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
        { fruit:'Apple', count:5000 },
        { fruit:'Mango', count:3000 },
        { fruit:'Orange', count:2300 },
        { fruit:'Banana', count:500 },
        { fruit:'Grape', count:4300 },
        { fruit:'Papaya', count:1200 },
        { fruit:'Melon', count:4500 }
    ];
    public legendSettings:object ={
        visible:true
    }
    public leafItemSettings: object = {
        labelPath: 'fruit',
        colorMapping:[
            {
               from:500,
               to:2500,
               color:['orange','pink']
           },
           {
               from:3000,
               to:5000,
               color:['green','red','blue']
           }
        ]
    };
    }

```

{% endtab %}

## Color for items excluded from color mapping

Based on the ranges in the data source, get the excluded ranges from color mapping, and then apply specific color to the items.

The following code example shows how to set the color for items excluded from color mapping.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;'  [dataSource]='data' weightValuePath='count' rangeColorValuePath='count' [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
        { fruit:'Apple', count:5000 },
        { fruit:'Mango', count:3000 },
        { fruit:'Orange', count:2300 },
        { fruit:'Banana', count:500 },
        { fruit:'Grape', count:4300 },
        { fruit:'Papaya', count:1200 },
        { fruit:'Melon', count:4500 }
    ];
    public leafItemSettings: object = {
        labelPath: 'fruit',
         colorMapping:[
            {
               from:500,
               to:2500,
               color:'orange'
           },
           {
               from:3000,
               to:4000,
               color:'green'
           },
           {
               color:'red'
           }
        ]
    };
    }

```

{% endtab %}

## Bind the colors to the items from data source

To set color for each items in treemap, bind the field name in the data source to the `rangeColorValuePath`.

The following code example shows to set the color for treemap items.

{% tab template= "treemap/getting-started/treemap", sourceFiles="app/**/*.ts" , isDefaultActive=true %}

```typescript
import { Component } from '@angular/core';

@Component({
    selector: 'app-container',
    template: `<ejs-treemap id='container' style='display: block;'  [dataSource]='data' weightValuePath='count' colorValuePath='color' [leafItemSettings]='leafItemSettings'>
    </ejs-treemap>`
})
export class AppComponent {
    public data: object[] = [
        { fruit:'Apple', count:5000, color: 'red'},
        { fruit:'Mango', count:3000, color:'blue'},
        { fruit:'Orange', count:2300, color:'green' },
        { fruit:'Banana', count:500, color:'yellow' },
        { fruit:'Grape', count:4300, color:'orange' },
        { fruit:'Papaya', count:1200, color:'pink' },
        { fruit:'Melon', count:4500, color:'violet' }

    ];
    public leafItemSettings: object = {
        labelPath: 'fruit'
    };
    }

```

{% endtab %}
