### Summary
A Meson build system implementation for GLFW v3.3.7

To use stand-alone, extract the contents of the glfw-patch directory into the root glfw-3.3.7 directory.<br>
To use as a wrap, extract the source tarball into your subproject directory.

##### TODO
- documentation build system
- Windows implementation
- MacOS/Cocoa implementation

##### Changes
v0.1.1
- Optimizations for pretty much everything

v0.1.0
- BSD & SunOS system dependency checks added
- Restructured project for future sanity

v0.1.0 (pre-2)
- Lowercased display-api options
- Added .wrapdb
- Rewrote Wayland implementation
- Updated to glfw-3.3.7

v0.1.0 (pre-1)
- Example binaries now properly install to {libdir}/GLFW
- Wayland API implemented

v0.0.0
- Initial push; only builds on Linux for X11
