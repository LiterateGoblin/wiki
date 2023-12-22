---
title: Win32
---
Win32 is a Windows API. As the first Windows API, applications developed using it are often faster than apps developed using other APIs, and offers greater developer freedom - at the expense of abstraction.

## Conventions

### BOOL

Boolean values returned by Win32 functions use the `BOOL` typedef rather than the `bool` type native to C++. This maps to `0` or `1` (for `FALSE` and `TRUE`  respectively) - yet most functions can return any non-zero integer to indicate "true". Therefore, conditional statements are required to **not** compare the return value to a `BOOL`. For example, the following is incorrect:

```
if (returnBool() == TRUE) { // Wrong!
...
}
```

But the following is correct:

```
if (returnBool()) {
...
}
```

### Entrypoint

Each Windows program has an entrypoint function known as `winMain` or `wWinMain`.

## References

<https://learn.microsoft.com/en-us/windows/apps/get-started/?tabs=cpp-win32%2Cnet-maui>. Accessed on 2023-12-20

<https://learn.microsoft.com/en-us/windows/win32/learnwin32/windows-coding-conventions>. Accessed on 2023-12-20
