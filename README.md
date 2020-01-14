# VerifyKit

[![Platform](https://img.shields.io/badge/Platforms-ANDROID-4E4E4E.svg?colorA=28a745)](#installation)
[![](https://jitpack.io/v/org.bitbucket.verifykit/verifykit-android.svg)](https://jitpack.io/#org.bitbucket.verifykit/verifykit-android)
[![API](https://img.shields.io/badge/API-14%2B-green.svg?style=flat)](https://android-arsenal.com/api?level=14)
![License](https://img.shields.io/badge/License-MIT-red.svg)

VerifyKit is the next generation phone number validation system. Users can easily verify their phone numbers without the need of entering phone number or a pin code.
## Installation

Add it to your app build.gradle at the end of repositories:

```groovy
implementation 'org.bitbucket.verifykit:verifykit-android:${lastVersion}'
```

Add it to your root build.gradle at the end of repositories:

```groovy
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
```kotlin
  val theme = VerifyKitTheme(
            backgroundColor = Color.WHITE,
            toolbarTitle = getString(R.string.app_name)
        )
        VerifyKit.init(
            this,
            VerifyKitOptions(
                isLogEnabled = true,
                verifyKitTheme = theme
            )
        )

```

You can call VerifyKit.startVerification(this) method from your Activity or Fragment. 

SampleActivity.kt
```kotlin
 VerifyKit.startVerification(this, object : VerifyCompleteListener {
            override fun onSuccess(sessionId: String) {
              // TODO operate SUCCESS process
            }

            override fun onFail(error: VerifyKitError) {
              // TODO operate FAIL process
            }
        })
```

You can get the result via VerifyCompleteListener interface from your activity or fragment.
```kotlin
  override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        VerifyKit.onActivityResult(requestCode, resultCode, data)
    }
```


There may be a case when user chooses a third party messaging app for validation, sends a message, but doesn't return to main app and kills it. In that case, that user is verified with VerifyKit but the main app doesn't know it yet.

To fix this, we have a method to check interrupted session status.


```kotlin
VerifyKit.checkInterruptedSession(applicationContext, object : VerifyCompleteListener {
            override fun onSuccess(sessionId: String) {
                // sessionId
            }

            override fun onFail(error: VerifyKitError) {
                // error
            }
        })
```


## AndroidManifest

Open the /app/manifest/AndroidManifest.xml file.

Add the following meta-data elements, an activity for VerifyKit and intent filter for DeepLink inside your application element:

```xml
<meta-data
            android:name="com.verifykit.sdk.clientKey"
            android:value="your_verifykit_client_key" />
<meta-data
            android:name="com.verifykit.sdk.clientSecret"
            android:value="your_verifykit_client_secret" />
<activity
            android:name="com.verifykit.sdk.ui.VerificationActivity"
            android:launchMode="singleInstance"
            android:screenOrientation="portrait">
	<intent-filter>
		<action android:name="android.intent.action.VIEW" />
		<category android:name="android.intent.category.DEFAULT" />
		<category android:name="android.intent.category.BROWSABLE" />
		<!--This code is optional-->
		<data
                    android:host="your_deep_link_url"
                    android:pathPattern="your_deep_link_pattern"
                    android:scheme="https" />
		<!--This code is optional-->
	</intent-filter>
</activity>
  
```




## Author

VerifyKit is owned and maintained by 
[VerifyKit DevTeam.](mailto:sdk@verifykit.com)


## License
[MIT](https://opensource.org/licenses/MIT)

Copyright (c) 2019-2020 VerifyKit. [https://verifykit.com](http://verifykit.com)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
