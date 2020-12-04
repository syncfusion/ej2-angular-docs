---
title: "Ribbon"
component: "Spreadsheet"
description: "Learn the various operations that you can perform in ribbon of the Angular Spreadsheet."
---

# Ribbon

It helps to organize a spreadsheet’s features into a series of tabs. By clicking the expand or collapse icon, you can expand or collapse the ribbon toolbar dynamically.

## Ribbon Customization

You can customize the ribbon using the following methods,

| Method | Action |
|-------|---------|
| [`hideRibbonTabs`](../api/spreadsheet/#hideribbontabs) | Used to show or hide the existing ribbon tabs. |
| [`enableRibbonTabs`](../api/spreadsheet/#enableribbontabs) | Used to enable or disable the existing ribbon tabs. |
| [`addRibbonTabs`](../api/spreadsheet/#addribbontabs) | Used to add custom ribbon tabs. |
| [`hideToolbarItems`](../api/spreadsheet/#hidetoolbaritems) | Used to show or hide the existing ribbon toolbar items. |
| [`enableToolbarItems`](../api/spreadsheet/#enabletoolbaritems) | Used to enable or disable the specified toolbar items. |
| [`addToolbarItems`](../api/spreadsheet/#addtoolbaritems) | Used to add the custom items in ribbon toolbar. |
| [`hideFileMenuItems`](../api/spreadsheet/#hidefilemenuitems) | Used to show or hide the ribbon file menu items. |
| [`enableFileMenuItems`](../api/spreadsheet/#enablefilemenuitems) | Used to enable or disable file menu items. |
| [`addFileMenuItems`](../api/spreadsheet/#addfilemenuitems) | Used to add custom file menu items. |

The following code example shows the usage of ribbon customization.

{% tab template="spreadsheet/ribbon/cutomization", sourceFiles="app/**/*.ts", isDefaultActive=true, iframeHeight="450px" %}

```javascript
import { Component, ViewChild } from '@angular/core';
import { SpreadsheetComponent, MenuSelectEventArgs } from '@syncfusion/ej2-angular-spreadsheet';
import { select } from '@syncfusion/ej2-base';
import { ClickEventArgs } from '@syncfusion/ej2-navigations';
import { dataSource } from './datasource';

@Component({
    selector: 'app-container',
    template: `<ejs-spreadsheet #spreadsheet (created)="created()" (fileMenuBeforeOpen)="fileMenuBeforeOpen()"
                (fileMenuItemSelect)="fileMenuItemSelect($event)" [openUrl]="openUrl" [saveUrl]="saveUrl" [showFormulaBar]="false" [showSheetTabs]="false" [allowInsert]="false" [allowDelete]="false" [allowMerge]="false">
                <e-sheets>
                  <e-sheet>
                    <e-ranges>
                      <e-range [dataSource]="data"></e-range>
                    </e-ranges>
                    <e-columns>
                      <e-column [width]=180></e-column>
                      <e-column [width]=130></e-column>
                      <e-column [width]=130></e-column>
                      <e-column [width]=180></e-column>
                      <e-column [width]=130></e-column>
                      <e-column [width]=120></e-column>
                    </e-columns>
                  </e-sheet>
                </e-sheets>
              </ejs-spreadsheet>`
})
export class AppComponent {
    @ViewChild('spreadsheet')
    spreadsheetObj: SpreadsheetComponent;

    data: object[] = dataSource;
    openUrl = 'https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/open';
    saveUrl = 'https://ej2services.syncfusion.com/production/web-services/api/spreadsheet/save';

    created() {
        this.spreadsheetObj.cellFormat({ fontWeight: 'bold', textAlign: 'center' }, 'A1:F1');
        // Hiding the `Insert` from ribbon.
        this.spreadsheetObj.hideRibbonTabs(['Insert']);
        // Set disabled state to `View` ribbon tab.
        this.spreadsheetObj.enableRibbonTabs(['View'], false);
        /// Adding the `Help` ribbon tab at the last index.
        // Specify the ribbon tab header text in last optional argument(`insertBefore`) for inserting new tab before any existing tab.
        this.spreadsheetObj.addRibbonTabs([{ header: { text: 'Help' }, content: [{ text: 'Feedback', tooltipText: 'Feedback',
            click: (args: ClickEventArgs): void => { /* Any click action for this toolbar item will come here. */ } }] }]);
        // Hiding the unwanted toobar items from `Home` by specifying its index.
        this.spreadsheetObj.hideToolbarItems('Home', [0, 1, 2, 4, 14, 15, 21, 24]);
        // Set diable state to `Underline`, 'Wrap text` toobar items from `Home` by specifying the item id.
        this.spreadsheetObj.enableToolbarItems(
            'Home', [`${this.spreadsheetObj.element.id}_underline`, `${this.spreadsheetObj.element.id}_wrap`], false);
        // Set disable state to `Protect Sheet` toolbar item from `Data` by mentioning its index.
        this.spreadsheetObj.enableToolbarItems('Data', [0], false);
        // Adding the new `Custom Formulas` toolbar item under `Formulas` tab for adding custom formulas.
        this.spreadsheetObj.addToolbarItems(
            'Formulas', [{ type: 'Separator' }, {
                text: 'Custom Formulas', tooltipText: 'Custom Formulas',
                // You can set click handler for each new custom toolbar item
                click: (args: ClickEventArgs): void => {
                    // You can add custom formualas here.
                }
            }]);
        // Adding new custom item `Import` after the existing `Open` item. By default, new item will add after the specified item.
        this.spreadsheetObj.addFileMenuItems([{ text: 'Import', iconCss: 'e-open e-icons' }], 'Open');
        // Adding new custom item `Export As` after the existing `Save As` item.
        // Set `insertAfter` optional argument as `false` for adding new item before the specified item.
        this.spreadsheetObj.addFileMenuItems(
            [{
                text: 'Export As', iconCss: 'e-save e-icons', items: [{ text: 'XLSX', iconCss: 'e-xlsx e-icons' },
                    { text: 'XLS', iconCss: 'e-xls e-icons' }, { text: 'CSV', iconCss: 'e-csv e-icons' }]
            }],
            'Save As', false);
    }

    fileMenuBeforeOpen (): void {
        // Because the file menu items are created dynamically, you need to perform the hide or show and enable/disable operations
        // under filemenu before open event.
        // Hiding the `Save As` and `Open` item.
        this.spreadsheetObj.hideFileMenuItems(['Save As', 'Open']);
         // Set disable state to `New` item. You can perform any file menu items customization by specifying the item id,
        // if it has more than one same item text. Set the last argument `isUniqueId` as true for using the item id.
        this.spreadsheetObj.enableFileMenuItems([`${this.spreadsheetObj.element.id}_New`], false, true);
    }

    fileMenuItemSelect (args: MenuSelectEventArgs): void {
        // Custom file menu items select handler
        switch (args.item.text) {
            case 'Import': select(`#${this.spreadsheetObj.element.id}_fileUpload`, this.spreadsheetObj.element).click();
                break;
            case 'XLSX': this.spreadsheetObj.save({ saveType: 'Xlsx' });
                break;
            case 'XLS': this.spreadsheetObj.save({ saveType: 'Xls' });
                break;
            case 'CSV': this.spreadsheetObj.save({ saveType: 'Csv' });
                break;
      }
    }
}
```

{% endtab %}

## See Also

* [Worksheet](./worksheet)
* [Rows and columns](./rows-and-columns)
