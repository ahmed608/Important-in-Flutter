# Important in Flutter

## Introduction
Flutter is a powerful framework for building cross-platform applications. This README provides essential commands, important packages, common issues, and their solutions to help you master Flutter development.

---

## 1. Important Commands

### General Commands
```sh
flutter doctor           # Checks Flutter installation and dependencies
flutter create my_app    # Creates a new Flutter project
flutter run              # Runs the app on a connected device or emulator
flutter build apk        # Builds an APK for Android
flutter build ios        # Builds an iOS app
flutter clean            # Clears the build cache
flutter pub get          # Fetches dependencies from pubspec.yaml
flutter pub upgrade      # Updates dependencies to the latest versions
flutter analyze          # Analyzes the project for potential issues
flutter format .         # Formats all Dart files in the project
flutter test             # Runs tests in the project
flutter build apk --target-platform android-arm,android-arm64,android-x64 --split-per-abi
```

### Dart Commands
```sh
dart --version         # Checks Dart version
dart run file.dart     # Runs a specific Dart file
dart analyze          # Analyzes Dart code for errors and warnings
```

### Build APK for Different Architectures
```sh
flutter build apk --target-platform android-arm,android-arm64,android-x64 --split-per-abi
```
```sh
Explanation:

This command builds separate APKs for different architectures (arm, arm64, x64).

--split-per-abi ensures each APK is optimized for a specific CPU architecture, reducing APK size.

It is useful when deploying to Play Store, as users download only the compatible APK for their device.
```

### Gradle Issues Commands
```sh
cd android && ./gradlew clean        # Cleans the Gradle build cache
cd android && ./gradlew build         # Builds the Android project
cd android && ./gradlew dependencies  # Lists dependencies and resolves conflicts
cd android && ./gradlew --stop        # Stops all Gradle daemons
cd android && ./gradlew --refresh-dependencies  # Forces dependency refresh
cd android && ./gradlew clean assembleDebug  # This compiles the app in debug mode

```
### Basic Git Commands
```sh
git init # Initializes a new Git repository in the current directory.
git clone <repo_url> #Clones an existing Git repository from a remote source.
git status # Shows the current status of your working directory (changes, staged files, etc.).
git add <file> # Adds a specific file to the staging area.
git add . # Adds all changes in the current directory to the staging area.
git commit -m "message" # Commits the staged changes with a descriptive message.
git push origin <branch> # Pushes committed changes to the remote repository.
git pull origin <branch> # Fetches and merges changes from the remote repository.
git branch # Lists all branches in the repository.
git checkout <branch> # Switches to a different branch.
git checkout -b <new_branch> # Creates and switches to a new branch.
git merge <branch> # Merges the specified branch into the current branch.
git log # Displays the commit history.
git diff # Shows differences between changes in working directory and last commit.
git reset --hard <commit> # Resets the repository to a specific commit (removes all changes).
git stash # Temporarily saves changes without committing.
git stash pop # Restores saved changes from stash.
git rebase <branch> # Reapplies commits from the current branch on top of another branch.
git tag <tag_name> # Creates a tag for a specific commit (useful for releases).
git remote -v # Lists remote repositories linked to your project.
git fetch # Fetches changes from the remote without merging them.
git show <commit> # Displays details about a specific commit.
git rm <file> # Removes a file from the repository.
git revert <commit> # Creates a new commit that undoes the changes of a specific commit.
git cherry-pick <commit> # Applies a specific commit from another branch.

```


---

## 2. Important Packages

### State Management
- `provider` - A recommended approach for state management.
- `riverpod` - A powerful alternative to provider.
- `bloc` - Business logic component for structured state management.
- `get` - Simple and efficient state management solution.

### Networking
- `http` - Simple package for REST API requests.
- `dio` - A more advanced HTTP client with interceptors and error handling.
- `graphql_flutter` - For integrating GraphQL in Flutter.

### Database and Storage
- `sqflite` - SQLite plugin for local database storage.
- `hive` - Lightweight and fast key-value database.
- `shared_preferences` - Store small amounts of data persistently.
- `firebase_core` & `cloud_firestore` - Firebase Firestore for cloud database storage.

### UI & Design
- `flutter_svg` - For SVG image support.
- `cached_network_image` - Caches images for performance.
- `lottie` - Adds Lottie animations.
- `flutter_screenutil` - Helps with responsive UI design.

### Authentication
- `firebase_auth` - Firebase authentication support.
- `google_sign_in` - Google login integration.
- `flutter_facebook_auth` - Facebook login integration.
- `sign_in_with_apple` - Apple login support.

### Others
- `flutter_local_notifications` - Local push notifications.
- `geolocator` - Fetch device location.
- `url_launcher` - Open URLs, emails, or phone calls.
- `flutter_native_splash` - Custom splash screens.

---

## 3. Common Issues & Solutions

### Issue: App Stuck on White Screen
**Solution:** Ensure `main()` method calls `WidgetsFlutterBinding.ensureInitialized()` before running `runApp()`.
```dart
void main() {
  WidgetsFlutterBinding.ensureInitialized();
  runApp(MyApp());
}
```

### Issue: Dependencies Not Found
**Solution:** Run `flutter pub get` to fetch the required dependencies.

### Issue: Emulator Not Detecting Changes
**Solution:** Try running `flutter clean` followed by `flutter run`.

### Issue: Gradle Build Failing in Android
**Solution:**
- Ensure `android/gradle/wrapper/gradle-wrapper.properties` has a compatible Gradle version.
- Run `flutter doctor` and resolve any missing dependencies.

### Issue: iOS Build Failing
**Solution:**
- Ensure Xcode is installed and updated.
- Run `pod install` inside `ios/` directory.

### Issue: Firebase Not Working on iOS
**Solution:**
- Make sure `GoogleService-Info.plist` is correctly placed in `ios/Runner/`.
- Add `use_frameworks!` in the `Podfile` and run `pod install`.

### Issue: PlatformException in Camera or Location Plugins
**Solution:**
- Add required permissions in `AndroidManifest.xml` (for Android) and `Info.plist` (for iOS).

## Common Signing Issues & Solutions

### Issue: Keystore Not Found
**Solution:** Ensure that the `keystore.jks` file exists and the path is correct in `key.properties`.

### Issue: Incorrect Keystore Password
**Solution:** Double-check the `storePassword` and `keyPassword` in `key.properties` and ensure they match the actual keystore.

### Issue: Missing Signing Config in `build.gradle`
**Solution:**
```gradle
android {
    signingConfigs {
        release {
            storeFile file("../keystore.jks")
            storePassword "your_password"
            keyAlias "your_key_alias"
            keyPassword "your_key_password"
        }
    }
}
```

### Issue: Invalid Key Alias
**Solution:** Run the following command to list key aliases in your keystore:
```sh
keytool -list -v -keystore your_keystore.jks
```

### Issue: `SHA1` or `SHA256` Mismatch
**Solution:** Get the correct fingerprint using:
```sh
keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android
```

### Issue: Play Store Rejecting APK Due to Signing
**Solution:** Ensure your app is signed with the correct `upload key` and matches the Play Console key.

### Issue: `jarsigner` Verification Failed
**Solution:** Run the following command to verify the signature:
```sh
jarsigner -verify -verbose -certs your_app.apk
```



```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

```xml
<key>NSCameraUsageDescription</key>
<string>We need camera access</string>
<key>NSLocationWhenInUseUsageDescription</key>
<string>We need your location</string>
```

---

## 4. Best Practices in Flutter Development
- Use **const** for widgets that don’t change to improve performance.
- Organize code into **separate files** for readability and maintainability.
- Use **Dart extension methods** to simplify repetitive tasks.
- Apply **Flutter hooks** to manage state efficiently.
- Optimize app size by using **Flutter WebP images** instead of PNGs.
- Prefer **lazy loading** for large lists to improve performance.
- Write unit and widget tests using **flutter_test** package.

---

## Conclusion
Flutter is an ever-evolving framework, and mastering its commands, packages, and debugging techniques will help you build efficient, scalable applications. Keep experimenting and stay updated with new features!

