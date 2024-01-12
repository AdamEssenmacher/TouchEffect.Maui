# Maui.TouchEffect
Forked from the amazingly popular original TouchEffect Library, this Compat version aims to ease your migration from Xamarin.Forms to .NET MAUI with a compatible implementation to get you up and running without rewriting the parts of your app that relied on the original library.

Get it from NuGet:

[![Nuget](https://img.shields.io/nuget/v/TouchEffect.Maui.svg)](https://www.nuget.org/packages/TouchEffect.Maui)

> The aim of this library is to provide temporary support for the touch effect without having to take a dependency on [XCT's MauiCompat](https://devblogs.microsoft.com/xamarin/introducing-net-maui-compatibility-for-the-xamarin-community-toolkit/) library. My results of using the compat library have been extremely tempramental, alot of the times the touch effect does not work and due to the packages target framework (net6) & age (2 years old) I figured a new port would be the best option. When [CommunityToolkit.Maui](https://github.com/CommunityToolkit/Maui) eventually releases this feature I will archive this repository.

This library supports the following platforms:

| Platform     | Supported |
| ------------ | --------- |
| iOS          | ✅         |
| Android      | ✅         |
| Mac Catalyst | ❌         |
| Windows      | ❌         |
| Tizen        | ❌         |

Due to the temporary nature of this library, I will not be adding support for any platforms I do not personally need. I am open to PR's but MCT are aiming for a NET8 release of TouchEffect so this library will only be kicking around for a matter of weeks/months.

## Install

- Install TouchEffect.Maui package
- 
 ```
 Install-Package TouchEffect.Maui -Version 7.0.0
 ```

- In your `MauiProgram.cs`, call `UseMauiTouchEffect`:
  ```diff
  var builder = MauiApp.CreateBuilder();
          builder
              .UseMauiApp<App>()
  ++          .UseMauiTouchEffect()
              .ConfigureFonts(fonts =>
              {
                  fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");
                  fonts.AddFont("OpenSans-Semibold.ttf", "OpenSansSemibold");
              });
  ```

## Usage

See the samples app from this project, it is a port of the `TouchEffectPage` from the XCT samples app.

<img src="assets/Sample_Demonstration.gif" alt="Sample app included with this project" width="500">


```xaml
<StackLayout
    TouchEffect.AnimationDuration="250"
    TouchEffect.AnimationEasing="{x:Static Easing.CubicInOut}"
    TouchEffect.Command="{Binding Command, Source={x:Reference Page}}"
    TouchEffect.PressedOpacity="0.6"
    TouchEffect.PressedScale="0.8"
    HorizontalOptions="CenterAndExpand"
    Orientation="Horizontal">
    <BoxView
        HeightRequest="20"
        WidthRequest="20"
        Color="Gold" />
    <Label Text="The entire layout receives touches" />
    <BoxView
        HeightRequest="20"
        WidthRequest="20"
        Color="Gold" />
</StackLayout>
```


### TouchEff Attached Properties
Property | Type | Default | Description
--- | --- | --- | ---
IsAvailable | `bool` | true | Makes effect available
ShouldMakeChildrenInputTransparent | `bool` | true | Makes layout's children input trasparent
Command | `ICommand` | null | Touch Command handler
CommandParameter | `object` | null | Touch Command handler parameter
Status | `TouchStatus` | Completed | Current touch status
State | `TouchState` | Regular | Current touch state
RegularBackgroundColor | `Color` | Default | Background color of regular state
PressedBackgroundColor | `Color` | Default | Background color of pressed state
HoveredBackgroundColor | `Color` | Default | Background color of hovered state
RegularOpacity | `double` | 1.0 | Opacity of regular state
PressedOpacity | `double` | 1.0 | Opacity of pressed state
HoveredOpacity | `double` | 1.0 | Opacity of hovered state
RegularScale | `double` | 1.0 | Scale of regular state
PressedScale | `double` | 1.0 | Scale of pressed state
HoveredScale | `double` | 1.0 | Scale of hovered state
RegularTranslationX | `double` | 0.0 | TranslationX of regular state
PressedTranslationX | `double` | 0.0 | TranslationX of pressed state
HoveredTranslationX | `double` | 0.0 | TranslationX of hovered state
RegularTranslationY | `double` | 0.0 | TranslationY of regular state
PressedTranslationY | `double` | 0.0 | TranslationY of pressed state
HoveredTranslationY | `double` | 0.0 | TranslationY of hovered state
RegularRotation | `double` | 0.0 | Rotation of regular state
PressedRotation | `double` | 0.0 | Rotation of pressed state
HoveredRotation | `double` | 0.0 | Rotation of hovered state
RegularRotationX | `double` | 0.0 | RotationX of regular state
PressedRotationX | `double` | 0.0 | RotationX of pressed state
HoveredRotationX | `double` | 0.0 | RotationX of hovered state
RegularRotationY | `double` | 0.0 | RotationY of regular state
PressedRotationY | `double` | 0.0 | RotationY of pressed state
HoveredRotationY | `double` | 0.0 | RotationY of hovered state
AnimationDuration | `int` | 0 | The common duration of animation
AnimationEasing | `Easing` | null | The common easing of animation
PressedAnimationDuration | `int` | 0 | The duration of animation by applying PressedOpacity and/or PressedBackgroundColor and/or PressedScale
PressedAnimationEasing | `Easing` | null | The easing of animation by applying PressedOpacity and/or PressedBackgroundColor and/or PressedScale
HoveredAnimationDuration | `int` | 0 | The duration of animation by applying HoveredOpacity and/or HoveredBackgroundColor and/or HoveredScale
HoveredAnimationEasing | `Easing` | null | The easing of animation by applying HoveredOpacity and/or HoveredBackgroundColor and/or HoveredScale
RegularAnimationDuration | `int` | 0 | The duration of animation by applying RegularOpacity and/or RegularBackgroundColor and/or RegularScale
RegularAnimationEasing | `Easing` | null | The easing of animation by applying RegularOpacity and/or RegularBackgroundColor and/or RegularScale
RippleCount | `int` | 0 | This property allows to set ripple of animation (Pressed/Hovered/Regular animation loop). '**0**: disabled'; '**-1**: infinite loop'; '**1, 2, 3 ... n**: Ripple's interations'
IsToggled | `bool?` | null | This property allows to achieve "switch" behavior. **null** means that feature is disabled and view will return to inital state after touch releasing
DisallowTouchThreshold | `int` | 0 | Movement threshold for considering **android** touch as canceled
NativeAnimation | `bool` | false | If native platform touch feedback animations are present (Tilt on UWP, Ripple on Android, Opacity/Color on iOS)
NativeAnimationColor | `Color` | Color.Default | The color used for the native touch feedback animation
NativeAnimationRadius | `int` | -1 | The radius of the native ripple animation on Android or Layer radius on iOS

### TouchEff Attached events
Event | Type | Default | Description
--- | --- | --- | ---
StatusChanged | `TEffectStatusChangedHandler` | null | Touch status changed
StateChanged | `TEffectStateChangedHandler` | null | Touch state changed
HoverStatusChanged | `TEffectHoverStatusChangedHandler` | null | Hover status changed
HoverStateChanged | `TEffectHoverStateChangedHandler` | null | Hover state changed
Completed | `TEffectCompletedHandler` | null | User tapped
AnimationStarted | `AnimationStartedHandler` | null | Animation started

### TouchImage Bindable Properties
Property | Type | Default | Description
--- | --- | --- | ---
RegularBackgroundImageSource | `ImageSource` | null | Background image source of regular state
PressedBackgroundImageSource | `ImageSource` | null | Background image source of pressed state
HoveredBackgroundImageSource | `ImageSource` | null | Background image source of hovered state
RegularBackgroundImageAspect | `Aspect` | AspectFit | Background image aspect of regular state
PressedBackgroundImageAspect | `Aspect` | AspectFit | Background image aspect of pressed state
HoveredBackgroundImageAspect | `Aspect` | AspectFit | Background image aspect of hovered state

**If you want to customize/extend existing controls, you may observe State property via triggers**

Check source code for more info, or ***just ask me =)***

## License
The MIT License (MIT) see [License file](LICENSE)

## Contribution
Feel free to create issues and PRs 😃
