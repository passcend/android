# Passcend Android

---

## 목차

- [호환성](#호환성)
- [설정](#설정)
- [의존성](#의존성)

## 호환성

- **최소 SDK**: 29 (Android 10)
- **대상 SDK**: 36 (Android 16)
- **지원 기기**: 스마트폰 및 태블릿
- **지원 방향**: 세로 및 가로 모드

## 설정

1. 저장소 복제:

    ```sh
    $ git clone https://github.com/your-org/passcend
    $ cd passcend/android
    ```

2. 프로젝트 루트 디렉토리에 `user.properties` 파일을 생성하고 다음 속성을 추가합니다:

    - `gitHubToken`: `read:packages` 스코프를 가진 GitHub Personal Access Token (PAT) (예: `gitHubToken=gph_xx...xx`). [GitHub 토큰 페이지](https://github.com/settings/tokens)에서 생성할 수 있습니다.
    - `localSdk`: 로컬 maven에서 SDK를 로드할지 여부를 결정하는 불리언 값 (예: `localSdk=true`). 새로운 SDK 기능을 개발할 때 유용합니다.

3. Setup the code style formatter:

    All code must follow the guidelines described in the [Code Style Guidelines document](docs/STYLE_AND_BEST_PRACTICES.md). To aid in adhering to these rules, all contributors should apply `docs/bitwarden-style.xml` as their code style scheme. In IntelliJ / Android Studio:

    - Navigate to `Preferences > Editor > Code Style`.
    - Hit the `Manage` button next to `Scheme`.
    - Select `Import`.
    - Find the `bitwarden-style.xml` file in the project's `docs/` directory.
    - Import "from" `BitwardenStyle` "to" `BitwardenStyle`.
    - Hit `Apply` and `OK` to save the changes and exit Preferences.

    Note that in some cases you may need to restart Android Studio for the changes to take effect.

    All code should be formatted before submitting a pull request. This can be done manually but it can also be helpful to create a macro with a custom keyboard binding to auto-format when saving. In Android Studio on OS X:

    - Select `Edit > Macros > Start Macro Recording`
    - Select `Code > Optimize Imports`
    - Select `Code > Reformat Code`
    - Select `File > Save All`
    - Select `Edit > Macros > Stop Macro Recording`

    This can then be mapped to a set of keys by navigating to `Android Studio > Preferences` and editing the macro under `Keymap` (ex : shift + command + s).

    Please avoid mixing formatting and logical changes in the same commit/PR. When possible, fix any large formatting issues in a separate PR before opening one to make logical changes to the same code. This helps others focus on the meaningful code changes when reviewing the code.

4. Setup JDK `Version` `21`:

    - Navigate to `Preferences > Build, Execution, Deployment > Build Tools > Gradle`.
    - Hit the selected Gradle JDK next to `Gradle JDK:`.
    - Select a `21.x` version or hit `Download JDK...` if not present.
    - Select `Version` `21`.
    - Select your preferred `Vendor`.
    - Hit `Download`.
    - Hit `Apply`.

5. Setup `detekt` pre-commit hook (optional):

Run the following script from the root of the repository to install the hook. This will overwrite any existing pre-commit hook if present.

```shell
echo "Writing detekt pre-commit hook..."
cat << 'EOL' > .git/hooks/pre-commit
#!/usr/bin/env bash

echo "Running detekt check..."
OUTPUT="/tmp/detekt-$(date +%s)"
./gradlew -Pprecommit=true detekt > $OUTPUT
EXIT_CODE=$?
if [ $EXIT_CODE -ne 0 ]; then
  cat $OUTPUT
  rm $OUTPUT
  echo "***********************************************"
  echo "                 detekt failed                 "
  echo " Please fix the above issues before committing "
  echo "***********************************************"
  exit $EXIT_CODE
fi
rm $OUTPUT
EOL
echo "detekt pre-commit hook written to .git/hooks/pre-commit"
echo "Making the hook executable"
chmod +x .git/hooks/pre-commit

echo "detekt pre-commit hook installed successfully to .git/hooks/pre-commit"
```

## Dependencies

### Application Dependencies

The following is a list of all third-party dependencies included as part of the application beyond the standard Android SDK.

- **AndroidX Activity**
    - https://developer.android.com/jetpack/androidx/releases/activity
    - Purpose: Allows access composable APIs built on top of Activity.
    - License: Apache 2.0

- **AndroidX Appcompat**
    - https://developer.android.com/jetpack/androidx/releases/appcompat
    - Purpose: Allows access to new APIs on older API versions.
    - License: Apache 2.0

- **AndroidX Autofill**
    - https://developer.android.com/jetpack/androidx/releases/autofill
    - Purpose: Allows access to tools for building inline autofill UI.
    - License: Apache 2.0

- **AndroidX Biometrics**
    - https://developer.android.com/jetpack/androidx/releases/biometric
    - Purpose: Authenticate with biometrics or device credentials.
    - License: Apache 2.0

- **AndroidX Browser**
    - https://developer.android.com/jetpack/androidx/releases/browser
    - Purpose: Displays webpages with the user's default browser.
    - License: Apache 2.0

- **AndroidX Camera**
    - https://developer.android.com/jetpack/androidx/releases/camera
    - Purpose: Display and capture images for barcode scanning.
    - License: Apache 2.0

- **AndroidX Compose**
    - https://developer.android.com/jetpack/androidx/releases/compose
    - Purpose: A Kotlin-based declarative UI framework.
    - License: Apache 2.0

- **AndroidX Core**
    - https://developer.android.com/jetpack/androidx/releases/core
    - Purpose: Backwards compatible platform features and APIs.
    - License: Apache 2.0

- **AndroidX Credentials**
    - https://developer.android.com/jetpack/androidx/releases/credentials
    - Purpose: Unified access to user's credentials.
    - License: Apache 2.0

- **AndroidX Lifecycle**
    - https://developer.android.com/jetpack/androidx/releases/lifecycle
    - Purpose: Lifecycle aware components and tooling.
    - License: Apache 2.0

- **AndroidX Navigation**
    - https://developer.android.com/jetpack/androidx/releases/navigation
    - Purpose: Provides a consistent API for navigating between Android components.
    - License: Apache 2.0

- **AndroidX Room**
    - https://developer.android.com/jetpack/androidx/releases/room
    - Purpose: A convenient SQLite-based persistence layer for Android.
    - License: Apache 2.0

- **AndroidX Security**
    - https://developer.android.com/jetpack/androidx/releases/security
    - Purpose: Safely manage keys and encrypt files and sharedpreferences.
    - License: Apache 2.0

- **AndroidX WorkManager**
    - https://developer.android.com/jetpack/androidx/releases/work
    - Purpose: The WorkManager is used to schedule deferrable, asynchronous tasks that must be run reliably.
    - License: Apache 2.0

- **Dagger Hilt**
    - https://github.com/google/dagger
    - Purpose: Dependency injection framework.
    - License: Apache 2.0

- **Glide**
    - https://github.com/bumptech/glide
    - Purpose: Image loading and caching.
    - License: BSD, part MIT and Apache 2.0

- **kotlinx.collections.immutable**
    - https://github.com/Kotlin/kotlinx.collections.immutable
    - Purpose: Immutable collection interfaces and implementation prototypes for Kotlin.
    - License: Apache 2.0

- **kotlinx.coroutines**
    - https://github.com/Kotlin/kotlinx.coroutines
    - Purpose: Kotlin coroutines library for asynchronous and reactive code.
    - License: Apache 2.0

- **kotlinx.serialization**
    - https://github.com/Kotlin/kotlinx.serialization/
    - Purpose: JSON serialization library for Kotlin.
    - License: Apache 2.0

- **OkHttp 3**
    - https://github.com/square/okhttp
    - Purpose: An HTTP client used by the library to intercept and log traffic.
    - License: Apache 2.0

- **Retrofit 2**
    - https://github.com/square/retrofit
    - Purpose: A networking layer interface.
    - License: Apache 2.0

- **Timber**
    - https://github.com/JakeWharton/timber
    - Purpose: Extensible logging library for Android.
    - License: Apache 2.0

- **ZXing**
    - https://github.com/zxing/zxing
    - Purpose: Barcode scanning and generation.
    - License: Apache 2.0

The following is an additional list of third-party dependencies that are only included in the non-F-Droid build variants of the application.

- **Firebase Cloud Messaging**
    - https://github.com/firebase/firebase-android-sdk
    - Purpose: Allows for push notification support.
    - License: Apache 2.0

- **Firebase Crashlytics**
    - https://github.com/firebase/firebase-android-sdk
    - Purpose: SDK for crash and non-fatal error reporting.
    - License: Apache 2.0

- **Google Play Reviews**
    - https://developer.android.com/reference/com/google/android/play/core/release-notes
    - Purpose: On standard builds provide an interface to add a review for the password manager application in Google Play.
    - License: Apache 2.0

### Development Environment Dependencies

The following is a list of additional third-party dependencies used as part of the local development environment. This includes test-related artifacts as well as tools related to code quality and linting. These are not present in the final packaged application.

- **detekt**
    - https://github.com/detekt/detekt
    - Purpose: A static code analysis tool for the Kotlin programming language.
    - License: Apache 2.0

- **JUnit 5**
    - https://github.com/junit-team/junit5
    - Purpose: Unit Testing framework for testing application code.
    - License: Eclipse Public License 2.0

- **MockK**
    - https://github.com/mockk/mockk
    - Purpose: Kotlin-friendly mocking library.
    - License: Apache 2.0

- **Robolectric**
    - https://github.com/robolectric/robolectric
    - Purpose: A unit testing framework for code directly depending on the Android framework.
    - License: MIT

- **Turbine**
    - https://github.com/cashapp/turbine
    - Purpose: A small testing library for kotlinx.coroutine's Flow.
    - License: Apache 2.0

### CI/CD Dependencies

The following is a list of additional third-party dependencies used as part of the CI/CD workflows. These are not present in the final packaged application.

- **Fastlane**
    - https://fastlane.tools/
    - Purpose: Automates building, signing, and distributing applications.
    - License: MIT

- **Kover**
    - https://github.com/Kotlin/kotlinx-kover
    - Purpose: Kotlin code coverage toolset.
    - License: Apache 2.0
