# Client library for the Google Play APK Expansion files.

## Installation 

In your module's `build.gradle` dependencies:
```GROOVY
compile 'com.github.bolein:better-apk-expansion:4.0.0'
```

In your root project's `build.gradle`:
```GROOVY
allprojects {
// ...
    repositories {
        // ...
        maven { url "https://jitpack.io" } // add this line
    }
}
```

## How to use

### Linking obb files
In order to test the download, your aplication must be published in Google Play (alpha or beta release works). Before starting to test the download, make sure that you have assosiated at least one OBB file with your current application's `versionCode`. Versions that have no assosiated expansion files can't start the donwload. You can assosiate the OBB files when you upload the apk file to the Play Console. 

Check the [APK Expansion Files documentation](https://developer.android.com/google/play/expansion-files.html#Overview) for more information about OBB files.

### Configuring Play Licensing
To start the downloading process you should first obrain a valid licensing response. Make sure that you have correctly set your publisher key. For more info about publisher account check the [documentation](https://developer.android.com/google/play/licensing/setting-up.html#account).

You can also set up your testing environment to always receive a valid response (see the [licensing documentation](https://developer.android.com/google/play/licensing/setting-up.html#test-env) for more info).

## Changelog
Version 4
* Updated for Marshmallow
   - No longer uses Apache HTTP
   - No longer relies on removed Notification methods
* Changed to refer to Google Play
* Notifications now rely on support library.

Version 3
* Directory structure corrected in distribution. No code changes.

Version 2
* Patch file now gets downloaded.
* Honeycomb devices now supported with ICS-like notifications
* CRC check (from sample) now supports compressed Zip files
* Use of reflection removed to allow easy obfuscation
* Service leak fixed
* Unprintable character removed from ZipResourceFile
* Minor formatting changes
* Additional comments and edits to this file

## Packages

### downloader_library
A library that works with the google_market_licensing library to download APK Expansion files in a background service.  This library depends on the licensing library, and must be built as a library project.
### zip_file 
A library that uses multiple zip files as a virtual read-only filesystem with hooks to support APK Expansion lies. This also must be built as an Android library project.
### downloader_sample
A sample application that assumes that zip format files have been uploaded as the main/patch file(s) on Android Market.  It downloads these files and then validates that the CRC's for every entry in the zip match.  This application depends on the downloader_library and the zip_file library. Because of dependency issues involving multiple libraries, you may have to do a clean build after creating each project.

## IMPORTANT THINGS TO KNOW

1) Do not plan to extract the contents of an APK Expansion file.  They are intended to be used in-place.  By not compressing audio and video files and storing them in a Zip file they can be played from within an expansion file.
2) See com.google.android.vending.expansion.downloader/Constants.java to turn on verbose logging in the library.  Please turn it off when you publish
3) You must add your SALT and Public key to the SampleDownloaderService and update the xAPKS structure in SampleDownloaderActivity in order to test with the sample code
4) There is no strong need to include the validator with your Android applications.  It is included as a demonstration, and can be used if you wish.

For more information, see the documentation at http://developer.android.com/guide/market/expansion-files.html

This library depends on the [Android License Verification Library](https://github.com/bolein/better-licensing).

See the licensing documentation at http://developer.android.com/guide/publishing/licensing.html
