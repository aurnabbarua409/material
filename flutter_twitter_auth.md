# Steps for twitter auth

<ol>
<li>Add firebase to your project.</li>
<li>Create a developer account in twitter and create an app.</li>
<li>Add twitter in firebase</li>
<li> Run this to install package </li>

```bash
flutter pub add twitter_login
```
<li>Then, write this code in a mehod</li>

```dart
try {
      final twitterLogin = TwitterLogin(
        apiKey: 'xYM1UuCQGOtbYNyJQmn839Iea',
        apiSecretKey: 'mKJGWhkpuOEyDpVAqhhzvvnl7PD1mzpKZj2wWl7Rff8NrBPxFE',
        redirectURI: 'myapp://',
      );

      // Trigger the sign-in flow
      final authResult = await twitterLogin.login();

      // Create a credential from the access token
      final twitterAuthCredential = TwitterAuthProvider.credential(
        accessToken: authResult.authToken!,
        secret: authResult.authTokenSecret!,
      );

      // Once signed in, return the UserCredential
      final userCred = await FirebaseAuth.instance.signInWithCredential(
        twitterAuthCredential,
      );
      print(userCred);
      print(userCred.user?.email ?? "Nothing is found");
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text(userCred.user.toString() ?? "Nothing")),
      );
    } catch (e) {
      print("got some error: $e");
    }
```
<li>Then in `android\app\src\main\AndroidManifest.xml` file</li>

```xml
<intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <!-- Accepts URIs that begin with "example://gizmos” -->
    <!-- Registered Callback URLs in TwitterApp -->
    <data android:scheme="myapp"
            /> <!-- host is option -->
</intent-filter>
```
</ol>
