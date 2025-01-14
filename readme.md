# Mapbox Speech

Mapbox Speech connects your iOS, macOS, tvOS, or watchOS application to the Mapbox Voice API. Take turn instructions from the [Mapbox Directions API](https://www.mapbox.com/api-documentation/#directions) and read them aloud naturally in multiple languages. This library is specifically designed to work with [MapboxDirections.swift](https://github.com/mapbox/MapboxDirections.swift/) as part of the [Mapbox Navigation SDK for iOS](https://github.com/mapbox/mapbox-navigation-ios/).

This library is compatible with applications written in Swift. Version 2.0 was the last version of this library to support applications written in Objective-C or AppleScript.

## Getting started

Specify the following dependency in your [Carthage](https://github.com/Carthage/Carthage) Cartfile:

```cartfile
github "mapbox/mapbox-speech-swift" ~> 0.2
```

Or in your [CocoaPods](http://cocoapods.org/) Podfile:

```podspec
pod 'MapboxSpeech', '~> 0.2.0'
```

Or in your [Swift Package Manager](https://swift.org/package-manager/) Package.swift:

```swift
.package(url: "https://github.com/mapbox/mapbox-speech-swift.git", from: "0.2.0")
```

Then `import MapboxSpeech` or `@import MapboxSpeech;`.

## Usage

You’ll need a [Mapbox access token](https://www.mapbox.com/developers/api/#access-tokens) in order to use the API. If you’re already using the [Mapbox Maps SDK for iOS](https://www.mapbox.com/ios-sdk/) or [macOS SDK](https://mapbox.github.io/mapbox-gl-native/macos/), Mapbox Speech automatically recognizes your access token, as long as you’ve placed it in the `MGLMapboxAccessToken` key of your application’s Info.plist file.

### Basics

The main speech synthesis class is `SpeechSynthesizer`. Create a speech synthesizer object using your access token:

```swift
import MapboxSpeech

let speechSynthesizer = SpeechSynthesizer(accessToken: "<#your access token#>")
```

Alternatively, you can place your access token in the `MGLMapboxAccessToken` key of your application’s Info.plist file, then use the shared speech synthesizer object:

```swift
// main.swift
let speechSynthesizer = SpeechSynthesizer.shared
```

With the directions object in hand, construct a SpeechOptions or MBSpeechOptions object and pass it into the `SpeechSynthesizer.audioData(with:completionHandler:)` method.

```swift
// main.swift

let options = SpeechOptions(text: "hello, my name is Bobby")
speechSynthesizer.audioData(with: options) { (data: Data?, error: NSError?) in
    guard error == nil else {
        print("Error calculating directions: \(error!)")
        return
    }
    
    // Do something with the audio!
}
```
