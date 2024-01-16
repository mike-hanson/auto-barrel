## NO LONGER MAINTAINED
I have retired and am no longer able to maintain this extension.  If you anyone is interested in taking over the maintainance please message me directly.  I am happy to transfer this and the source repo, and help get up an running with publishing it to the marketplace.

# Auto Barrel

Auto Barrel adds support for creating a barrel (index.[tj]s) in a folder and optionally keeping it up to date automatically.

Please note the *raison d'etre' for this extension is the **Automated** maintenance of barrel files.  While it provides two commands for creating and updating barrel files it was not intended for manual barrel management.  There are several other extensions that may provide better support for manual barrel management. 

![install and work](images/auto-barrel.gif)

## Features

Create Barrel - Right click on any folder in Explorer viewlet and this command allows you to create a new barrel with export statements for all other modules of the same language or Vue.js modules.

Auto Barrel - Start - From the command pallete execute this command to have Auto Barrel automatically add and delete export statements as files are added or deleted from the folder.

Auto Barrel - Stop - From the command pallete execute this command to stop automatic management of barrel files.

Update Barrel - Righ click on a barrel file in Exporer viewlet and this command allows you to update the barrel to include new files added manually. Perfect if you forget to start Auto Barrel before adding new files.

You can also prevent Auto Barrel from treating existing index.[tj]s files as barrels by adding a comment to the file

### Recursive Barelling

As of v1.4.0 Auto Barrel supports including files in sub folders in a barrel file. When Auto Barrel - Start is active and this feature is enabled (it is enabled by default) Auto Barrel walks up the folder tree to find the nearest ancestor index.[jt]s file to manage. This can lead to a file with the name index.\* being incorrectly identified as a barrel. If this happens the file will need to be excluded using either the setting or an appropriate comment as described below.

As of v1.5.0 Auto Barrel recognises barrel files in nested folders and imports the folder rather than individual files in the folder. However this requires recursive barrelling to be enabled.

## Extension Settings

The following settings can be configured to control the behaviour of Auto Barrel.

```javascript
'autoBarrel.defaultLanguage';
```

This defaults to TypeScript. Supported values are TypeScript or JavaScript. When Create Barrel is executed Auto Barrel attempts to determine the language extension from the contents of the folder. If all of the files in the folder have the same extension it will create a barrel file with that extension. If the file contains a mix of JavaScript and TypeScript files Create Barrel will use this setting.

```javascript
'autoBarrel.alwaysUseDefaultLanguage';
```

This defaults to false. If this is set to true then the Create Barrel command will not attempt to determine the language extension it will create a barrel file with the appropriate language specified.

```javascript
'autoBarrel.watchGlob';
```

This defaults to a glob that includes TypesScript, JavaScript, React and Vue files. When the Auto Barrel - Start command is executed from the Command Pallette this setting is used to configure a File System Watcher to monitor file creation and deletion using this setting. Since the most common convention is to put source files in a src folder below a workspace root Auto Barrel uses a default that will watch for creation or deletion of files in any folder below any src folder. If you use a different convention or want to limit the files that are watched you can change the glob.

For example to ignore .js files change it to _\*\*\/src\/\*\*\/_.ts* or to ignore .ts files change it to *\*\*\/src\/\*\*\/_.ts_

```javascript
'autoBarrel.ignoreFilePathContainingAnyOf';
```

A comma separated list of path fragments that should be ignored. This defaults to _.spec,.test_ so that test files located next to the source file are not included in barrels as is the default when using tools such as angular-cli to generate components.

The setting is used to prevent files where the full path contains any of the fragments from being added to new or existing barrel files.

```javascript
'autoBarrel.useImportAliasExportPattern';
```

This defaults to false. If this is set to true then instead of simply exporting files included in the barral like this

```javascript
export * from './auth.actions';
```

We import the file with an alias derived from the name and export the alias something like this

```javascript
import * as AuthActions from './auth.actions';

export { AuthActions };
```

The alias uses both dots and hyphens as word separators to build the alias. A file name like **login-page.actions** will result in an alias of **LoginPageActions**

```javascript
'autoBarrel.disableRecursiveBarrelling';
```

This defaults to false.

If this is set to true then files in sub folders below the barrel file will not be included when using the Create Barrel command. Also when the Auto Barrel - Start command is active only barrel files in the same folder as a new or deleted file will be affected, Auto Barrel will not walk up the folder tree looking for a barrel file.

```javascript
'autoBarrel.excludeSemiColonAtEndOfLine';
```

This defaults to false.

If enabled then semi colons will not be included at the end of statements generated in barrel files.

```javascript
'autoBarrel.includeExtensionOnExport';
```

This defaults to '.vue';

This should be a comma separated string of extensions (including the dot) that should be included on generating an export statement. When a file is processed if the extension is included in this list then the extension will be included in the file path of the export statement.

```javascript
'autoBarrel.quoteStyle';
```

This defaults to 'Single'.

If this is set to 'Double' then a double quoute will be used in generated code when building the import path for statements.

## Ignoring Potential Barrel Files

If your workspace/s contain existing index.ts or index.js files that are matched by the autoBarrel.watchGlob pattern, but they are not barrel files you can tell Auto Barrel to ignore them during automatic monitoring by adding the following comment as the first line of the file.

```javascript
// auto-barrel-ignore
```

If Auto Barrel detects a file creation in a folder containing a potential barrel file and the barrel file contains this comment as the first line it will abort processing and make no further attempt to add an export for the new file. This can also be achieved using the _ignoreFilePathContainingAnyOf_ setting introduced in v1.0.3 but this method is still valid.

## Automating Start

If you would like to have Auto Barrel start monitoring for changes when you open a workspace we recommend the excellent [Auto Run Command](https://marketplace.visualstudio.com/items?itemName=gabrielgrinberg.auto-run-command#overview) extension. With the extension installed simply add a rule something like this to User Settings

```javascript
"auto-run-command.rules": [
    ...
     {
         "condition": [
             "always"
         ]
         "command": "autoBarrel.start",
         "message": "Starting Auto Barrel..."
     }
 ]
```

**Enjoy!**

**NB: Please not this repository is only for providing support for Auto Barrel, the source code is no longer public**
