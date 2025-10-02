# Unyt Releases

![GitHub release (latest by date)](https://img.shields.io/github/v/release/unytco/unyt-app-tx5?style=for-the-badge)
![GitHub All Releases](https://img.shields.io/github/downloads/unytco/unyt-app-tx5/total?style=for-the-badge)

## Intro

Unyt is a Holochain based application for creating agent-centric, peer-to-peer, Mutual Credit accounting systems with smart contract like functionality.

We are working with potential partner projects like yours as we build out this software to ensure that it meets the needs of your team as well as your community of users.

## Overview

This [Test Plan](./testing_docs/1_0_testing_plan.md) document gives a bit of a overview of the sorts of UX / UI feedback that we are seeking at present.

## Installation

Download the appropriate version for your system.

| Releases                                                                     |
| ---------------------------------------------------------------------------- |
| [macOS x64 (Intel)](https://downloads.unyt.co/macos-x64)                     |
| [macOS arm64 (Silicon)](https://downloads.unyt.co/macos-arm64)               |
| [Linux Debian](https://downloads.unyt.co/linux-deb) (recommended)            |
| [Linux AppImage](https://downloads.unyt.co/linux-appimage) (read note below) |
| [Windows](https://downloads.unyt.co/windows)                                 |
| [Android](#) (no release available)                                          |
| [iOS](#) (no release available)                                              |

> [!IMPORTANT]
> If you encounter sandbox-related issues, you can try running the AppImage with:
>
> ```bash
> ELECTRON_DISABLE_SANDBOX=1 ./unyt.AppImage
> ```
>
> This is automatically configured in the latest version, but might be needed for manual execution in some cases.

All available versions can be found in the [Releases](https://github.com/unytco/unyt-app-tx5/releases)

Once installed, set up Unyt either with a password or without a password. In either case, the software will run locally on your device and your password will not leave your device.

NOTE: If you set up with a password and later lose your password, we will NOT be able to help you regain access to your account. You will need to delete the software and reinstall to create a fresh account to continue testing. See below section on **Starting Fresh**.

## Setup

Note: The release for your operating system may not be code signed yet, so you may need to right click to open the file. In Mac, because you downloaded the software directly and not through Apple's App Store, you may need to open the System Settings and go to Privacy and Security, scroll down to Security and give Unyt permission to run.

When you open Unyt on your operating system for the first time, it will create a set of public and private keys for you that you can use to interact with others. These are stored in a private keystore (Lair) on your own machine and are used during future uses.

To get started, you can try sending, executing, and receiving transactions either with friends that have also downloaded Unyt, or with team members from the Development Team.

for v0.13.0:
Matthew's Public Key is:
`uhCAkOKFD_M3OuSQ8q-oEMSC-gKOHIJuchdp8eS1W1jnWPnWAW65F`

Jarod's Public Key is:
`uhCAkBNcC5msV7syB9I71XS18GMQDugPMQ6N6XQsU2cVHr5Y-YgWc`

## Starting Fresh

Details on removal and reinstallation.

If you want to start fresh (whether because you lost a password or for another reason), uninstall the old version and then reinstall again. On Mac, you will also need to delete your local data:

Here are the steps for Uninstalling, Deleting Local Data and Reinstalling the app:

1. Close the app.

2. Delete the unyt file from your applications folder.

3. Open the Terminal application
4. In Terminal, type the following two commands and hit enter after each:

```
cd ~/Library/Application\ Support
```

```
rm -rf co.unyt.unyt
```

That co.unyt.unyt file had your local data in it.

Now that it is deleted, you can again install unyt and start fresh with a new account.

Next, dive into the [Test Plan](./testing_docs/1_0_testing_plan.md).

## License

[![License: CAL 1.0](https://img.shields.io/badge/License-CAL%201.0-blue.svg)](https://github.com/holochain/cryptographic-autonomy-license)

<<<<<<< HEAD
Copyright (C) 2024 - 2025, unyt.co

=======

```
yarn build:linux

# or
yarn build:mac

# or
yarn build:windows
```

### Build on CI for all platforms

The general workflow goes as follows:

1. Make sure that CI has access to your app's .webhapp file by either

   - specifying the `webhapp` field in `kangaroo.config.ts` pointing to a URL where CI can fetch it and a sha256 to verify its integrity
   - remove `pouch/*.webhapp` from the `.gitignore` file and commit your .webhapp to git.

2. Create a draft release on github and set its "Tag verion" to the value of the `version` field that you chose in `kangaroo.config.ts` and prefix it with `v`, for example `v0.1.0`.

3. Merge the main branch into the release branch and push it to github to trigger the release workflow.

If you do this for the first time you will need to create the `release` branch first:

```
git checkout -b release
git merge main
git push --set-upstream origin release
```

For subsequent releases after that you can run

```
git checkout release
git merge main
git push
```

## Automatic Updates

By default, the kangaroo is set up to check github releases for semver compatible releases by their tag name whenever the app starts up and will prompt to install and restart if one is available. This can be disabled by setting `autoUpdates` to `false` in `kangaroo.config.ts`.

> [!NOTE]
> Note that once your app is deployed, this setting can only be turned on again for newer releases and users will have to manually install new versions.

## Versioning

To allow for subsequent incompatible releases of your app (for example due to switching to a new Holochain version) without having to change the app's name or identifier, the kangaroo is set up to use semver to support incompatible versions of your app running fully independently from each other and store their data in dedicated locations on disk.

Examples:

- version 0.0.2 and 0.0.3 of your app will store their data in independent locations on disk and version 0.0.3 will not have access to any data created/obtained in version 0.0.2
- version 0.3.4 will reuse the same Holochain conductor and data as version 0.3.2
- versions 0.3.0-alpha and 0.3.0-beta will _not_ share data
- versions 0.3.0-alpha.0 and 0.3.0-alpha.1 _will_ share data

> [!NOTE]
> It is your responsibility to make sure that if you mark two versions of your app as semver compatible they actually are compatible (e.g. that you don't try to run a new incompatible version of Holochain on existing databases).

## Code Signing

### macOS

To use code signing on macOS for your release in CI you will have to

1. Set the `macOSCodeSigning` field to `true` in `kangaroo.config.ts`
2. Add the following secrets to your github repository with the appropriate values:

- `APPLE_DEV_IDENTITY`
- `APPLE_ID_EMAIL`
- `APPLE_ID_PASSWORD`
- `APPLE_TEAM_ID`
- `APPLE_CERTIFICATE`
- `APPLE_CERTIFICATE_PASSWORD`

3. Uncomment the line `afterSign: scripts/notarize.js` in `./templates/electron-builder-template.yml`.

> [!WARNING] > **Unsigned applications are put under quarantine on macOS 15 (Sequoia).** The option in the Privacy & Security panel of the System Settings to allow them has been removed. To unset the quarantine attribute of an unsigned app,
> the command `xattr -r -d com.apple.quarantine /path/to/app` can be executed from a Terminal. The app can then be run.

### Windows

If you want to code sign your app with an EV certificate, you can follow [this guide](https://melatonin.dev/blog/how-to-code-sign-windows-installers-with-an-ev-cert-on-github-actions/) to get your EV certificate hosted on Azure Key Vault and then

1. Set the `windowsEVCodeSigning` field to `true` in `kangaroo.config.ts`
2. Add all the necessary secrets to the repository:

- `AZURE_KEY_VAULT_URI`
- `AZURE_CERT_NAME`
- `AZURE_TENANT_ID`
- `AZURE_CLIENT_ID`
- `AZURE_CLIENT_SECRET`

## Permissions on macOS

Access to things like camera and microphone on macOS require special permissions to be set in the .plist file. For this, uncomment the corresponding permissions in `./templates/electron-builder-template.yml` as needed.

## Run your App from the command line

If you want to customize some runtime parameters you can run your app via the terminal and pass additional options:

```
Options:
  -V, --version                  output the version number
  -p, --profile <string>         Runs Holochain Kangaroo Electron (Test) with a custom profile with its own dedicated data store.
  -n, --network-seed <string>    If this is the first time running kangaroo with the given profile, this installs the happ with the
                                 provided network seed.
  --holochain-path <path>        Runs Holochain Kangaroo Electron (Test) with the holochain binary at the provided path. Use with caution
                                 since this may potentially corrupt your databases if the binary you use is not compatible with existing
                                 databases.
  --lair-path <path>             Runs the Holochain Kangaroo Electron (Test) with the lair binary at the provided path. Use with caution
                                 since this may potentially corrupt your databases if the binary you use is not compatible with existing
                                 databases.
  --holochain-rust-log <string>  RUST_LOG value to pass to the holochain binary
  --holochain-wasm-log <string>  WASM_LOG value to pass to the holochain binary
  --lair-rust-log <string>       RUST_LOG value to pass to the lair keystore binary
  -b, --bootstrap-url <url>      URL of the bootstrap server to use (not persisted across restarts).
  -s, --signal-url <url>      URL of the signaling server to use (not persisted across restarts).
  --ice-urls <string>            Comma separated string of ICE server URLs to use. Is ignored if an external holochain binary is being used
                                 (not persisted across restarts).
  --print-holochain-logs         Print holochain logs directly to the terminal (they will be still written to the logfile as well)
  -h, --help                     display help for command
```

> > > > > > > main
