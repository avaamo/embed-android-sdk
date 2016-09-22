### Avaamo Embed SDK


##### [Prerequisite](#prerequisite)
##### [Android Studio setup](#setup)
##### [Initializing the app](#initializing-the-app-1)
### [Customizations](#customizations)
###### [Initialize Avaamo in the background](#initialize-avaamo-in-the-background-1)
###### [Change color theme](#change-color-theme-1)
###### [Open Avaamo with a deeplink](#open-avaamo-with-a-deeplink-1)
###### [Listening for Avaamo events](#listening-for-avaamo-events-1)
###### [Access badge count](#access-badge-count-1)



#### Prerequisite
> 1. You should have the SDK 'aar' downloaded.
> 2. You should have your `parner_uuid` and `secret` available.

Please contact your Avaamo account manager to request these details.


#### Setup
1. Create an android application with Android Studio.
2. To import the Avaamo Embed SDK, follow these steps.
  1. Go to `File: New Module`.
  2. Choose `Import JAR/AAR package`.
  ![](https://raw.githubusercontent.com/avaamo/embed-android-sdk/master/images/add-aar-depencency.png)
  3. On the next screen, for the File name field, navigate to the SDK aar file, and select it's path.
  ![](https://raw.githubusercontent.com/avaamo/embed-android-sdk/master/images/add-module.png)
  ![](https://raw.githubusercontent.com/avaamo/embed-android-sdk/master/images/add-module-2.png)
  ![](https://raw.githubusercontent.com/avaamo/embed-android-sdk/master/images/add-module-3.png)
  4. Leave the sub-project name (avaamo) as is.
  5. Click on the project, and `Open Module Settings`. In the `Dependencies` tab, click on the `+` button and Add `avaamo` as a module dependency.
  6. Add these repositories to your application's `build.gradle` file.
  ```
  repositories {
     maven { url 'https://s3.amazonaws.com/repo.commonsware.com' }
     maven { url 'https://maven.fabric.io/public' }
     mavenCentral()
  }
  ```
  7. Add the following dependencies to your application's 'build.gradle' file.
  ```
    provided 'org.parceler:parceler:0.2.10'
    compile('com.crashlytics.sdk.android:crashlytics:2.5.5@aar') {
      transitive = true;
    }
    compile 'com.android.support:support-v13:23.4.0'
    compile 'com.android.support:appcompat-v7:23.4.0'
    compile 'com.android.support:design:23.4.0'
    compile 'com.android.support:cardview-v7:23.4.0'
    compile 'com.android.support:recyclerview-v7:23.4.0'
    compile 'com.android.support:multidex:1.0.1'

    compile 'com.mobsandgeeks:android-saripaar:1.0.2'
    compile 'com.jakewharton:butterknife:6.0.0'
    compile 'uk.co.ribot:easyadapter:1.2.0'
    compile 'com.google.android.gms:play-services-base:9.0.0'
    compile 'com.google.android.gms:play-services-maps:9.0.0'
    compile 'com.google.android.gms:play-services-location:9.0.0'
    compile 'com.google.android.gms:play-services-gcm:9.0.0'
    compile 'de.greenrobot:eventbus:2.2.1'
    compile 'com.squareup.phrase:phrase:1.0.3'
    compile 'com.squareup.picasso:picasso:2.5.2'
    compile 'com.squareup.okhttp:okhttp:2.7.2'
    compile 'com.squareup.okio:okio:1.6.0'
    compile 'com.squareup.okhttp:okhttp-urlconnection:2.7.2'
    compile 'com.squareup.retrofit:retrofit:1.9.0'
    compile ('com.squareup.retrofit:converter-simplexml:1.9.0') {
      exclude group: 'xpp3', module: 'xpp3'
      exclude group: 'stax', module: 'stax-api'
      exclude group: 'stax', module: 'stax'
    }
    compile 'com.j256.ormlite:ormlite-android:4.48'
    compile 'com.j256.ormlite:ormlite-core:4.48'
    compile 'com.googlecode.libphonenumber:libphonenumber:6.2'
    compile 'com.google.code.gson:gson:2.4'
    compile 'com.google.guava:guava:18.0'
    compile 'com.jakewharton.timber:timber:2.4.0'
    compile 'com.birbit:android-priority-jobqueue:2.0.0'
    compile 'com.commonsware.cwac:wakeful:1.1.0'
    compile 'org.parceler:parceler-api:0.2.10'
    compile 'com.github.johnkil.android-progressfragment:progressfragment-native:1.4.0'
    compile 'me.leolin:ShortcutBadger:1.1.3@aar'
    compile 'com.commit451:PhotoView:1.2.5'
    compile 'net.frakbot:jumpingbeans:1.2.0'
    compile 'com.parse.bolts:bolts-tasks:1.3.0'
    compile 'com.mobsandgeeks:adapter-kit:0.5.3'
    compile 'com.splitwise:tokenautocomplete:2.0.2@aar'
    compile 'com.github.bumptech.glide:glide:3.7.0'
    compile 'net.yslibrary.keyboardvisibilityevent:keyboardvisibilityevent:1.0.0'
    compile 'de.hdodenhof:circleimageview:2.0.0'
    compile 'com.kbeanie:multipicker:1.1.0@aar'
    compile 'com.github.gcacace:signature-pad:1.2.0'
    compile 'com.fasterxml.jackson.core:jackson-databind:2.5.3'
    compile 'com.squareup.okhttp:okhttp-ws:2.7.2'
  ```
  ![](https://raw.githubusercontent.com/avaamo/embed-android-sdk/master/images/add-dependencies.png)
  > These dependences get downloaded in about 5 minutes on a 1 MBPS speed internet connection.

  8. In your `app/src/main/AndroidManifest.xml` file, set the theme of your application to `@style/Avaamo` theme, and add `tools:replace=”android:theme, android:icon`. Also add the tools namespace to the manifest tag.
  ```xml
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:tools="http://schemas.android.com/tools"
       package="your_package_name">

    <application
       android:allowBackup="true"
       android:icon="@drawable/ic_launcher"
       android:label="@string/app_name"
       android:supportsRtl="true"
       android:theme="@style/Avaamo"
       tools:replace="android:theme, android:icon">
  ```

  9. Add these four permissions to your app/src/main/AndroidManifest.xml file inside the <manifest> element.
  ```xml
   <uses-permission android:name="android.permission.READ_CONTACTS" />
   <uses-permission android:name="android.permission.WRITE_CONTACTS" />
   <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
   <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
  ```
  10. Add the following snippets to your application's build.gradle file. (In the default config section)
  ```
    defaultConfig {
      ...
      multiDexEnabled true 
      ...
  ```
  11. Configure Android Studio to use more memory.
  ```
  dexOptions {
        incremental true
        preDexLibraries = true
        javaMaxHeapSize "4g"
    }
  ```
  12. Library conflicts configuration
  ```
    packagingOptions {
        exclude 'META-INF/LICENSE'
        exclude 'META-INF/NOTICE'
    }
  ```
  13. Setup is done!.


#### Initializing the app
1. Initialize the Avaamo embed app with 2 mandatory parameters. (This code sample uses sample data. Please use your `partner_uuid` and create the `user_jwt_token` as mentioned below.
```java
  Intent intent = new Intent(MainActivity.this, PartnerLoginActivity.class);
  // Dummy data
  intent.putExtra("partner_uuid","2671a7f3-4fea-49ae-835a-95771bbe5ffd");
  intent.putExtra("user_jwt_token", "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1dWlkIjoiMTIzNDU2Nzg5MCIsImZpcnN0X25hbWUiOiJKb2huIiwibGFzdF9uYW1lIjoiU21pdGgiLCJlbWFpbCI6ImpzbWl0aEBhdmFhbW8uY29tIiwicGhvbmUiOiIrMTIzNDU2Nzg5IiwiY3VzdG9tMSI6InZhbHVlMSJ9.XDk8boUHwd3fotdDxlmP3cHPthwTw5Y57mXLyc6cc9I");
  startActivity(intent);
```
**Description of parameters**

Name | Description | Required
---- | ----------- | --------
partner_uuid | This will identify your company and the embed.  This is unique to each embed. If you are embedding Avaamo in an another app, please request a new partner_uuid | Yes
user_jwt_token | This is the JWT encoded string. This JWT encoded string has to include 3 mandatory user identification parameters. `uuid`, `first_name`, `last_name`. <br/><br/>Add one or more of these optional parameters. `email`, `phone`. <br/><br/>You can also include other custom properties which will come handy when creating broadcast lists within Avaamo Dashboard. | Yes

> `user_jwt_token` is a JSON Web Token encoded string of the user data. User data needs to be in the JSON format and needs to encoded using HS256 algorithm and embed_secret provided to you by Avaamo. You can find JWT library of your choice and a demo UI to generate the tokens at https://jwt.io/

**Example user JSON**
```json
{
  "uuid": "h89dc70-46a8-4f5b-aa38-4d016a31234",
  "first_name": "John Doe",
  "last_name": "John Doe",
  "email": "john.doe@company.com",
  "phone": "+16503835760",
  "custom_attribute1": "value1",
  "custom_attribute2": "value2"
}
```

Ensure each embed user has a different `uuid`. In case a uuid does not exist, you could use email as the `uuid`. For example

```json
{
  "uuid": "john.doe@company.com",
  "first_name": "John Doe",
  "last_name": "John Doe",
  "email": "john.doe@company.com",
  "phone": "+16503835760",
  "custom_attribute1": "value1",
  "custom_attribute2": "value2"
}
```

Javascript: [Code Samples](https://github.com/avaamo/embed-android-sdk/blob/master/Javascript.md)

Java: [Code Samples](https://github.com/avaamo/embed-android-sdk/blob/master/Java.md)


2. That is it!. Avaamo is now embedded in your app. When launched Avaamo embed app shows up like this.


## Customizations
##### Initialize Avaamo in the background
To start receiving avaamo notifications even before a user tap on a button or a UI elment to launch the Avaamo embed app.

```java
  AvaamoSDK sdk = new AvaamoSDK(this);
  if (sdk.isInitialized()) {
     sdk.init();
  }
```

##### Change color theme
```xml
  <style name="Avaamo.ActionBarStyle">
     <item name="background">yourcolorcode</item>
  </style>
```
Specify your app's base colors
```xml
<resources>
    <color name="colorPrimary">#3F51B5</color>
    <color name="colorPrimaryDark">#303F9F</color>
    <color name="colorAccent">#FF4081</color>
</resources>
```
Set the base colors to your theme
```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    <!-- Customize your theme here. -->
    <item name="colorPrimary">@color/colorPrimary</item>
    <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
    <item name="colorAccent">@color/colorAccent</item>
</style>
```

##### Open Avaamo with a deeplink
a. While initializing the library
```java
intent.putExtra("deeplink" ,<deeplink url>)
```
b. Any time after the library is initialized
```java
AvaamoUtils.openDeeplink(<deeplink url>)
```

This [ page ](https://github.com/avaamo/java/wiki/Deep-Links) has more information about all the available deeplinks

##### Enable data syncing
```java
AvaamoSDK sdk = new AvaamoSDK(this);
sdk.enableSyncConversations();
sdk.enableSyncContacts();
sdk.enableSyncCompanyContacts();
sdk.enableSyncBroadcasts();
sdk.enableSyncBots();
```

##### Listening for Avaamo events
  - For a new message
```xml
    <receiver android:name="AvaamoBroadcastReceiver">
     <intent-filter>
         <action android:name="com.avaamo.action.NOTIFY_MESSAGE"/>
     </intent-filter>
    </receiver>
```
```java
    @Override
    public void onReceive(Context context, Intent intent) {
       String action = intent.getAction();
       if (action.equals("com.avaamo.action.NOTIFY_MESSAGE")) {
           int badge = intent.getIntExtra("badge", 0);
       }
    }
```
##### Access badge count
```java
  AvaamoUtils.getBadge()
```

##### Enable Google maps
After signing up for Google Maps for android and setting up an API key, add this meta-data tag in the AndroidManifest.xml file of your app, just before the end of application tag.
```
<meta-data tools:replace="android:value"
    android:name="com.google.android.maps.v2.API_KEY"
    android:value="your-api-key" />
```
