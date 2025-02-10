
# React Native iCloud Account Status <!-- omit from toc -->

React Native module to determine whether the current user’s iCloud account can be accessed.

## Table of contents <!-- omit from toc -->

- [balns internal use](#balns-internal-use)
  - [Upgrading React Native versions](#upgrading-react-native-versions)
- [Getting started](#getting-started)
  - [Requirements](#requirements)
  - [Mostly automatic installation](#mostly-automatic-installation)
  - [Manual installation](#manual-installation)
- [Usage](#usage)
- [API](#api)
  - [Constants](#constants)
  - [Methods](#methods)
    - [getStatus()](#getstatus)
- [License](#license)


## balns internal use

### Upgrading React Native versions

- The `react-native` package version used in this repo needs to be synchronysed with the other balns dependencies
- So far, it seems sufficient to increase the package version number in `package.json` (under `peerDependencies`). The version of this package should similarly be incremented with each such change.
- This repo does not have its own example app, so this cannot be tested in isolation
- Run `npm i` to update `package-lock.json` as well
- To create and publish an updated tag:
  ```bash
  git tag 1.0.x
  git push origin 1.0.x
  ```

## Getting started

### Requirements

* iOS 8.0+
* The iCloud capability with CloudKit:
  1. Click on your target and then the Capabilities tab
  2. Turn on the iCloud capability
  3. Expand it and check the CloudKit option under Services

### Mostly automatic installation

1. `$ npm install react-native-icloud-account-status --save`
2. **React Native 0.60+**: `$ cd ios && pod install`  
   **React Native <0.60**: `$ react-native link react-native-icloud-account-status`

### Manual installation

1. `$ npm install react-native-icloud-account-status --save`
2. In XCode, in the project navigator, right click `Libraries` ➜ `Add Files to [your project's name]`
3. Go to `node_modules` ➜ `react-native-icloud-account-status` and add `RNIcloudAccountStatus.xcodeproj`
4. In XCode, in the project navigator, select your project. Add `libRNIcloudAccountStatus.a` to your project's `Build Phases` ➜ `Link Binary With Libraries`
5. Run your project (`Cmd+R`)

## Usage

```javascript
import iCloudAccountStatus from 'react-native-icloud-account-status';

iCloudAccountStatus.getStatus()
  .then((accountStatus) => {
    if (accountStatus === iCloudAccountStatus.STATUS_AVAILABLE) {
      alert('iCloud is available');
    } else {
      alert('iCloud is not available');
    }
  })
  .catch((error) => {
    alert(`Error when getting iCloud account status: ${error.message}`);
  });
```

## API

### Constants

* `STATUS_COULD_NOT_DETERMINE`
* `STATUS_AVAILABLE`
* `STATUS_RESTRICTED`
* `STATUS_NO_ACCOUNT`

### Methods

#### getStatus()

Gets the current user's iCloud account status.

Returns a `Promise` that resolves to a string of one of the following:

* `'couldNotDetermine'`
* `'available'`
* `'restricted'`
* `'noAccount'`

For more information about each status, see [`CKAccountStatus`](https://developer.apple.com/documentation/cloudkit/ckaccountstatus?language=objc) at the Apple Developer Documentation.

## License

Copyright (c) 2020 Blockfirm AB

This project is licensed under the MIT License.
See [LICENSE](LICENSE) for full license text.
