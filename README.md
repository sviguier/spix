# Spix

[![Build Status](https://www.travis-ci.org/faaxm/spix.svg?branch=master)](https://www.travis-ci.org/faaxm/spix)

Spix is a minimally invasive UI testing library that enables your
Qt/Qml app's UI to be controlled either via c++ code, or through a http RPC
interface.

UI elements are referenced through names and paths which are robust against
design changes. To click on a button you write

```c++
mouseClick("mainWindow/ok_button");
```

To provide an RPC test interface to your App,
only add these three lines to your `main(...)` function:

```c++
spix::AnyRpcServer server;
auto bot = new spix::QtQmlBot();
bot->runTestServer(server);
```

And a test script in python could look like this:

```c++
import xmlrpc.client

s = xmlrpc.client.ServerProxy('http://localhost:9000')
s.mouseClick("mainWindow/Button_1")
s.wait(200)
s.mouseClick("mainWindow/Button_2")
resultText = s.getStringProperty("mainWindow/results", "text")
s.quit()
```

## What is this good for

The obvious use for Spix is to automatically test the GUI of your Qt/QML application
and make sure that it behaves as you expect. However, you can also use Spix as
an easy way to remote control existing Qt/QML applications or to automatically
generate and update screenshots for your documentation.

## Getting Started

### Requirements

* Qt
* [AnyRPC](https://github.com/sgieseking/anyrpc)

### Installation (Mac)

* Qt can be installed via `brew install qt`
* Clone `anyrpc`anf follow README to install, make sure to run `make install`

* Now build spix as follows

```console
cd spix
mkdir build
cd build
cmake-gui ..

Select generate, then close window when finished

make
```


## Current Features

* Send mouse events (click, move, drag/drop)
* Drop mime data from external apps
* Enter text
* Check existence and visibility of items
* Get property values of items (text, position, color, ...)
* Take and save a screenshot
* Quit the app
* Remote control, also of embedded devices / ios