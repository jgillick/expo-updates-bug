# Repro Repo for Expo Update bug

When installing expo into an existing react native project, and adding expo-updates without EAS build, the updates config doesn't get built into the app.

For example, on ios, with `EXUpdatesEnabled` set to `<true />` in `Expo.plist`, inside the app `Updates.isEnabled` is `false`. Further, the `runtimeVersion` is also any empty string. It appears that all the values are set to default.

## Installation steps:

1. `npx @react-native-community/cli@latest init expoUpdatesBug` ([source](https://reactnative.dev/docs/getting-started-without-a-framework))
2. `npx install-expo-modules@latest` ([source](https://docs.expo.dev/bare/installing-expo-modules/#automatic-installation))
3. `npx expo install expo-updates` ([source](https://docs.expo.dev/bare/installing-updates/))
4. `npx pod-install` ([source](https://docs.expo.dev/bare/installing-updates/))
5. `npx eas-cli@latest update:configure` ([source](https://docs.expo.dev/bare/installing-updates/#javascript-and-json))
6. Update `app.json` ([source](https://docs.expo.dev/bare/installing-updates/#javascript-and-json))
7. Update `build.gradle`, `AndroidManifest.xml`, and `strings.xml` ([source](https://docs.expo.dev/bare/installing-updates/#android))
8. Update `Podfile.properties.json`, `Podfile`, and `Expo.plist` ([source](https://docs.expo.dev/bare/installing-updates/#ios))
9. ([source](https://docs.expo.dev/eas-update/standalone-service/#using-eas-update-without-eas-build) [and](https://docs.expo.dev/eas-update/getting-started/#configure-the-update-channel)) -- [this page](https://docs.expo.dev/eas-update/standalone-service/#using-eas-update-without-eas-build) should link directly to [this](https://docs.expo.dev/eas-update/getting-started/#configure-the-update-channel), for clarity.
10. Edit `App.tsx` to log `Updates` module (see [App.tsx](./App.tsx)).
11. Run `npx expo run:ios`
12. View logs

## Update module output:

```json
{
  "channel": "",
  "checkAutomatically": "NEVER",
  "createdAt": null,
  "isEmbeddedLaunch": false,
  "isEmergencyLaunch": false,
  "isEnabled": false,
  "isUsingEmbeddedAssets": false,
  "localAssets": {},
  "manifest": {},
  "runtimeVersion": "",
  "updateId": null,
  "latestContext": {
    "checkError": null,
    "rollback": null,
    "isRestarting": false,
    "sequenceNumber": 0,
    "latestManifest": null,
    "isDownloading": false,
    "downloadedManifest": null,
    "isUpdatePending": false,
    "downloadError": null,
    "isRollback": false,
    "isChecking": false,
    "isUpdateAvailable": false,
    "lastCheckForUpdateTimeString": null
  },
  "UpdateCheckResultNotAvailableReason": {
    "NO_UPDATE_AVAILABLE_ON_SERVER": "noUpdateAvailableOnServer",
    "UPDATE_REJECTED_BY_SELECTION_POLICY": "updateRejectedBySelectionPolicy",
    "UPDATE_PREVIOUSLY_FAILED": "updatePreviouslyFailed",
    "ROLLBACK_REJECTED_BY_SELECTION_POLICY": "rollbackRejectedBySelectionPolicy",
    "ROLLBACK_NO_EMBEDDED": "rollbackNoEmbeddedConfiguration"
  },
  "UpdatesCheckAutomaticallyValue": {
    "ON_LOAD": "ON_LOAD",
    "ON_ERROR_RECOVERY": "ON_ERROR_RECOVERY",
    "WIFI_ONLY": "WIFI_ONLY",
    "NEVER": "NEVER"
  },
  "UpdatesLogEntryCode": {
    "NONE": "None",
    "NO_UPDATES_AVAILABLE": "NoUpdatesAvailable",
    "UPDATE_ASSETS_NOT_AVAILABLE": "UpdateAssetsNotAvailable",
    "UPDATE_SERVER_UNREACHABLE": "UpdateServerUnreachable",
    "UPDATE_HAS_INVALID_SIGNATURE": "UpdateHasInvalidSignature",
    "UPDATE_CODE_SIGNING_ERROR": "UpdateCodeSigningError",
    "UPDATE_FAILED_TO_LOAD": "UpdateFailedToLoad",
    "ASSETS_FAILED_TO_LOAD": "AssetsFailedToLoad",
    "JS_RUNTIME_ERROR": "JSRuntimeError",
    "INITIALIZATION_ERROR": "InitializationError",
    "UNKNOWN": "Unknown"
  },
  "UpdatesLogEntryLevel": {
    "TRACE": "trace",
    "DEBUG": "debug",
    "INFO": "info",
    "WARN": "warn",
    "ERROR": "error",
    "FATAL": "fatal"
  },
  "UpdateInfoType": {
    "NEW": "new",
    "ROLLBACK": "rollback"
  }
}
```
