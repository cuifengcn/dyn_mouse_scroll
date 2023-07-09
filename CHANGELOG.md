## 1.0.8

- Include Wizzel1's scroll speed commits (but changed scrollSpeed from int to double)
- When changing scroll direction, restart animation from current position instead of future position.
- Change animation curve to Curves.easeOutQuart (looks more natural), speed to 2.0 and duration to 380
- Fix trackpad gestures not working when switching between mouse wheel and trackpad
- Fix trackpad gestures not working out of the box (it used to require a click with trackpad to work)
- Detect locked scrollbar, default behaviour for scrollview not scrollable (e.g. when the mouse is hovering the scrollbar)
