# DigLit App – Digital Literacy Driver License

> "And today, in every phone in one of your pockets […] we have access to more information than at any time in human
> history, at a touch of a button.
> But, ironically, the flood of information hasn’t made us more discerning of the truth.
> In some ways, it’s just made us more confident in our ignorance.
> We assume whatever is on the web must be true.
> We search for sites that just reinforce our own predispositions.
> Opinions masquerade as facts.
> The wildest conspiracy theories are taken for gospel." - Barack Obama, 2016

The digital world offers instant access to limitless information, yet also floods us with misinformation, deepfakes,
and AI-generated content.

**DigLit** is a modular, cross-platform learning app designed to equip students with the skills to:

- **Think critically** about online information.
- **Understand AI and algorithms** beyond myths and misconceptions.
- **Engage ethically and responsibly** in digital spaces.

Think of it as a **driver’s license for the internet**, giving young people the competencies they need to navigate
today's AI-powered, fast-moving information highways with confidence and responsibility.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Setup](#setup)
  - [Option A — Using FVM (recommended)](#option-a--using-fvm-recommended)
  - [Option B — Using system Flutter](#option-b--using-system-flutter)
- [Run the App](#run-the-app)
  - [Android](#android)
  - [Web (Chrome)](#web-chrome)
- [Troubleshooting](#troubleshooting)
  - [Linux/NVIDIA emulator crash (X11/DRI3)](#linuxnvidia-emulator-crash-x11dri3)
  - [Gradle tries to write into a read-only Flutter SDK](#gradle-tries-to-write-into-a-read-only-flutter-sdk-eg-usrlibflutter)
  - [ADB/emulator mismatch](#adbemulator-mismatch)

## Prerequisites

- **Dart & Flutter**
  - Recommended via [FVM](https://fvm.app/) to pin the Flutter version per-project
- **Java 17** (required by recent Android Gradle Plugin)
- **Android SDK** (for Android builds)
- **Chrome** (for Web target)
- **VS Code** (recommended IDE, with Flutter and Dart extensions)

Check your toolchain:

```bash
flutter doctor
```

> If you plan to use FVM (recommended), you’ll run `fvm flutter doctor` instead (after installing FVM below).

## Setup

### Option A — Using FVM (recommended)

FVM (Flutter Version Manager) ensures everyone uses the same Flutter SDK version defined by the repository.

1. Clone project repository

    ```bash
    git clone <repo-url> diglit
    cd diglit
    ```

1. Install FVM

    ```bash
    dart pub global activate fvm
    # Ensure FVM is on your PATH (add to your shell rc if needed)
    export PATH="$PATH:$HOME/.pub-cache/bin"
    ```

1. Install the pinned Flutter SDK

    ```bash
    fvm install
    ```

1. Set FVM as the Flutter version for this project

    ```bash
    fvm use
    ```

1. Fetch project dependencies

    ```bash
    fvm flutter pub get
    ```

1. Configure VS Code to use FVM

    VS Code → Settings → "Flutter SDK Path" → set to:

    ```bash
    ${workspaceFolder}/.fvm/flutter_sdk
    ```

### Option B — Using system Flutter

If you prefer your machine’s Flutter installation:

```bash
git clone <repo-url> diglit
cd diglit
flutter --version
flutter pub get
```

## Run the App

### Android

1. Start an Android emulator or connect a device.
  
     Android Studio → Device Manager → Create/start a virtual device

     or

    ```bash
    # With FVM
    fvm flutter emulators
    fvm flutter emulators --launch <avd_name>

    # Or system Flutter
    flutter emulators
    flutter emulators --launch <avd_name>
    ```

    Find the `<avd_name>`:

    ```bash
    emulator -list-avds  
    ```

    You can find the `<avd_name>` using:

    ```bash
    emulator -list-avds  
    ```

1. Accept Android licenses if prompted

    ```bash
    flutter doctor --android-licenses
    ```

1. Run the application on the emulator or connected device

    ```bash
    # With FVM
    fvm flutter run -d <emulator_id_or_device_id>

    # Or system Flutter
    flutter run -d <emulator_id_or_device_id>
    ```

    Find devices:

    ```bash
    # With FVM
    fvm flutter devices

    # Or system Flutter
    flutter devices
    ```

If the run fails, refer to [Troubleshooting](#troubleshooting).

### Web (Chrome)

1. Make sure Chrome is available

    ```bash
    which google-chrome-stable
    ```

1. Run application in Chrome

    ```bash
    # With FVM
    fvm flutter run -d chrome

    # Or system Flutter
    flutter run -d chrome
    ```

### Troubleshooting

### Linux/NVIDIA emulator crash (X11/DRI3)

- Boot once with software GPU:

  ```bash
  emulator -avd <avd_name> -gpu swiftshader_indirect -no-snapshot-load
  ```
  
- Or disable DRI3 for this run:

  ```bash
  LIBGL_DRI3_DISABLE=1 emulator -avd <avd_name> -gpu host -no-snapshot-load
  ```

#### Gradle tries to write into a read-only Flutter SDK (e.g., /usr/lib/flutter)

- Use **FVM** so Gradle resolves the Flutter plugin from:

  ```bash
  .fvm/flutter_sdk/packages/flutter_tools/gradle
  ```

#### ADB/emulator mismatch

- Ensure you’re using the same Android SDK everywhere:

    ```bash
    which adb
    adb version
    echo $ANDROID_SDK_ROOT
    ```

- Kill and restart:

    ```bash
    adb kill-server
    adb start-server
    ```
