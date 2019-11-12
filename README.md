# AndroidSDKTest

<img src="https://support.appsflyer.com/hc/article_attachments/115011109089/android.png"  width="450">


🛠 In order for us to provide optimal support, we would kindly ask you to submit any issues to support@appsflyer.com

*When submitting an issue please specify your AppsFlyer sign-up (account) email , your app ID , production steps, logs, code snippets and any additional relevant information.*

## Table of content

- [Installation](#installation)
- [Guides](#guides)
- [API](#api) 
- [Demo](#demo)  


## <a id="installation">📲Installation

```
repositories {
    mavenCentral()
}
```

```
implementation 'com.appsflyer:af-android-sdk:5.+'
implementation 'com.android.installreferrer:installreferrer:1.0'
```

## <a id="setup"> 🚀 Setup

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!-- Optional : -->
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```

```java
import android.app.Application;
import android.util.Log;
import com.appsflyer.AppsFlyerConversionListener;
import com.appsflyer.AppsFlyerLib;
import com.appsflyer.AppsFlyerLibCore;
import java.util.Map;

public class AFApplication extends Application {
    private static final String AF_DEV_KEY = "K2aMGPY3SkC9WckYUgHJ99";

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


 ## <a id="guides"> 📖 Guides

Great installation and setup guides can be viewed [here](/Docs/Guides.md).
- [init SDK Guide](/Docs/Guides.md#init-sdk)
- [Deeplinking Guide](/Docs/Guides.md#deeplinking)
- [Uninstall Guide](/Docs/Guides.md#track-app-uninstalls)


## <a id="api"> 📑 API
  
See the full [API](/Docs/API.md) available for this plugin.


## <a id="demo"> 📱 Demo
  
  Check out the demo for this project [here](Docs/Guides.md#demo).
