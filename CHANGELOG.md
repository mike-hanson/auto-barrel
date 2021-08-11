# Change Log

All notable changes to the "auto-barrel" extension will be documented in this file.

Based on [Keep a Changelog](http://keepachangelog.com/).

## [Unreleased]

## [1.10.0] 2021-06-20

### Added
New setting to control whether double or single quotes should be used when generating code

## [1.9.1] 2021-03-17

### Added
Create Barrel and Update Barrel commands now sort file list before writing to barrel file (PR from Ben Winding)

## [1.9.0] 2021-02-15

### Added
Support for list of extensions to include in generated export statements

## [1.8.0] 2021-01-11

### Added
Support for excluding semi colons at end of generated statements through a new setting excludeSemiColonAtEndOfLine

## [1.7.1] 2019-11-19

### Fixed
Issue with initial implementation of Vue support where it included the extension

## [1.7.0] 2019-11-15

### Added
Support for including .vue files in barrels. Barrel files themselves still have either .ts or .js.

## [1.6.3] 2019-09-15

### Changed
Updated engines setting to ensure compatability with recent changes

## [1.6.2] 2019-09-10

### Fixed

An issue with new Update Barrel command where it would not update file if it was active editor with changes

## [1.6.0] 2019-09-08

### Added

New Update Barrel command to explorer context menu

## [1.5.2] 2019-06-20

### Fixed

Reverted webpack bundling changes as this caused issues after updating.

## [1.5.1] 2019-06-17

### Changed

Introduced bundling with web pack to reduce files in package and improve loading speed

### Fixed

Ordering issue when creating new barrel introduced in last change

## [1.5.0] 2019-06-15

### Added

Support for recognising nested barrel files and importing the containing folder rather than the contents

### Changed

A lot of re-factoring to use dependency injection and make things more testable as it is no longer the simple extension created to suit own purposes

### Known issues

Occasionally the formatting of a barrel file is not perfect when a nested barrel file is imported and previous individual file imports are removed

## [1.4.0] 2019-03-21

### Added

Support for including files in sub folders in a barrel when creating a new barrel
Support for managing files in sub folders when Auto Barrel - Start is active
Setting to disable sub folder features for both commands

### Known Issues

With sub folder support enabled some index.\* files may be incorrectly recognised as barrel files making it necessary to add an exclusion for the file.

## [1.3.0] 2019-02-28

### Added

Support for including .jsx and .tsx files in barrels. Barrel files themselves still have either .ts or .js.

### Changed

Removed the use of Extension from Language settings. You now select TypeScript or JavaScript and the appropriate file extension is used.

## [1.2.0] 2019-02-16

### Added

Support for default exports
Notification that Start command was successful

## [1.1.1] 2019-02-13

### Fixed

Issue introduced in 1.1.0 where trailing . was left on import statements

## [1.1.0] 2019-02-13

### Added

New setting to enable using an import | alias | export pattern for files added to a barrel so instead of this

```javascript
export * from './auth.actions';
```

With the setting enabled you get this

```javascript
import * as AuthActions from './auth.actions';

export { AuthActions };
```

### Fixed

Issue where windows path separator was hard coded

## [1.0.3] 2019-02-01

### Added

Populated CHANGELOG.md
New setting for list of path fragments that should be ignored with default of ".spec,.test" to ignore test files

### Changed

Reverted changes in [1.0.2] as it was unreliable
Create Barrel uses new setting to prevent files from being included in new barrel file
Start Command handler uses new setting to prevent new files from being added to existing barrel files

## [1.0.2] 2019-02-01

### Changed

Modified default watch glob to exclude files with .spec in the name

## [1.0.1] 2019-21-01

### Added

Added feedback for start command when it is executed and the extension is already started
Added feedback for stop command when it is executed and the extension is not started

### Fixed

Issue where an export for the barrel file was added to itself if it was created after the start command was executed
Issue where the stop command would generate an error if the extension had not been started

## [1.0.0] 2019-21-01

### Added

- Initial release
