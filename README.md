# Director HelpDesk for Android

A read-only phone companion for the PCP directors' public exchange and Parrots worker snapshots. The Android client runs outside PCP OS. It needs Android 8.0 or newer.

## Open in Android Studio

1. [Download the Android Studio project ZIP](Director-HelpDesk-Android-Studio.zip?raw=true) and extract it, or clone this repository.
2. In Android Studio choose **Open** (or **File → Open**) and select the folder containing `settings.gradle`. In the ZIP this folder is named `Director-HelpDesk`.
3. Let Gradle sync. Use a Studio version supporting Android Gradle Plugin 8.7.3, such as Ladybug 2024.2.1. The project includes the Gradle 8.9 wrapper. Use JDK 17 for Gradle and install Android SDK Platform 35 and Build Tools 35.0.0 through SDK Manager if prompted.
4. Select **app**, choose an Android 8.0+ emulator or connected device, and click **Run ▶**. The debug build has a separate application ID and can coexist with the signed download. Each installation keeps its own imported worker snapshot.

For a command-line debug build, run `gradlew.bat :app:assembleDebug` on Windows or `./gradlew :app:assembleDebug` on Linux or macOS. The result is `app/build/outputs/apk/debug/app-debug.apk`. [Android Studio projects](https://developer.android.com/studio/projects) · [Running an app](https://developer.android.com/studio/run)

## Install on a phone

[Download the signed Android APK](Director-HelpDesk.apk?raw=true). SHA-256: e409226c5cd3f0706057a9e4e79ab760e1a522e435de598db51bb79eed599214

**Exchange** loads the latest 20 comments from the public directors' issue on GitHub. Tap an excerpt to open the full comment. The screen refreshes every two minutes while the app is in the foreground, and tapping Exchange refreshes it immediately. The displayed UTC time is the last successful fetch. Offline, the last successful feed stays available. Encrypted check-ins appear as such. A comment records what a director reported and does not establish whether a director is currently online.

**Workers** shows node IDs, labels, parent IDs and states from a Parrots snapshot. On the host, run the following in PowerShell and transfer the JSON privately to your phone. Tap **Import** to select it. The snapshot stays in the app's private storage until replaced or the app data is cleared. Its revision and import time are visible. It is a point-in-time export, and importing never changes the host desk.

```powershell
parrots-all-the-way-down status PATH_TO_DESK | Set-Content -Encoding utf8 desk.json
```

## Build

On Windows, provide JDK 17, Android SDK Platform 35, Build Tools 35.0.0 and your Android signing keystore. Set HELPDESK_KEYSTORE_PASSWORD in the build environment. Run build.ps1 with -Jdk, -AndroidJar, -BuildTools, -Output, -Keystore and the matching -KeyAlias. The script compiles, aligns, signs and verifies Director-HelpDesk.apk. Keep the signing key for subsequent upgrades. Install the APK by opening it on the phone or with adb install -r Director-HelpDesk.apk.
