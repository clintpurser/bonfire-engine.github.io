# Get Started

> An awesome project.

## Installing

1. Depend on it

Add this to your package's pubspec.yaml file:

```yaml
dependencies:
  bonfire: ^LATEST_VERSION
```

2. Install it

You can install packages from the command line:

```
$ flutter pub get
```

3. Import it

Now in your Dart code, you can use:

```dart
import 'package:bonfire/bonfire.dart';
```

## Using

### Creating your map
You need create your map using [Tiled](https://www.mapeditor.org/). After that you can export your map in json file. [See more detail about Tiled in Bonfire](tiled_support)

Now you can run to see your map:


```dart
@override
  Widget build(BuildContext context) {
    return BonfireWidget(
      joystick: Joystick(
        directional: JoystickDirectional(),
      ), // required
      map: WorldMapByTiled('tile/map.json', forceTileSize: 32),
    );
  }
```

This way you can see your map be rendering and can use directional joystick to explorer.


### Creating your player

To create a player you will need SpriteAnimations. You can see how load Sprites in [Flame doc](https://docs.flame-engine.org/main/flame/rendering/images.html)

- [IMAGES USED](https://github.com/RafaelBarbosatec/bonfire/tree/master/example/assets/images/player)

```dart
class PlayerSpriteSheet {
 
  static Future<SpriteAnimation> get idleRight => SpriteAnimation.load(
        "player/knight_idle.png",
        SpriteAnimationData.sequenced(
          amount: 6,
          stepTime: 0.1,
          textureSize: Vector2(16, 16),
        ),
      );

  static Future<SpriteAnimation> get runRight => SpriteAnimation.load(
        "player/knight_run.png",
        SpriteAnimationData.sequenced(
          amount: 6,
          stepTime: 0.1,
          textureSize: Vector2(16, 16),
        ),
      );

  static SimpleDirectionAnimation get simpleDirectionAnimation =>
      SimpleDirectionAnimation(
        idleRight: idleRight,
        runRight: runRight,
      );
}
```


To create a player just need create a class and extends by `SimplePlayer`. [See more detail about Player in Bonfire](player)


```dart

class Kinght extends SimplePlayer {

    Kinght(Vector2 position)
      : super(
          position: position, 
          size: Vector2(32,32),
          animation: PlayerSpriteSheet.simpleDirectionAnimation,
      );
}

```

Now only adds your player in the game:


```dart
@override
  Widget build(BuildContext context) {
    return BonfireWidget(
      joystick: Joystick(
        directional: JoystickDirectional(),
      ), 
      map: WorldMapByTiled('tile/map.json', forceTileSize: 32),
      player: Kinght(Vector2(40,40))
    );
  }
```

And then you can see your player in the map and move that with directional of the Joystick.

### Next step
Know all components that you can use in Bonfire [See here](overview)

Complete simple example you can see [here](https://github.com/RafaelBarbosatec/bonfire/tree/master/example/lib/simple_example).