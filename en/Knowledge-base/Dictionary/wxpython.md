---
title: wxPython
description: 
published: true
date: 2023-02-24T03:32:36.769Z
tags: 
editor: markdown
dateCreated: 2023-02-24T03:32:29.597Z
---

- [wxPython***Korean** document is available*](/ko/Knowledge-base/Dictionary/wxpython)
{.links-list}



# Overview
wxPython is a GUI toolkit for the Python programming language. It enables developers to create applications with a native graphical user interface on multiple platforms including Windows, Mac OS, and Unix. It is an open source library that is free to use and distribute.

# Description
wxPython is a wrapper around the popular wxWidgets cross-platform C++ library. It provides a set of Python classes and functions that allow developers to create applications with a native graphical user interface. It is written in Python and C++ and is available for Windows, Mac OS, and Unix platforms.

The wxPython library provides a wide range of features, including:

- A set of GUI controls such as buttons, checkboxes, and text boxes
- Support for layout management and window positioning
- Event handling for user actions such as mouse clicks
- Drawing capabilities for creating custom graphics
- Support for printing and drag-and-drop
- Access to native platform features such as the clipboard and file system

wxPython also provides a number of utility classes and functions for working with the underlying wxWidgets library. This includes functions for managing windows, dialogs, and frames, as well as functions for working with the clipboard and file system.

# History
wxPython was originally developed by Robin Dunn in 1998. It was initially released as a commercial product, but later released as open source software in 1999. Since then, it has been actively maintained and developed by a group of volunteers.

# Features
wxPython provides a wide range of features for creating GUI applications. These include:

- A set of GUI controls such as buttons, checkboxes, and text boxes
- Support for layout management and window positioning
- Event handling for user actions such as mouse clicks
- Drawing capabilities for creating custom graphics
- Support for printing and drag-and-drop
- Access to native platform features such as the clipboard and file system
- Utility classes and functions for working with the underlying wxWidgets library

# Example
The following example shows how to create a simple window using wxPython:

```python
import wx

app = wx.App()

frame = wx.Frame(None, title="Hello World")
frame.Show()

app.MainLoop()
```

# Pros and Cons
The main advantage of wxPython is its cross-platform compatibility. It allows developers to create applications with a native graphical user interface that runs on Windows, Mac OS, and Unix platforms.

The main disadvantage of wxPython is that it is written in Python and C++, which can make it difficult to debug and maintain.

# Related Technology
wxPython is related to other GUI toolkits such as PyQt, Tkinter, and wxWidgets. It is also related to other Python libraries such as PyGTK and PyGame.