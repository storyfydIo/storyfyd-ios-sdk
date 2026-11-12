# Storyfyd iOS SDK

Interactive stories for iOS apps. This repository only distributes the compiled SDK
(`StoryfydSDK.xcframework`) as a Swift package; it is updated automatically by the release
pipeline, so please do not open pull requests here.

- **Version**: 1.11.2
- **Minimum**: iOS 17.0, Xcode 16 or newer
- **UI**: SwiftUI (works in UIKit through `UIHostingController`)
- **Dependencies**: none

## Installation (Swift Package Manager)

In Xcode: **File > Add Package Dependencies...**, enter

```
https://github.com/storyfydIo/storyfyd-ios-sdk
```

and pick **Up to Next Major Version** from `1.11.2`. Add the `StoryfydSDK` library to your app
target.

In a `Package.swift`:

```swift
dependencies: [
    .package(url: "https://github.com/storyfydIo/storyfyd-ios-sdk", from: "1.11.2"),
],
targets: [
    .target(name: "MyApp", dependencies: [
        .product(name: "StoryfydSDK", package: "storyfyd-ios-sdk"),
    ]),
]
```

Swift Package Manager verifies the SHA-256 checksum of the downloaded framework against the one
in `Package.swift`, so a modified file is rejected.

## Quick start

```swift
import StoryfydSDK
import SwiftUI

@main
struct MyApp: App {
    init() {
        StoryfydSDK.configure(token: "YOUR_APP_TOKEN")
        // Optional: identify the visitor for personalised stories.
        StoryfydSDK.setUser(StoryfydUser(id: "user_123", email: "john@example.com"))
    }

    var body: some Scene {
        WindowGroup {
            StoryfydStoriesView()
        }
    }
}
```

The look of the widget and the player is set in the Storyfyd panel and reaches the app without an
update. `StoryfydStoriesView(configuration:theme:delegate:)` takes playback options, a forced
light or dark theme and a `StoryfydDelegate` for events and in-app links.

## Privacy

The framework ships a privacy manifest (`PrivacyInfo.xcprivacy`) that Xcode merges into your app's
privacy report.
