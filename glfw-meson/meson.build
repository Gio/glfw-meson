#####  GLFW  #####
#@ Project file
project('glfw', 'c'
       , version : '3.3.6'
       , license : 'zlib'
       , default_options : ['default_library=static'
                           ,'b_asneeded=false'
                           ,'b_ndebug=if-release'
                           ,'c_std=c99'
                           ,'warning_level=0'
                           ,'werror=false']
       , meson_version : '>=0.61.0')
#@ Project variables
sys_os = host_machine.system()               #  Returns the OS set in the native or cross configuration file
sys_cc = meson.get_compiler('c')             #  Returns the C compiler set in the native or cross configuration file
prj_sub = meson.is_subproject()              #  Returns TRUE if current build is a subproject

opt_prefix = get_option('prefix')            #  Returns the install path prefix
opt_bindir = get_option('bindir')            #  Returns the binary subdirectory
opt_libdir = get_option('libdir')            #  Returns the library subdirectory
opt_incdir = get_option('includedir')        #  Returns the include subdirectory
opt_datadir = get_option('datadir')          #  Returns the data subdirectory

opt_docs = get_option('build-docs')          #  Build documentation? T/F
opt_tests = get_option('build-tests')        #  Build test programs? T/F
opt_examples = get_option('build-examples')  #  Build example programs? T/F
opt_install = get_option('install')          #  Install GLFW? T/F
opt_display = get_option('display-api')      #  Returns the selected backend API
#@ Build summary
#——TODO:
# ☐ Create OS-specific build summaries
# ☐ Create option summary
#if prj_sub == false                    #  If built as a subproject, silence the build summary
#  if sys_os == 'linux'                 #  Linux and related project summaries
#  summary()
#  endif
#endif


### Dependencies ###
deps = []
#@ Backend API
if opt_display == 'OSMesa'
  #——TODO:
  # ☐ Implement OSMesa build
  error('OSMesa headless-only build is not currently implemented.')
elif opt_display == 'X11'
  foreach l : ['x11', 'xrandr', 'xinerama', 'xkbcommon', 'xcursor', 'xi']
    x_dep = dependency(l, required : false)
    if x_dep.found() == true
      deps += x_dep
    else
      error('Development headers for ' + l + ' not found!')
    endif
  endforeach
elif opt_display == 'Wayland'
  #——TODO:
  # ☐ Implement Wayland build
  warning('Wayland support is experimental & incomplete.')
  error('Wayland build is not currently implemented.')
elif opt_display == 'Win32'
  #——TODO:
  # ☐ Implement Win32 build
  error('Win32 build is not currently implemented.')
elif opt_display == 'Cocoa'
  #——TODO:
  # ☐ Implement Cocoa build
  error('Cocoa build is not currently implemented.')
endif
#@ System Dependencies
#——TODO:
# ☐ Check different OSes for system dependencies
# ☐ Implement system dependencies
if sys_os == 'linux'
  foreach l : ['m', 'rt', 'dl']
    l_dep = sys_cc.find_library(l, required : false)
    if l_dep.found() == true
      deps += l_dep
    endif
  endforeach
endif
deps += dependency('threads')


### Configuration ###
cfg_data = configuration_data()
foreach d : ['OSMesa', 'X11', 'Wayland', 'Win32', 'Cocoa']
	cfg_data.set('_GLFW_' + d.to_upper(), opt_display == d)
endforeach
cfg_file = configure_file(configuration : cfg_data
                         ,output : 'glfw_config.h')


### Targets ###
#@ Install key
I = opt_install
#@ Primary target:
##   GLFW library
#  Common files
s_common = [cfg_file
           ,'src/context.c'
           ,'src/init.c'
           ,'src/input.c'
           ,'src/monitor.c'
           ,'src/vulkan.c'
           ,'src/window.c']
#  Backend files
if opt_display == 'OSMesa'
#——TODO:
# ☐ Implement OSMesa build routine
  s_display = ['src/null_init.c'
              ,'src/null_monitor.c'
              ,'src/null_window.c'
              ,'src/null_joystick.c'
              ,'src/posix_time.c'
              ,'src/posix_thread.c'
              ,'src/osmesa_context.c']
elif opt_display == 'X11'
  s_display = ['src/x11_init.c'
              ,'src/x11_monitor.c'
              ,'src/x11_window.c'
              ,'src/xkb_unicode.c'
              ,'src/posix_time.c'
              ,'src/posix_thread.c'
              ,'src/egl_context.c'
              ,'src/glx_context.c'
              ,'src/osmesa_context.c']
  if sys_os == 'linux'
    s_display += 'src/linux_joystick.c'
  else
    s_display += 'src/null_joystick.c'
  endif
elif opt_display == 'Wayland'
#——TODO:
# ☐ Implement Wayland build routine
  s_display = ['src/wl_init.c'
              ,'src/wl_monitor.c'
              ,'src/wl_window.c'
              ,'src/posix_time.c'
              ,'src/posix_thread.c'
              ,'src/xkb_unicode.c']
  if sys_os == 'linux'
    s_display += 'src/linux_joystick.c'
  else
    s_display += 'src/null_joystick.c'
  endif
elif opt_display == 'Win32'
#——TODO:
# ☐ Implement Win32 build routine
  s_display = ['src/win32_init.c'
              ,'src/win32_joystick.c'
              ,'src/win32_monitor.c'
              ,'src/win32_time.c'
              ,'src/win32_thread.c'
              ,'src/win32_window.c'
              ,'src/wgl_context.c']
elif opt_display == 'Cocoa'
#——TODO:
# ☐ Implement Cocoa build routine
  s_display = ['src/cocoa_init.m'
              ,'src/cocoa_joystick.m'
              ,'src/cocoa_monitor.m'
              ,'src/cocoa_window.m'
              ,'src/cocoa_time.c'
              ,'src/posix_thread.c'
              ,'src/nsgl_context.m']
endif
srcfiles = [s_common, s_display]
incdirs = [include_directories('include'), include_directories('src')]
#  Build
glfw_lib = build_target('glfw3'
                       , srcfiles
                       , c_args : ['-D_GLFW_USE_CONFIG_H']
                       , include_directories : incdirs
                       , dependencies : deps
                       , version : meson.project_version()
                       , build_by_default : true
                       , pic : true
                       , install : I
                       , target_type : 'library')
glfw_dep = declare_dependency(include_directories : incdirs
                             ,link_with : glfw_lib)
#  Headers
if I == true
  install_headers('include/GLFW/glfw3.h'
                 ,'include/GLFW/glfw3native.h'
                 , subdir : 'GLFW')
endif
#@ Secondary target:
##   GLFW documentation
subdir('docs')
#@ Secondary target:
##   Test programs
subdir('tests')
#@ Secondary target:
##   GLFW examples
subdir('examples')


### Post
#@ Subproject
if prj_sub == true
  meson.override_dependency('glfw3', glfw_dep)  #  Overrides any installed GLFW library
endif
#@ Pkg-config
if I == true
  pkg = import('pkgconfig')
  pkg.generate(glfw_lib
              , name : 'GLFW'
              , description : 'A multi-platform library for OpenGL, window, and input'
              , url : 'https://www.glfw.org/'
              , filebase : 'glfw3')
endif
