# NeuroLoop

Neuroscience-backed micro-habit tracker. Flutter + Firebase (Auth, Firestore) + Provider.

## Setup

1. `flutter create --platforms=android,ios .` (generates the native folders; keeps `lib/`, `pubspec.yaml`)
2. Create a Firebase project, then register your Android/iOS apps.
   - Android: put `google-services.json` in `android/app/` and apply the
     `com.google.gms.google-services` Gradle plugin. Set `minSdkVersion` to 23 or higher.
   - iOS: add `GoogleService-Info.plist` via Xcode. Deployment target iOS 13+.
   - Or run `flutterfire configure` and pass `DefaultFirebaseOptions.currentPlatform`
     to `Firebase.initializeApp()` in `lib/main.dart`.
3. Firebase console -> Authentication -> enable **Anonymous** and **Email/Password**.
4. Firebase console -> Firestore -> create a database, then publish `firestore.rules`.
5. `flutter pub get && flutter test && flutter run`

## Elastic Consistency

Rolling 30-day score: `(completed + 0.5 * forgiven) / eligible days`.
An isolated miss (done the day before, done or still possible the day after)
is "forgiven" at half credit. Two misses in a row count in full. A single miss can never reset the score.
See `lib/domain/elastic_consistency.dart` and `test/elastic_consistency_test.dart`.
