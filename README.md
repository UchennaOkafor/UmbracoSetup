# Umbraco Wiki

## Intro
The purpose of this repository is to add information about important things to remember when setting up umbraco projects, this includes the different packages to install in order to make the most out of umbraco.
This wiki was written for **Umbraco 7.10.4**

## Getting Started

### Instllation
```
 PM> Install-Package UmbracoCms
```
or go to NuGet and search for UmbracoCms and install. 
Upon installation, unless you want to toy around and get to the grips with Umbraco, click the customize button which will let you setup connection strings for your database and also to opt out of installing with a sample website.

### Git Ignore
https://github.com/github/gitignore/blob/master/Umbraco.gitignore

### Packages
* [uSync](https://our.umbraco.org/projects/developer-tools/usync)
* [uSync Content Edition](https://our.umbraco.org/projects/developer-tools/usynccontentedition)
* [Umbraco Forms](https://our.umbraco.org/projects/developer-tools/umbraco-forms/)
* [Material Design Icon Pack](https://our.umbraco.org/projects/backoffice-extensions/material-design-icon-pack)
* [ImageGen](https://our.umbraco.org/projects/website-utilities/imagegen/)
* [Font Awesome Icon Pack and Media Icons](https://our.umbraco.org/projects/backoffice-extensions/font-awesome-icon-pack-and-media-icons/)
* [Ditto](https://our.umbraco.org/projects/developer-tools/ditto)
* [Doc Type Grid Editor](https://our.umbraco.org/projects/backoffice-extensions/doc-type-grid-editor/)

#### Doc Type Grid Editor

[Developer Guide](https://github.com/uche1/UmbracoWiki/blob/master/Doc-Type-Grid-Editor---Developers-Guide-v1.1.pdf) -  This has more detailed documentation. However, the bits that we're interested in for now is the json config settings shown below which can be found in **/config/grid.editors.config.json**
```JSON
{
    "name": "Doc Type",
    "alias": "docType",
    "view": "/App_Plugins/DocTypeGridEditor/Views/doctypegrideditor.html",
    "render": "/App_Plugins/DocTypeGridEditor/Render/DocTypeGridEditor.cshtml",
    "icon": "icon-item-arrangement",
    "config": {
        "allowedDocTypes": [],
        "nameTemplate": "",
        "enablePreview": true,
        "viewPath": "/Views/Partials/Grid/Editors/DocTypeGridEditor/",
        "previewViewPath": "/Views/Partials/Grid/Editors/DocTypeGridEditor/Previews/",
        "previewCssFilePath": "",
        "previewJsFilePath": ""
    }
}
```
Doc Type Grid Editor is a very powerful package because it allows you to render Document Types in Grid Layouts. What I like to do is, edit allowedDocTypes so that only certain document types can be rendered. You can even use a regex pattern to configure accepted templates, e.g. "Widget$" will match all doc types with an alias ending in "Widget". This is a very powerful tool.

You can just duplicate this json config and effectively creating more ways users can add components to widgets using the grid layout. The **name**, **alias**, **icon** and **allowDocTypes** are the fields that should be changed to suit your needs.


### App Settings
``` XML
  <appSettings>
    <!--
      Umbraco web.config configuration documentation can be found here:
      http://our.umbraco.org/documentation/using-umbraco/config-files/#webconfig
      -->
    <add key="umbracoReservedPaths" value="~/umbraco,~/install/,~/bundles,~/Content" />
    <add key="Umbraco.ModelsBuilder.Enable" value="true" />
    <add key="Umbraco.ModelsBuilder.ModelsMode" value="LiveAppData" />
  </appSettings>
```
Ensure Enable = true and ModelsMode =  LiveAppData. Live app data means the models are auto generated when the document types are changed in the backoffice. This is good as it helps speed up development.

https://our.umbraco.org/Documentation/reference/templating/Modelsbuilder/Builder-Modes


### Misc
```
Umbraco.TypedContent(Id).OfType<Type>();
```
