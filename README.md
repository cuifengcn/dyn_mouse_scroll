# Multiplatform Smooth Scroll
A fork of the [dyn_mouse_scroll](https://pub.dev/packages/dyn_mouse_scroll) package, including [Wizzel1's fixes](https://github.com/Wizzel1/dyn_mouse_scroll) and my own fixes;
Provides wrapper for scrollable widgets that enables smooth scrolling with a mouse wheel, trackpad or touch screen on all platforms;
This fork fixes all issues regarding trackpad, mouse/trackpad switching and animations, fixing the slippery effect when changing scroll direction;
The fork also changes the default mouse scroll animation to look smoother;
Additionally, it allows to change the scroll speed, on top of the duration and animation curve.

First gif: Scrolling slowly.  
Second gif: Scrolling quickly (flick scroll).   
Third gif: Mobile drag scroll detected, physics change.  
<p float="left">
  <img src="https://raw.githubusercontent.com/Bluebar1/dyn_mouse_scroll/main/assets/slow_scroll.gif" width="200" height="350"/>
  <img src="https://raw.githubusercontent.com/Bluebar1/dyn_mouse_scroll/main/assets/fast_scroll.gif" width="200" height="350"/>
  <img src="https://raw.githubusercontent.com/Bluebar1/dyn_mouse_scroll/main/assets/drag_scroll.gif" width="200" height="350"/>
</p>

## Features
* Animate smooth scroll based on speed of user's scroll.
* Automatically detect if the wrong ScrollPhysics is being used and update using [provider](https://pub.dev/packages/provider).
* Adjust the duration of your scroll events.
* Choose what mobile physics you would like to use.
## Basic Usage
```dart
DynMouseScroll(
  builder: (context, controller, physics) => ListView(
    controller: controller,
    physics: physics,
    children: ...
    )
)
```

With additional settings:
```dart
DynMouseScroll(
  durationMS = 500,
  scrollSpeed = 4.4,
  animationCurve = Curves.easeOutQuart,
  builder: (context, controller, physics) => ListView(
    controller: controller,
    physics: physics,
    children: ...
    )
)
```

## Problem:
Flutter does not animate smooth scrolls for pointers, causing choppy experiences for the end user.
One package, [web_smooth_scroll](https://pub.dev/packages/web_smooth_scroll), attempts to fix this problem
by disabling default scrolling entirely (mobile can't drag now) and listening for pointer events to animate
the scroll controller that can only move at one speed. 

## Solution:
To allow mobile default scrolling to still be accessible ~~I detect the user's platform
and automatically update if the detection was wrong. When the user scrolls, the 'futurePosition'
variable is updated and the animation is started~~ I set the mobile scroll physics as the default
one, switching to desktop scroll physics as the mouse wheel scroll is initiated and only starting the animation
after the widget is rebuilt; the desktop scroll physics then takes priority over mobile physics,
switching back to mobile physics only after the last scroll animation has ended, only if no new scroll wheel
action had been initiated in the meantime.

