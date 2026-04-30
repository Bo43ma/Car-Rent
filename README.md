# Car Rent — Flutter Car Rental App

A sleek, animated Flutter application for browsing and renting luxury cars. Built with a custom bottom sheet, smooth animations, and a reactive BLoC-style state management pattern.
---

## Features

- **Animated Car Details** — Fade and scale transitions trigger when the bottom sheet is expanded or collapsed
- **Image Carousel** — Swipeable car image gallery powered by `flutter_carousel_widget`, with a custom indicator bar
- **Draggable Bottom Sheet** — Custom bottom sheet with tap and vertical drag gesture support; slides up to reveal full car specs
- **Car Specifications** — Horizontally scrollable cards for Offer Details, Specifications, and Features
- **BLoC-style State Management** — Lightweight reactive state using Dart `Stream`s and a `StreamController`, no external BLoC package required

---

## Project Structure

```
lib/
    bloc/ state_bloc.dart       # Stream-based state management (animation toggle)
          state_provider.dart   # Holds and toggles animation state

    model/ car.dart              # Car & CarList data models + sample data

    main.dart                 # UI: AppBar, carousel, bottom sheet, animations
```

---

## Getting Started

### Prerequisites

- Flutter SDK `>=3.0.0`
- Dart SDK `>=3.0.0`

### Assets

Place your car images inside the `assets/` folder and declare them in `pubspec.yaml`:

```yaml
flutter:
  assets:
    - assets/corvette_front.png
    - assets/corvette_back.png
    - assets/interior1.png
    - assets/interior2.png
    - assets/corvette_front2.png
    - assets/lambo_front.png
    - assets/interior_lambo.png
    - assets/lambo_back.png
```

---

## Dependencies

| Package | Purpose |
|---|---|
| [`flutter_carousel_widget`](https://pub.dev/packages/flutter_carousel_widget) | Image carousel for car photos |

Add to `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_carousel_widget: ^2.0.0
```

---

## State Management

This project uses a minimal custom BLoC pattern without any external state management library:

- **`StateProvider`** — holds a single `isAnimating` boolean and toggles it
- **`StateBloc`** — wraps the provider with a `StreamController`, broadcasting animation state changes to the UI
- **`StreamBuilder`** in `CarDetailsAnimation` — listens to the stream and drives fade/scale `AnimationController`s accordingly

This is a great example of using Dart's built-in reactive primitives before reaching for packages like `flutter_bloc` or `riverpod`.

---

## How to Add a New Car

Open `lib/model/car.dart` and add a new `Car` to the `carList`:

```dart
Car(
  companyName: "Ferrari",
  carName: "F8 Tributo",
  price: 4500,
  imgList: ["ferrari_front.png", "ferrari_side.png"],
  offerDetails: [
    {Icon(Icons.speed): "Automatic"},
    {Icon(Icons.people): "2 seats"},
  ],
  specifications: [
    {Icon(Icons.av_timer): {"Mileage": "8 kmpl"}},
    {Icon(Icons.power): {"Engine": "3902 cc"}},
  ],
  features: [
    {Icon(Icons.bluetooth): "Bluetooth"},
    {Icon(Icons.ac_unit): "AC"},
  ],
)
```
