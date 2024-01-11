# BetterRoaming IOS Package

### Installation

#### XCode

* From file menu select `File` -> `Add Package Dependencies...`
![add-package.png](docs%2Fscreenshots%2Fadd-package.png)
* Enter https://github.com/Truphone/betterroaming-ios-sdk in the search field`
![add-package.png](docs%2Fscreenshots%2Finstall-package.png)
* Select `ebtterroaming-ios-sdk` package
* Click `Add Package` button


### Usage

#### Import the package
```swift
import BetterRoamingSdk

// ...

var manager = BetterRomaingManager()
```

#### Check eSim support
```swift
let supported: Bool = await manager.checkEsimSupport()
```

#### Generate and download an eSim
```swift
let body = [
    "subscriber": [
        "email": "...",
        "first_name": "...",
        "last_name": "...",
        "country_of_residence": "GB"
    ],
    "device": [
        "operating_system": "ios"
    ],
    "tenant": "...",
    "externalID": "...",
    "activation_token": "..."
]

let result: BRInstallEsimResult = try await manager.generateESimAndDownload(body: body)

/**
    Result status can be 4 different values 
     - .unknwon -> user probably cancelled or something went wrong
     - .fail -> installation failed
     - .success -> installation succeeded (you should check result.iccid)
     - .cancel -> user cancelled the installation (ios 17 or more)
*/
```

#### Open contact page
```swift
try await manager.openContactPage(params: ["tenant_id": "..."])
```

#### Open status page
```swift
try await manager.openStatusPage(iccid: iccid)
```
