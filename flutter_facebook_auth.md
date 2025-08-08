# facebook_auth

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

# Steps for Facebook Auth:
<li>Go to https://developers.facebook.com/docs/facebook-login/android/?locale=en&lsrc=lb </li>

<li>Generate file:  android\app\src\main\res\values\strings.xml </li>

<li>write these text in the Strings.xml file: </li>

```xml
<resources>
     <string name="app_name">myapp1</string>
     <string name="facebook_app_id">1685541038816554</string>
     <string name="fb_login_protocol_scheme">fb1685541038816554</string>
     <string name="facebook_client_token">19c8e7184e56a268397d5d0be1d22268</string>
</resources> 
```
<li>open this file: /android/app/src/main/AndroidManifest.xml </li>
<li>In AndroidManifest.xml file, in application write: </li>

```xml
<meta-data android:name="com.facebook.sdk.ApplicationId" android:value="@string/facebook_app_id"/>
<meta-data android:name="com.facebook.sdk.ClientToken" android:value="@string/facebook_client_token"/>
```
then in manifest: 

```xml
<queries>
     <provider android:authorities="com.facebook.katana.provider.PlatformProvider" />
</queries>
```
<li> then create a method and write this: </li>

```dart
final LoginResult result = await FacebookAuth.instance
        .login(); // by default we request the email and the public profile
    // or FacebookAuth.i.login()
    if (result.status == LoginStatus.success) {
      // you are logged
      final AccessToken accessToken = result.accessToken!;
      final userData = await FacebookAuth.i.getUserData(
        fields: "name,email,picture.width(200),birthday,friends,gender,link",
      );
      print(userData);
    } else {
      print(result.status);
      print(result.message);
    }
```
