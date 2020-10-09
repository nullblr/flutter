# "null" Mobile App

A Flutter project for null community.

1. `flutter create nullMobileApp`
2. `flutter devices`
3. `flutter run`
4. Edit `/lib/main.dart`
5. In `pubspec.yaml` file, add following dependencies

        http: ^0.12.2
        url_launcher: ^5.2.5

6. Generate flutter app icons by following the instructions [here](https://www.digitalocean.com/community/tutorials/flutter-app-icons)
7. Create a keystore
   
        keytool -genkey -v -keystore ~/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key

8. Follow deployment steps [here](https://flutter.dev/docs/deployment/android)
   
        flutter build appbundle --target-platform android-arm,android-arm64,android-x64,android-x86
        flutter build appbundle --target-platform android-arm,android-arm64,android-x64,android-x86 --obfuscate --split-debug-info=/nullMobileApp/bundle_debug_files

9. Fetch the Android App Bundle

        ls -l build/app/outputs/bundle/release/app.aab

10. Generate APKs from app bundle

        bundletool build-apks --bundle=build/app/outputs/bundle/release/app.aab --output=APKs/null.apks
        bundletool build-apks --bundle=build/app/outputs/bundle/release/app.aab --output=APKs/null.apks --ks=/home/mirage/Documents/android-pentesting/nullFlutterAPKSigning/key.jks --ks-key-alias=key --local-testing --overwrite
        ls -l APKs/null.apks

11. Generate a device-specific set of APKs

        bundletool build-apks --connected-device --bundle=build/app/outputs/bundle/release/app.aab --output=APKs/null_x86.apks --ks=/home/mirage/Documents/android-pentesting/nullFlutterAPKSigning/key.jks --ks-key-alias=key --local-testing --adb=/home/mirage/Android/Sdk/platform-tools/adb

12. Deploy APKs to a connected device

        bundletool install-apks --apks=APKs/null.apks --adb=/home/mirage/Android/Sdk/platform-tools/adb

13. Build an APK

        flutter build apk --split-per-abi
        ls -l build/app/outputs/flutter-apk/

## Troubleshooting

* `flutter channel stable`
* `flutter upgrade --force`
* `flutter pub cache repair`

## References

* https://dartpad.dev/
* https://flutter.dev/docs/cookbook
* https://dart.dev/guides/language/spec
* https://www.digitalocean.com/community/tutorials/flutter-app-icons
* https://flutter.dev/docs/deployment/android
* https://github.com/flutter/flutter/issues/49507
* https://github.com/google/bundletool
* https://developer.android.com/studio/command-line/bundletool
