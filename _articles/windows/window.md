---
title: Window (Windows)
---
A *window* is the primary user interface(UI) element of the Windows operating system. The defining traits of a window are:

- it occupies a portion of the screen,
- it may be visible,
- it knows how to draw itself, and
- it responds to events [^1].

Each window has a *window handle*. Handles are integers used to refer to window objects. They index a table of all windows, similar to file descriptors. Each window belongs to a *window class* [^2]. A window class defines behavior that a set of windows may have in common. Each window class must have a *window procedure*, application instance handle, and window class name registered to it. A window procedure, also known as a *window proc*, is a callback that defines the behavior of a window when handling a message. Window class names need to be unique to the process and must avoid conflicts with any existing window classes defined as part of the standard library. Data that is unique to a particular instance of a window class is called *instance data*.

## Types

There are several kinds of windows with different functions in the UI:

### Application window

An application window acts as the main container for child UI elements that make up the GUI for the application [^1]. This window has a title bar, a minimize button, a maximize button, and a close button; this area is called the *non-client area* and is managed by the operating system. The rest of this window is the *client area* and the window is responsible for managing how this area is drawn.

Some functions reference the top-left most pixel of the client area as (0,0). Coordinates that use that as the origin are called *client coordinates*. Other functions reference the top-left most pixel of the non-client area; these are *window coordinates*. Functions that reference the top-left coordinate of the entire screen are said to use *screen coordinates*.

### UI controls

Generally, this window represents some interactive UI element positioned relative to the application window [^1]. These windows are *child* windows to some parent application window.

### Modal windows

Modal dialog windows typically contain a message or prompt for the user about the state of another application window [^1]. This window is *owned* by the application window it refers to. Owned windows always appear in front of their owner window, are only visible when their owner is visible, and are destroyed when their owner is destroyed.

## Reference

[^1]: Quinn Radich, et al. "What Is a Window?" *Microsoft Learn*,  [**learn.microsoft.com/en-us/windows/win32/learnwin32/what-is-a-window-**](https://learn.microsoft.com/en-us/windows/win32/learnwin32/what-is-a-window-). [Archived](https://web.archive.org/web/20240114173810if_/https://learn.microsoft.com/en-us/windows/win32/learnwin32/what-is-a-window-) from the original on 14 Jan 2024. Accessed 14 Jan 2024.
[^2]: Quinn Radich, et al. "Create a window." *Microsoft Learn*, [**learn.microsoft.com/en-us/windows/win32/learnwin32/creating-a-window**](https://learn.microsoft.com/en-us/windows/win32/learnwin32/creating-a-window). [Archived](https://web.archive.org/web/20240114185208if_/https://learn.microsoft.com/en-us/windows/win32/learnwin32/creating-a-window) from the original on 14 Jan 2024. Accessed 14 Jan 2024.
