---
title: Developing a Graphical User Interface (GUI) using Python
description: 
published: true
date: 2023-02-17T18:01:52.692Z
tags: 
editor: markdown
dateCreated: 2023-01-30T05:27:31.681Z
---

- [Python을 사용하여 그래픽 사용자 인터페이스(GUI) 개발***Korean** version of this document is available*](/ko/Knowledge-base/Common/developing-a-graphical-user-interface-gui-using-python)
{.links-list}



## What is a GUI?

A Graphical User Interface (GUI) is a type of user interface that allows users to interact with electronic devices in a graphical way, usually using a pointing device like a mouse, to control electronic applications. 

A GUI offers a more intuitive way for users to interact with computer applications than a command line interface (CLI), which requires users to learn and type commands. GUIs also make it easier for new users to get started with using an application. 

Creating a GUI in Python is done using a module called PyQt5. PyQt5 is a comprehensive set of Python bindings for Qt v5. Qt is a cross-platform application development framework widely used for the development of GUI programs.

## How to create a GUI in Python

There are many ways to create a GUI in Python, but the most commonly used module is PyQt5. 

PyQt5 is a comprehensive set of Python bindings for Qt v5. Qt is a cross-platform application development framework widely used for the development of GUI programs. 

To create a basic GUI in Python using PyQt5, you need to do the following:

1. Import the PyQt5 module.
2. Create a QtWidgets.QApplication instance. 
3. Create a QtWidgets.QWidget instance. 
4. Set the widget's properties.
5. Add a QtWidgets.QLabel instance to display text.
6. Add a QtWidgets.QPushButton instance to trigger an action.
7. Connect the button's clicked signal to a slot.
8. Run the application.

Let's go through each step in detail. 

### Importing the PyQt5 module

First, we need to import the PyQt5 module. We can do this using the following code:

```
import PyQt5
```

### Creating a QtWidgets.QApplication instance

Next, we need to create a QtWidgets.QApplication instance. This instance is responsible for managing the application's control flow and main settings. 

We can create a QApplication instance by calling the QtWidgets.QApplication() constructor. We need to pass in the command line arguments using the sys.argv parameter. 

```
import sys

app = QtWidgets.QApplication(sys.argv)
```

### Creating a QtWidgets.QWidget instance

Once we have a QApplication instance, we can create a QtWidgets.QWidget instance. This widget will be the main container for our GUI. 

We can create a QWidget instance by calling the QtWidgets.QWidget() constructor. 

```
widget = QtWidgets.QWidget()
```

### Setting the widget's properties

Once we have a QWidget instance, we can set its properties. The most common properties that we set are the widget's size and position. 

We can set the size of the widget using the QtWidgets.QWidget.resize() method. We need to pass in the width and height of the widget in pixels. 

```
widget.resize(400, 300)
```

We can set the position of the widget using the QtWidgets.QWidget.move() method. We need to pass in the x and y coordinates of the widget in pixels. 

```
widget.move(100, 100)
```

### Adding a QtWidgets.QLabel instance

Once we have a QWidget instance, we can add child widgets to it. The most common child widget that we add to a QWidget is a QtWidgets.QLabel. 

A QLabel is a widget that can display text. We can create a QLabel by calling the QtWidgets.QLabel() constructor. We need to pass in the text that we want to display. 

```
label = QtWidgets.QLabel("Hello, World!")
```

Once we have a QLabel, we can add it to our QWidget using the QtWidgets.QWidget.addWidget() method. 

```
widget.addWidget(label)
```

### Adding a QtWidgets.QPushButton instance

Once we have a QWidget, we can also add a QtWidgets.QPushButton. A QPushButton is a widget that can be clicked by the user to trigger an action. 

We can create a QPushButton by calling the QtWidgets.QPushButton() constructor. We need to pass in the text that we want to display on the button. 

```
button = QtWidgets.QPushButton("Click me!")
```

Once we have a QPushButton, we can add it to our QWidget using the QtWidgets.QWidget.addWidget() method. 

```
widget.addWidget(button)
```

### Connecting the button's clicked signal to a slot

Once we have a QPushButton, we need to connect its clicked signal to a slot. A slot is a Python callable. When the button is clicked, the slot will be called. 

We can connect the button's clicked signal to a slot using the QtCore.QObject.connect() method. We need to pass in the button's clicked signal and the slot that we want to call. 

```
QtCore.QObject.connect(button, QtCore.SIGNAL("clicked()"), some_slot)
```

### Running the application

Once we have created our GUI, we can run it by calling the QtWidgets.QApplication.exec_() method. 

```
app.exec_()
```

## Example

Let's put all of the steps together to create a simple "Hello, World!" GUI. 

```
import sys
from PyQt5 import QtWidgets, QtCore

app = QtWidgets.QApplication(sys.argv)

widget = QtWidgets.QWidget()
widget.resize(400, 300)
widget.move(100, 100)

label = QtWidgets.QLabel("Hello, World!")
button = QtWidgets.QPushButton("Click me!")

widget.addWidget(label)
widget.addWidget(button)

QtCore.QObject.connect(button, QtCore.SIGNAL("clicked()"), some_slot)

widget.show()

app.exec_()
```

When we run the code, we should see a window like this:

![Hello, World!](https://github.com/mravendi/python_gui/raw/master/helloworld.png)

Clicking on the button will call the some_slot() function. 

## Conclusion

In this post, we have covered the basics of creating a GUI in Python using the PyQt5 module. We have seen how to create a QWidget, how to add child widgets to it, and how to connect the widget's signals to slots.