# ElementumService

A service that executes binaries for [Kodi](https://github.com/xbmc/xbmc)'s addon [Elementum](https://github.com/elgatito/plugin.video.elementum) on [Android](https://www.android.com/) without a [W^X violation](https://developer.android.com/about/versions/10/behavior-changes-10#execute-permission).

## Build

Prepare an [Elementum](https://github.com/elgatito/plugin.video.elementum) addon `.zip` at `path/to/plugin.video.elementum-<version>.zip` containing [Android](https://www.android.com/) binaries for your device either by [building the Elementum project](https://github.com/elgatito/plugin.video.elementum#build) or by downloading it from a [release's](https://github.com/elgatito/plugin.video.elementum/releases) assets.

Assuming you already have [Android Studio](https://developer.android.com/studio) setup, execute the following command in a terminal:

```bat
gradlew clean assembleRelease zipAndroidClient -DaddonZip="path/to/plugin.video.elementum-<version>.zip"
```

and when it completes successfully look for the following files in the newly created `build` folder:

1. `plugin.video.elementum-<version>.android_client.zip` found directly in the `build` folder is the addon `.zip` you provided with its binaries removed and scripts modified to work with the service app;

2. `ElementumService-<ABI>-release-<version>.apk` found in the `build/outputs/apk/release` subfolder are one or more `.apk` files containing the binaries from the addon `.zip` you provided.

## Install

Install an `.apk` with an [Application Binary Interface](https://en.wikipedia.org/wiki/Application_binary_interface) (ABI) that your device supports or the bigger universal one.

Add [Elementum](https://github.com/elgatito/plugin.video.elementum) to [Kodi](https://github.com/xbmc/xbmc) from the `.android_client.zip`. When the addon completes installation it'll start the service app which may ask you for some [Android permissions](https://support.google.com/googleplay/answer/6270602).

## Notes

From now on when [Elementum](https://github.com/elgatito/plugin.video.elementum) starts its daemon it'll actually start the service app and when it stops it'll stop the service app.

You'll no longer be able to use paths to [Kodi](https://github.com/xbmc/xbmc)'s data folder as they will be translated to the service app's data folder.

The output from the binaries will no longer appear in [Kodi's log](https://kodi.wiki/view/Log_file) and will go to [Android's log](https://developer.android.com/studio/command-line/logcat) instead.
