# Gaming Layer for Cornholius

The Gaming Layer is a special layer designed for gaming on the Cornholius (48-key Cornelius) keyboard. It provides a standard QWERTY layout without tap-hold behaviors and makes use of the extra keys available on the 48-key board.

## Features

- **Plain QWERTY layout**: No tap-hold behaviors that could interfere with gaming
- **Utilizes extra keys**: The far left and far right columns, plus the bottom row corners are used for common gaming keys
- **Layer lock**: You can lock onto the gaming layer and return to the base layer when done

## Key Layout

### Core Area (Standard QWERTY)
The main 3x10 alpha block uses standard QWERTY layout:
```
Q W E R T    Y U I O P
A S D F G    H J K L '
Z X C V B    N M , . /
```

### Thumb Keys
- Left side: ESC, SPACE, TAB
- Right side: ENTER, BACKSPACE, To Base Layer

### Extra Keys (Left Column)
- Top: LCTRL
- Middle: LSHFT
- Bottom: LALT
- Far Bottom Left: Lock to Game Layer
- Next: LGUI
- Next: DEL

### Extra Keys (Right Column)
- Top: RCTRL
- Middle: RSHFT
- Bottom: RALT
- Far Bottom Right: To Base Layer
- Previous: F2
- Previous: F1

## How to Access

1. **Enter Gaming Layer**: Press and hold the FUN layer thumb key, then double-tap the key in position RALT (bottom right home row position) to lock into the gaming layer
2. **Exit Gaming Layer**: Double-tap the "To Base Layer" key in the bottom right corner or in the right thumb cluster

## Common Gaming Use Cases

- **FPS Games**: Left hand on WASD with easy access to CTRL/SHIFT/ALT for crouch/sprint/abilities
- **MOBA Games**: Standard key positions for abilities with modifier keys on the left column
- **MMO Games**: All letters available plus easy modifier access

## Building with Gaming Layer

The gaming layer is automatically included when building for the Cornholius keyboard. No special configuration is required.

To build with the standard workflow:
```yaml
board: cornholius
alphas: qwerty  # or your preferred layout for the base layer
```

The gaming layer will use QWERTY regardless of your base layer choice.
