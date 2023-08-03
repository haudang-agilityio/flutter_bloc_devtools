# Remote Devtools for flutter_bloc

## Progress
Fork of https://github.com/andrea689/flutter_bloc_devtools, and custom support null safety and cubit for latest versions of [bloc](https://pub.dev/packages/bloc)

Because the flutter_bloc_devtools package not support null safety.


## Original docs

Remote Devtools support for Blocs of [flutter_bloc](https://github.com/felangel/bloc/tree/master/packages/flutter_bloc).

Note: `Cubit` is supported

![Devtools Demo](https://github.com/andrea689/flutter_bloc_devtools/raw/main/demo.gif)

## Installation

Add the library to pubspec.yaml:

```yaml
dependencies:
  flutter_bloc_devtools:
    git:
      url: https://github.com/haudang-agilityio/flutter_bloc_devtools.git
      ref: main
```

Note: The version on pub.dev doesn't work with null safety and v8 of bloc.

## BlocObserver configuration

Add `RemoteDevToolsObserver` to your `Bloc.observer`:

```dart
void main() async {
  BlocOverrides.runZoned(
        () async => runApp(const CounterApp()),
    blocObserver: RemoteDevToolsObserver('127.0.0.1:8000'),
  );
}
```

## Making your Events and States Mappable

Events and States ~~have to~~ may implement `Mappable`:

```dart
class CounterState extends Equatable implements Mappable {
  final int counter;

  const CounterState({
    this.counter,
  });

  @override
  List<Object> get props => [
        counter,
      ];

  @override
  Map<String, dynamic> toMap() => {
        'counter': counter,
      };
}
```

## Using remotedev

Use the Javascript [Remote Devtools](https://github.com/zalmoxisus/remotedev-server) package. Start the remotedev server on your machine

```bash
npm install -g remotedev-server
remotedev --port 8000
```

Run your application. It will connect to the remotedev server. You can now debug your flutter_bloc application by opening up `http://localhost:8000` in a web browser.

## Examples

- [Counter](example/counter)
