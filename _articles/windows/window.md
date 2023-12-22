---
title: Window (Windows)
---
A *window* is the primary UI element of the Windows operating system. The defining traits of a window are:

- it occupies a portion of the screen,
- it may be visible,
- it knows how to draw itself, and
- it responds to events.

## Types

There are several kinds of windows with different functions in the UI:

### Application window

A window that acts as the main container for child UI elements that make up the GUI for the application. This window has a title bar, a minimize button, a maximize button, and a close button; this area is called the *non-client area* and is managed by the operating system. The rest of this window is the *client-area* and the window is responsible for managing how this area is drawn.

### UI controls

Generally, this window represents some interactive UI element positioned relative to the application window. These windows are *child* windows to some parent application window.

### Modal windows

Modal dialog windows typically contain a message or prompt for the user about the state of another application window. This window is *owned* by the application window it refers to. Owned windows always appear in front of their owner window, are only visible when their owner is visible, and are destroyed when their owner is destroyed.

## Window Handles

Window handles are integers used to refer to window objects. They are integers that are used to index a table of all windows, similar to file descriptors. 

## Coordinates

Some functions reference the top-left most pixel of the client area as (0,0). Coordinates that use that as the origin are called *client coordinates*.

Other functions reference the top-left most pixel of the non-client area; these are *window coordinates*.

Functions that reference the top-left coordinate of the entire screen are said to use *screen coordinates*.

## Reference

<https://learn.microsoft.com/en-us/windows/win32/learnwin32/what-is-a-window->. Accessed 2023-12-20
