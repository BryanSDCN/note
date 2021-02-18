.. _windowsdev:

==============================
Windows开发笔记
==============================

不用DLL实现键盘钩子
=========================

g_hHook=SetWindowsHookEx(WH_JOURNALRECORD,KeyboardProc,GetModuleHandle(NULL),0);

http://blog.sina.com.cn/s/blog_6d3bb6bf0100mp7h.html




常用的API
==========================

LowLevelKeyboardProc callback function

KBDLLHOOKSTRUCT structure (winuser.h)

ShellExecuteA function (shellapi.h)

WM_XBUTTONDOWN message

SetWindowsHookExA function (winuser.h)

SetWindowsHookExA function (winuser.h)

KBDLLHOOKSTRUCT structure (winuser.h)

LowLevelMouseProc function

MSLLHOOKSTRUCT structure (winuser.h)

LoadImageA function (winuser.h)

MAKEINTRESOURCEA macro (winuser.h)

GetModuleHandleA function (libloaderapi.h)

MouseProc callback function

WindowProc callback function

SendInput function (winuser.h)

MapVirtualKeyA function (winuser.h)

WM_KEYDOWN message

About Keyboard Input

PostMessageA function (winuser.h)

keybd_event function (winuser.h)

CreateCompatibleBitmap function (wingdi.h)

WM_SYSKEYDOWN message

Sleep function (synchapi.h)

RegisterHotKey function (winuser.h)

CreateIconIndirect function (winuser.h)

CreateWindowA macro (winuser.h)

WM_HOTKEY message


`Virtual-Key Codes`__

.. __: https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes



C语法笔记
===============

high-order和low-order
--------------------------

high-order byte/word，指高位字节或者字(2字节)
low-order byte/word，指低位字节或者字


C++语法笔记
==================




