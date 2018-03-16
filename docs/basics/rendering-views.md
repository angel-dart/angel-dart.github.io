# Rendering Views
Just like `res.render` in Express, Angel's `ResponseContext` exposes a `Future` called `render`. This invokes whichever function is assigned to your server's `viewGenerator`.

There is a Mustache templating plug-in for Angel available: [https://github.com/angel-dart/mustache](https://github.com/angel-dart/mustache)

## Example

```dart
app.get('/view', (req, res) async => await res.render('hello', {'locals': ['foo', 'bar']});
```

## ViewGenerator
Angel declares the following typedef:

```dart
/// A function that asynchronously generates a view from the given path and data.
typedef Future<String> ViewGenerator(String path, [Map data]);
```

A templating plug-in can assign one of these to `app.viewGenerator` to set itself up:

```dart
import 'dart:io';
import 'package:angel_framework/angel_framework.dart';

Future plugin(Angel app) async {
  app.viewGenerator = (String path, [Map data]) async {
    return "Requested view $path with locals: $data";
  };
}

main() async {
  Angel app = new Angel();
  await app.configure(plugin);
  await app.startServer();
}
```

# Next Up...
1. Explore Angel's isomorphic [client library](client-library.md).
2. Find out how to [test Angel applications](testing.md).