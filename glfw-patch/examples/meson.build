###  GLFW examples
#@ Build check
if opt_examples == false
  subdir_done()
endif

#@ Constants
relpath = '../'
exdirs = [include_directories(relpath + 'include')
         ,include_directories(relpath + 'src')
         ,include_directories(relpath + 'deps')]
glad_gl = [relpath + 'deps/glad_gl.c']
glad_vulkan = [relpath + 'deps/glad_vulkan.c']
getopt = [relpath + 'deps/getopt.c']
tinycthread = [relpath + 'deps/tinycthread.c']

#@ Flags
if sys_os == 'linux'
  c_flags = ['-D_XOPEN_SOURCE=700']
endif

#@ Example executables
build_target('offscreen'
            , [relpath + 'examples/offscreen.c', glad_gl]
            , include_directories : exdirs
            , dependencies : [glfw_dep, deps]
            , build_by_default : true
            , install : I
            , install_dir : opt_libdir / 'GLFW'
            , target_type : 'executable')
build_target('boing'
            , [relpath + 'examples/boing.c', glad_gl]
            , include_directories : exdirs
            , c_args : c_flags
            , dependencies : [glfw_dep, deps]
            , build_by_default : true
            , install : I
            , install_dir : opt_libdir / 'GLFW'
            , target_type : 'executable')
build_target('gears'
            , [relpath + 'examples/gears.c', glad_gl]
            , include_directories : exdirs
            , c_args : c_flags
            , dependencies : [glfw_dep, deps]
            , build_by_default : true
            , install : I
            , install_dir : opt_libdir / 'GLFW'
            , target_type : 'executable')
build_target('heightmap'
            , [relpath + 'examples/heightmap.c', glad_gl]
            , include_directories : exdirs
            , dependencies : [glfw_dep, deps]
            , build_by_default : true
            , install : I
            , install_dir : opt_libdir / 'GLFW'
            , target_type : 'executable')
build_target('particles'
            , [relpath + 'examples/particles.c', tinycthread, getopt, glad_gl]
            , include_directories : exdirs
            , c_args : c_flags
            , dependencies : [glfw_dep, deps]
            , build_by_default : true
            , install : I
            , install_dir : opt_libdir / 'GLFW'
            , target_type : 'executable')
build_target('sharing'
            , [relpath + 'examples/sharing.c', glad_gl]
            , include_directories : exdirs
            , dependencies : [glfw_dep, deps]
            , build_by_default : true
            , install : I
            , install_dir : opt_libdir / 'GLFW'
            , target_type : 'executable')
build_target('simple'
            , [relpath + 'examples/simple.c', glad_gl]
            , include_directories : exdirs
            , dependencies : [glfw_dep, deps]
            , build_by_default : true
            , install : I
            , install_dir : opt_libdir / 'GLFW'
            , target_type : 'executable')
build_target('splitview'
            , [relpath + 'examples/splitview.c', glad_gl]
            , include_directories : exdirs
            , c_args : c_flags
            , dependencies : [glfw_dep, deps]
            , build_by_default : true
            , install : I
            , install_dir : opt_libdir / 'GLFW'
            , target_type : 'executable')
build_target('wave'
            , [relpath + 'examples/wave.c', glad_gl]
            , include_directories : exdirs
            , c_args : c_flags
            , dependencies : [glfw_dep, deps]
            , build_by_default : true
            , install : I
            , install_dir : opt_libdir / 'GLFW'
            , target_type : 'executable')
