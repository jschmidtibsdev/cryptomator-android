# Cryptomator for Android (Fork)

Personal fork of [Cryptomator Android](https://github.com/cryptomator/android) with license check removed.

## Building the APK

### With Docker (recommended)

No JDK or Android SDK needed — just Docker.

```bash
# Build the Docker image (one-time, takes a few minutes)
docker build -t cryptomator-android buildsystem/

# Build the APK
docker run --rm -v "$(pwd)":/project -w /project cryptomator-android ./gradlew clean assembleApkstoreDebug
```

On Windows (PowerShell):
```powershell
docker build -t cryptomator-android buildsystem/
docker run --rm -v "${PWD}:/project" -w /project cryptomator-android ./gradlew clean assembleApkstoreDebug
```

The APK will be at:
```
presentation/build/outputs/apk/apkstore/debug/presentation-apkstore-debug.apk
```

Transfer to your Android device and install (enable "Install from unknown sources").

### Without Docker

Requires JDK 17 and Android SDK (API 35, Build Tools 35.0.1).

```bash
./gradlew assembleApkstoreDebug
```

### Cloud Provider API Keys (Optional)

Without API keys, cloud providers (Dropbox, OneDrive, pCloud, Google Drive) won't work. For debug builds, set environment variables: `DROPBOX_API_KEY_DEBUG`, `ONEDRIVE_API_KEY_DEBUG`, `ONEDRIVE_API_REDIRCT_URI_DEBUG`, `PCLOUD_CLIENT_ID_DEBUG`.

Google Drive requires a [Google Cloud Platform](https://console.cloud.google.com) project with Drive API enabled and OAuth credentials matching your signing key fingerprint.

## Syncing with Upstream

```bash
# Add upstream remote (one-time)
git remote add upstream https://github.com/cryptomator/android.git

# Fetch and merge latest changes
git fetch upstream
git checkout develop
git merge upstream/develop
git push origin develop
```

To merge a specific release tag:
```bash
git fetch upstream --tags
git merge <tag-name>
```

## License

Dual-licensed under GPLv3 and a commercial license. See upstream repository for details.
