# Flutter CI/CD Demo

A hands-on Flutter project created to implement and demonstrate a complete **CI/CD pipeline** using GitHub Actions, Fastlane, and Firebase App Distribution.

The project focuses on automating the workflow from **code push → validation → release build → tester distribution**.

## 🚀 Pipeline Overview

```text
                    Git Push
                       │
                       ▼
              ┌─────────────────┐
              │ GitHub Actions  │
              └────────┬────────┘
                       │
              ┌────────▼────────┐
              │       CI        │
              ├─────────────────┤
              │ flutter pub get │
              │ flutter analyze │
              │ flutter test    │
              │ build APK       │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │       CD        │
              ├─────────────────┤
              │ Ruby + Bundler  │
              │ Fastlane        │
              │ Build APK       │
              └────────┬────────┘
                       │
                       ▼
          Firebase App Distribution
                       │
                       ▼
                    Testers
```

## 🧩 Continuous Integration

CI is implemented with **GitHub Actions** and runs automatically on pushes and pull requests targeting `main`.

The CI workflow:

* Installs Flutter dependencies
* Runs static analysis with `flutter analyze`
* Runs automated tests with `flutter test`
* Builds a release APK

Workflow:

```text
.github/workflows/flutter_ci.yml
```

## 🚢 Continuous Delivery

CD is implemented using **Fastlane** and **Firebase App Distribution**.

On every push to `main`, the CD workflow:

1. Sets up Java, Flutter, and Ruby
2. Installs Ruby dependencies with Bundler
3. Executes the Fastlane `firebase_distribution` lane
4. Builds the release APK
5. Distributes the APK through Firebase App Distribution

Workflow:

```text
.github/workflows/firebase_distribution.yml
```

## ⚡ Fastlane

Fastlane automates the Android release and distribution process.

The project contains a dedicated lane:

```ruby
firebase_distribution
```

The lane handles the release build and Firebase App Distribution upload.

Fastlane configuration:

```text
android/fastlane/
├── Appfile
├── Fastfile
└── Pluginfile
```

## 🔐 Secrets Management

Sensitive authentication data is handled through **GitHub Actions Secrets** instead of being stored in the repository.

The Firebase CLI token is provided to the workflow through:

```text
FIREBASE_CLI_TOKEN
```

The secret is injected at runtime and accessed by Fastlane through an environment variable.

## 🛠️ Tech Stack

| Technology                | Purpose                    |
| ------------------------- | -------------------------- |
| Flutter                   | Application framework      |
| Dart                      | Programming language       |
| Git & GitHub              | Version control            |
| GitHub Actions            | CI/CD automation           |
| Fastlane                  | Build & release automation |
| Ruby                      | Fastlane runtime           |
| Bundler                   | Ruby dependency management |
| Firebase App Distribution | Tester distribution        |

## 📁 Project Structure

```text
flutter-ci-cd-demo/
│
├── .github/
│   └── workflows/
│       ├── flutter_ci.yml
│       └── firebase_distribution.yml
│
├── android/
│   ├── fastlane/
│   │   ├── Appfile
│   │   ├── Fastfile
│   │   └── Pluginfile
│   ├── Gemfile
│   └── Gemfile.lock
│
├── ios/
├── lib/
├── test/
├── pubspec.yaml
└── README.md
```

## 🎯 Key Takeaways

This project provided practical experience with:

* Building CI workflows for Flutter
* Automating testing and release builds
* Integrating Fastlane with a Flutter Android project
* Automating APK distribution with Firebase App Distribution
* Managing Ruby dependencies with Bundler
* Configuring GitHub Actions workflows
* Managing CI/CD secrets securely
* Separating Continuous Integration from Continuous Delivery

## ✅ Status

**CI/CD pipeline implemented and verified successfully.**

A push to `main` can trigger automated validation, release building, and Firebase App Distribution without manually building and uploading the APK.
