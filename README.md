# keyboard-maestro-cycling-window-manager

A cycling window manager partially inspired by Raycast, but with extra unique features such as undo and compound hotkeys.

Why use this over the new window management features in MacOS 15 Sequoia?

1. Cycling behavior gives quick access to more window positions without having to remember as many hotkeys
2. Compound hotkeys provide an intuitive visual/spatial set of key combinations that are easy to remeber
3. Undo functionality

## —Cycling Window Manager—

Written by @gaufde  
https://github.com/gaufde/keyboard-maestro-cycling-window-manager  
https://forum.keyboardmaestro.com/t/macros-cycling-window-manager/38293

## —Features—

The point of this macro group is to make it easy to size and move window on multiple screens.

These macros support:
1. Any number of monitors/screens
2. Move the front window to any half of the screen with a hotkey command
3. Move the front window to any quarter of the screen, or fill the screen with a compound hotkey command (similar to the WinMover macros by @cfriend)
4. Move the front window to any third of the screen by repeatedly cycling the hotkey commands (similar to how Raycast does it)
5. Move the front window to the center of the screen
6. Move the front window to the center of the screen without resizing
7. Move the front window to the previous size and position to “undo” a move.
8. Throw the front window to the next/previous screen (maintaining relative size and position)

## —Requirements—

These macros were written and tested in KM 11.0.3 on MacOS 13.7.

## —Example Usage—

⌃⌥⌘←       = left column (first cycle)  
    ⌃⌥⌘←   = left third (second cycle)  
    ⌃⌥⌘←   = left two-thirds (third cycle)  
    ⌃⌥⌘←   = middle third (fourth cycle)  

Note: Similar behavior is available for →,↓, and ↑. Also,  despite the animation of the window motion being slower in KM 11.0.2+, I have put work into making sure that the cycling can handle fast inputs. Simply count the number of key-presses and the window should ultimately end up in the correct position!

⌃⌥⌘.               = Center window on current screen without resizing  

⌃⌥⌘ + /        = center half size (first cycle)  
    ⌃⌥⌘/       = center 5/8 size (second cycle)  
    ⌃⌥⌘/       = center 3/4 size (third cycle)  
    ⌃⌥⌘/       = full screen (fourth cycle)  

⌃⌥⌘←↑       = top left quadrant of the screen  

Note: similar behavior is available for ↑→,←↓, and ↓→.  


⌃⌥⌘←→       = full screen  
⌃⌥⌘↓↑          = full screen  

Note: these compound hotkeys are most reliable if you hold the keys down for just a moment longer than you would a normal press.

⌃⌥⌘Z            = cycle through the previous window frames for the current window.  

⌃⌥←              = Throw window to previous screen  
⌃⌥→              = Throw window to next screen  

## —Installation—

Download the .kmmacros file and double click it to install in Keyboard Maestro. The macro group will be disabled by default, so right click and choose enable. That’s it, all the hotkeys should now work!

## —Parameters—

You can adjust the timeout before the cycling resets in the `CWM-SUB: Init` macro.

If you want, you can remove the animation delay that KM added in 11.0.2. Simply run the `CWM-HELPER: Set WindowSetFrameAnimationTime` macro using the “Try” button in the KM GUI. If you have issues with windows moving unreliably, then use the `CWM-HELPER: Reset WindowSetFrameAnimationTime` macro to revert back to the default settings.

## —Extending—

It should be relatively easy to extend these macros if you want to customize them or add functionality.

The existing macros should serve as a guide. Duplicate the one most similar to what you want and edit it from there.

That said, here are a couple of important guidelines:

1. Use your own `window_cycle_namespace` for new functionality. The namespaces currently used are `up`, `down`, `left`, `right`, `center`, `undo`, and `reset`. You will choose a namespace when calling `CWM-SUB: Calculate cycling index`, or you can write to the dictionary directly. If you need to force the cycle to reset, then set `window_cycle_namespace` in the dictionary to `reset` directly. 

2. When using `CWM-SUB: Move window to position`, the last parameter allows you to choose between passing coefficients only, or passing the values directly. Coefficients are easiest when working with fractions of the screen size, but sometime more flexibility is needed. See `CWM Window Center Move Only` for an example of passing values directly.

## —Change Log—

1.0.0  
First public release