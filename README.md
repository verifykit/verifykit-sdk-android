# VerifyKit

[![Platform](https://img.shields.io/badge/Platforms-ANDROID-4E4E4E.svg?colorA=28a745)](#installation)
[![](https://jitpack.io/v/org.bitbucket.verifykit/verifykit-android.svg)](https://jitpack.io/#org.bitbucket.verifykit/verifykit-android)
[![API](https://img.shields.io/badge/API-14%2B-green.svg?style=flat)](https://android-arsenal.com/api?level=14)


VerifyKit is the next generation phone number validation system. Users can easily verify their phone numbers without the need of entering phone number or a pin code.
## Installation

Add it to your app build.gradle at the end of repositories:

```bash
implementation 'org.bitbucket.verifykit:verifykit-android:${lastVersion}'
```

Add it to your root build.gradle at the end of repositories:

```bash
allprojects {
  repositories {
    ...
    maven { url 'https://jitpack.io' }
  }
}
```

## Requirements

Minimum SDK Version is  api 14


## Usage

In your Application file you should initialize VerifyKit. VerifyKit.init() method needs VerifyKitOptions object. 

Application.kt
```
  VerifyKit.init(
            VerifyKitOptions("YOUR API KEY HERE", // Receive from dashboard
                isLogEnabled = true,  //  default true
                verifyKitEnvironment = VerifyKitEnvironment.DEBUG // default DEBUG
            )
        )

```

You can call VerifyKit.startVerification(this) method from your Activity or Fragment. 

SampleActivity.kt
```
 VerifyKit.startVerification(this)
```

You can get the result via VerifyCompleteListener interface from your activity or fragment.
```
  override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        VerifyKit.onActivityResult(requestCode, resultCode, data, object : VerifyCompleteListener {
            override fun onCompleteLogin(sessionId: String) {
              // TODO operate SUCCESS process
            }

            override fun onFail(error: VerifyKitError) {
              // TODO operate FAIL process
            }
        })
    }
```

## Notes:

Before your app release, please change the VerifyKitEnvironment to 'release' instead of 'debug'.

## Author

VerifyKit is owned and maintained by 
[VerifyKit DevTeam.](mailto:sdk@verifykit.com)


## License
[MIT](https://opensource.org/licenses/MIT)

Copyright (c) 2019-2020 VerifyKit. [http://verifykit.com](http://verifykit.com)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
