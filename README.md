# appsflyer_android_sdk

<img src="https://support.appsflyer.com/hc/article_attachments/115011109089/android.png"  width="250">


🛠 In order for us to provide optimal support, we would kindly ask you to submit any issues to support@appsflyer.com

*When submitting an issue please specify your AppsFlyer sign-up (account) email , your app ID , production steps, logs, code snippets and any additional relevant information.*

## Table of content

- [Adding the SDK to your project](#installation)
- [Initializing the SDK](#installation)
- [Getting started with Deeplinking](#deeplinking)
- [Guides](#guides)
- [API](#api) 
- [Sample App](#demo)
- [Known issues with integrating the SDK](#issues)
- [Testing installs](#testing)


## <a id="installation">📲Adding the SDK to your project

#### A. Using Gradle
1. Add the code below to Module-level `/app/build.gradle` before `dependencies`

```groovy
repositories {
    mavenCentral()
}
```
2. Add the latest version of *AppsFlyer SDK* as a dependency. <br />
   It is highly reccomeneded to also add the [*install referrer library*](https://developer.android.com/google/play/installreferrer/library).
   
```groovy
implementation 'com.appsflyer:af-android-sdk:5.+'
implementation 'com.android.installreferrer:installreferrer:1.0'
```
#### B. Manually adding the jar file

1. Download the [AF-Android-SDK.jar](https://s3-eu-west-1.amazonaws.com/download.appsflyer.com/Android/AF-Android-SDK.jar)
2. Add it to your project

## <a id="setup"> 🚀 Initializing the SDK
    
#### 1. AndroidManifest setup

Add the following [persmissions](https://developer.android.com/guide/topics/permissions/overview) to your [AndroidManifest.xml](https://developer.android.com/guide/topics/manifest/manifest-intro) file. <br />
The permissions should be added outside of the `<application>` tag.

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!-- Optional : -->
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```

#### 2. Init the SDK

It is highly reccomended to init the SDK in a [Application](https://developer.android.com/reference/android/app/Application) class. <br />
This will prevent the SDK from being destroyed thoughout the lifecycle of the app.
<br />

**Important: You must insert your apps [dev key](https://support.appsflyer.com/hc/en-us/articles/211719806-Global-app-settings-#sdk-dev-key). It is required for all apps.** 

If you do not already have a `Application` level class then you will need to create one. To do this, in the same folder as your `MainActivity.java`, create a new Java class. (in this example the class is called `AFApplication.java`). 

```java
import android.app.Application;
import android.util.Log;
import com.appsflyer.AppsFlyerConversionListener;
import com.appsflyer.AppsFlyerLib;
import com.appsflyer.AppsFlyerLibCore;
import java.util.Map;

public class AFApplication extends Application {
    private static final String AF_DEV_KEY = "Q2aM**********HJ56";

    @Override
    public void onCreate() {
        super.onCreate();

        AppsFlyerConversionListener conversionListener = new AppsFlyerConversionListener() {
            @Override
            public void onConversionDataSuccess(Map<String, Object> conversionData) {
                for (String attrName : conversionData.keySet()) {
                    Log.d(AppsFlyerLibCore.LOG_TAG, "attribute: " + attrName + " = " + conversionData.get(attrName));
                }
            }

            @Override
            public void onConversionDataFail(String s) {
            }

            @Override
            public void onAppOpenAttribution(Map<String, String> map) {
            }

            @Override
            public void onAttributionFailure(String s) {
            }
        };

        AppsFlyerLib.getInstance().init(AF_DEV_KEY, conversionListener, getApplicationContext());
        AppsFlyerLib.getInstance().startTracking(this);
    }
}
```

## <a id="deeplinking"> 🔗 Getting started with Deeplinking

...
    
    
 ## <a id="guides"> 📖 Guides

Great installation and setup guides can be viewed [here](/Docs/Guides.md).
- [init SDK Guide](/Docs/Guides.md#init-sdk)
- [Deeplinking Guide](/Docs/Guides.md#deeplinking)
- [Uninstall Guide](/Docs/Guides.md#track-app-uninstalls)


## <a id="api"> 📑 API
  
See the full API [here](https://support.appsflyer.com/hc/en-us/articles/207032126-AppsFlyer-SDK-Integration-Android#api-reference.

## <a id="demo"> 📱 Sample App
  
  Check out the sample app page [here](https://github.com/AppsFlyerSDK/AndroidSampleApp).
  
## <a id="issues"> 🔎 Known issues with integrating the SDK
    ...
    
## <a id="testing"> 🎯 Testing installs
    
1. [Whitelisting](https://support.appsflyer.com/hc/en-us/articles/207031996) your test device.
2. Simulating a non-organic install:
    a. Make sure your device is whitelisted.
    b. Generate a AppsFlyer [tracking link](https://support.appsflyer.com/hc/en-us/articles/207033836-Custom-link-management#intro).
    c. Uninstall the app from the device.
    d. Click on the link on the device.
    e. Install the app.
    f. You should see a non-organic install on your [dashboard](https://support.appsflyer.com/hc/en-us/articles/209680763-Dashboard-overview-explained).
    
    
    

