### Avaamo Embed SDK - Instructions

###### Before you begin
> 1. You should have the SDK 'aar' downloaded.
> 2. You should have your `parner_uuid` and `secret` available.


###### Setup
1. Create an android application with Android Studio.
2. To import the Avaamo Embed SDK, follow these steps.
  1. Go to `File: New Module`.
  2. Choose `Import JAR/AAR package`.

  ![](/images/add-aar-dependency.png)
  3. On the next screen, for the File name field, navigate to the SDK aar file, and select it's path.
  4. Leave the sub-project name (avaamo) as is.
  5. Click on the project, and `Open Module Settings`. In the `Dependencies` tab, click on the `+` button and Add `avaamo` as a module dependency.
  6. Add these repositories to your application's `build.gradle` file.
  ```
      repositories {
         maven { url 'https://repo.commonsware.com.s3.amazonaws.com' }
         maven { url 'https://maven.fabric.io/public' }
         mavenCentral()
      }
  ```
  7. Add the following dependencies to your application's 'build.gradle' file.
  8. In your `app/src/main/AndroidManifest.xml` file, set the theme of your application to `@style/Avaamo` theme, and add `tools:replace=”android:theme, android:icon`. Also add the tools namespace to the manifest tag.
  ```
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
  9. In your app/src/main/AndroidManifest.xml file, include PartnerLoginActivity and meta-data tag.
  10. Add these four permissions to your app/src/main/AndroidManifest.xml file inside the <manifest> element.
  11. Setup is done!.


###### Initializing the app
1. Initialize the Avaamo embed app with 2 mandatory parameters. (This code sample uses sample data. Please use your `partner_uuid` and create the `user_jwt_token` as mentioned below.
2. That is it!. Avaamo is now embedded in your app. When launched Avaamo embed app shows up like this.
3. To initialize the messaging service in the background
4. Colors
5. Open Avaamo app with
6. Listening for Avaamo events
