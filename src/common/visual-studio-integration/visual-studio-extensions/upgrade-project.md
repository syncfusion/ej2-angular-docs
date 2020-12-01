# Upgrade Project

The Syncfusion Angular migration is a Visual Studio add-in that allows you to migrate the existing Syncfusion Angular Application from one Essential Studio version to another version. This helps to avoid the manual work stuff in required places when migrating the Syncfusion version.

> The Syncfusion Angular Project migration are available from v17.3.0.9.

The following steps help you to upgrade the Syncfusion version in **Syncfusion Angular Application** through the **Visual Studio**:

1. Open the Angular application which uses the Syncfusion component.

2. To open Migration Wizard, follow either one of the options below:

    **Option 1:**

    Choose **Extensions-> Syncfusion-> Essential Studio for Essential Studio for ASP.NET Core ->Migrate Project…** in **Visual Studio** menu.

    ![menu](../images/migrate-menu.png)

    **Option 2:**

    Right-click on the **Application** from the **Solution Explorer** and select the **Syncfusion Essential JS 2** and choose the **Migrate the Essential JS 2  project to Another version…**

    ![Context menu](../images/migrate-context-menu.png)

3. The Syncfusion Project Migration window appears. You can choose the required Syncfusion Angular version to migrate. The Syncfusion Angular versions are loaded from published Syncfusion angular NPM packages and it requires the internet connectivity. If you want to take backup of project, select the Backup the project. Also if you want to select asset option, select Asset From value.

    ![Migration Window](../images/migration-window.PNG)

4. Once the migration process completed, will get the success message window.

    ![project backup](../images/Confirmation-window.PNG)

5. The Syncfusion Angular NPM packages, and CSS are updated to the respective version in the project.

## Upgraded changes

The Syncfusion NPM packages and Style link will be updated with the selected Syncfusion Angular version in the Syncfusion Project Migration.

## Npm packages

The installed Syncfusion Angular NPM packages are updated with the selected Syncfusion Angular version in ClientApp/package.json file.

![NPM packages](../images/npm-packages.png)

## CDN Style Link

The selected Syncfusion Angular version updated in the ClientApp/src/index.html file with cdn link.

![Style links](../images/cdnstyle-link.png)

## NPM Style Link

The selected Syncfusion Angular version updated in the ClientApp/src/index.html file from npm package.

![Style links](../images/npmstyle-link.png)
