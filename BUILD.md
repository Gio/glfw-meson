
#### Usage
GLFW-Meson can be used either standalone or as a subproject.

##### Requirements
- [Meson](https://mesonbuild.com/) version "0.49.0" or later for standalone
- Meson version "0.55.0" or later for subproject
- [GLFW](https://www.glfw.org/) v3.3.7 source tarball

##### Standalone
First, unpack the glfw-meson & glfw-3.3.7 archives into a directory:<br>
`~/foo$ tar -xf glfw-meson.tar.gz && tar -xf glfw-3.3.7.tar.gz`

Next, copy the contents of the glfw-patch directory into the glfw-3.3.7 directory:<br>
`~/foo$ cp -r ./glfw-meson/glfw-patch/* ./glfw-3.3.7`

Finally, change to the glfw-3.3.7 directory, set up the build directory, and build the library:<br>
`~/foo/glfw-3.3.7$ meson setup build`<br>
`~/foo/glfw-3.3.7$ meson compile -C build`<br>

##### Subproject
First, unpack the glfw-meson archive:<br>
`~/foo$ tar -xf glfw-meson.tar.gz`

Then, simply copy glfw.wrap into the main project's subprojects directory and the glfw-patch directory into packagefiles:<br>
`~/foo$ cp ./glfw-meson/glfw.wrap path/to/project/subprojects/glfw.wrap`<br>
`~/foo$ cp -r ./glfw-meson/glfw-patch path/to/project/subprojects/packagefiles`

The main project will automatically pull the correct revision from the glfw repository.

##### Configuration
`meson configure`
`meson configure -D<option>=<value>`
`meson configure -Dglfw:<option>=<value>`
