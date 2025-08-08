# Steps for instagram auth
<li> Run this command to install package</li>

```bash
dart pub add insta_login
```

<li> Then write this code </li>

```dart
//May be it will work, I didn't test it
InstaView(
    instaAppId: '',
    instaAppSecret:
        '',
    redirectUrl: 'https://ayesha-iftikhar.web.app/',  // MAy be she is the creator
    onComplete: (_token, _userid, _username) {
    WidgetsBinding.instance.addPostFrameCallback((
        timeStamp,
    ) {
        setState(() {
        token = _token;
        userid = _userid;
        username = _username;
        });
    });
    },
);
```
