# CLibui
SPM package for the [libui](https://github.com/andlabs/libui) toolkit.

![example gif](https://fat.gfycat.com/LikelyFlickeringElectriceel.gif)

# Installation

```sh
git clone https://github.com/andlabs/libui.git && cd libui
make && sudo make install
cp /usr/lib/libui.dylib /usr/local/lib/libui.dylib
ln -s /usr/local/lib/libui.dylib /usr/local/lib/libui.A.dylib
cp /usr/include/ui*.h /usr/local/include
```

When compiling through SPM, make sure to add the correct include and linker flags like so:

```sh
swift build -Xcc -I/usr/local/include -Xlinker -L/usr/local/lib
```

# Example

```swift
import CLibui

var options = uiInitOptions(Size: 0)
let error = uiInit(&options)
guard error == nil else { fatalError(String(validatingUTF8: error)!) }

let menu = uiNewMenu("File")
uiMenuAppendItem(menu, "item")
uiMenuAppendQuitItem(menu)

uiOnShouldQuit( { _ in print("quitting!"); return 1 }, nil)

let window = uiNewWindow("Window", 640, 480, 1)
uiWindowSetMargined(window, 1)
uiWindowOnClosing(window, { _ in print("closing!"); return 1 }, nil)

let box = uiNewVerticalBox()
uiBoxSetPadded(box, 1)
uiWindowSetChild(window, UnsafeMutablePointer(box))

let label = uiNewLabel("hello, libui!")
uiBoxAppend(box, UnsafeMutablePointer(label), 0)

uiControlShow(UnsafeMutablePointer(window))

uiMain()
```
