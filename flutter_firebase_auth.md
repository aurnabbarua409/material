# Firebase Auth
<li> Install firebase CLI </li>

```bash
npm install -g firebase-tools
```

if you get error, check this url in system path:

```txt
C:\Users\Aurnab_Barua\AppData\Roaming\npm
```
<li> run: </li>

```bash
firebase login
```

<li> then run:
</li>

```bash
dart pub global activate flutterfire_cli
```


<li> run </li>

```bash
flutterfire configure
```
if you get error: check this in system path:

```txt
C:\Users\Aurnab_Barua\AppData\Local\Pub\Cache\bin
```

<li> then, run </li>

```bash
flutter pub add firebase_core
```

<li> Then run again </li>

```bash
flutterfire configure
```

<li> in lib/main.dart file, write </li>

```dart
import 'package:firebase_core/firebase_core.dart';
import 'firebase_options.dart';
```

<li> then </li>

```dart
WidgetsFlutterBinding.ensureInitialized();
await Firebase.initializeApp(
  options: DefaultFirebaseOptions.currentPlatform,
);
runApp(const MyApp());
```


