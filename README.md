# CLibui
SPM package for the [libui](https://github.com/andlabs/libui) toolkit.

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
