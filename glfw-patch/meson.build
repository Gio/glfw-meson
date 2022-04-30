#####  GLFW  #####
#@ Project file
project('glfw', 'c'
       , version : '3.3.7'
       , license : 'zlib'
       , default_options : ['default_library=static'
                           ,'b_ndebug=if-release'
                           ,'c_std=c99'
                           ,'warning_level=0'
                           ,'werror=false']
       , meson_version : '>=0.61.0')
#@ Project variables
sys_os = host_machine.system()               #  Returns the OS set in the native or cross configuration file
sys_cc = meson.get_compiler('c')             #  Returns the C compiler set in the native or cross configuration file
msn_ver = meson.version()                    #  Returns the version of Meson in use
prj_xx = meson.is_cross_build()              #  Returns TRUE if the current build is a cross
prj_sub = meson.is_subproject()              #  Returns TRUE if the current build is a subproject
#
opt_prefix = get_option('prefix')            #  Returns the install path prefix
opt_bindir = get_option('bindir')            #  Returns the binary subdirectory
opt_libdir = get_option('libdir')            #  Returns the library subdirectory
opt_incdir = get_option('includedir')        #  Returns the include subdirectory
opt_datadir = get_option('datadir')          #  Returns the data subdirectory
#
opt_docs = get_option('build-docs')          #  Build documentation? T/F
opt_tests = get_option('build-tests')        #  Build test programs? T/F
opt_examples = get_option('build-examples')  #  Build example programs? T/F
opt_install = get_option('install')          #  Install GLFW? T/F
opt_display = get_option('display-api')      #  Returns the selected backend API
#@ Extra variables
if (sys_os == 'dragonfly' or sys_os.str.endswith('bsd'))  #
  bsd = ['bsd']                                           #  Unifies the BSDs in one reference
endif                                                     #
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
#  OSMesa
if opt_display == 'osmesa'
  deps += dependency('osmesa')
#  X11
elif opt_display == 'x11'
  foreach x : ['x11', 'xrandr', 'xinerama', 'xcursor', 'xi', 'xkbcommon']
    deps += dependency(x, required : true)
  endforeach
#  Wayland
elif opt_display == 'wayland'
  warning('Wayland support is experimental & incomplete.')
  warning('GLFW < 3.4 cannot detect Wayland if both x11 and Wayland exist on-system!')
  foreach w : ['wayland-client', 'wayland-cursor', 'wayland-server', 'wayland-egl', 'xkbcommon']
    deps += dependency(w, required : true)
  endforeach
  wl_protocols = dependency('wayland-protocols')
  wl_dir = wl_protocols.get_variable(pkgconfig : 'pkgdatadir')
  wl_scan_dep = dependency('wayland-scanner'
                          , required : false
                          , native : true)
  if wl_scan_dep.found()
    wl_scanner = find_program(wl_scan_dep.get_variable(pkgconfig : 'wayland_scanner'), native : true)
  else
    wl_scanner = find_program('wayland-scanner', native : true)
  endif
  s_wayland = []
  protocols = [['idle-inhibit', 'unstable']
              ,['pointer-constraints', 'unstable']
              ,['relative-pointer', 'unstable']
              ,['viewporter', 'stable']
              ,['xdg-decoration', 'unstable']
              ,['xdg-shell', 'stable']]
  foreach p : protocols
    x_path = join_paths(wl_dir, p[1], p[0], p[0])
    if p[1] == 'stable'
      x_name = p[0]
      xml = files(x_path + '.xml')
    else
      x_name = p[0] + '-unstable-v1'
      xml = files(x_path + '-unstable-v1.xml')
    endif
    foreach f : ['client-header', 'server-header', 'private-code']
      if (f == 'client-header' and p[0] == 'xdg-decoration')
        outfile = 'wayland-' + p[0] + '-client-protocol.h'
      elif f == 'client-header'
        outfile = 'wayland-' + x_name + '-client-protocol.h'
      elif f == 'server-header'
        outfile = 'wayland-' + p[0] + '-server-protocol.h'
      elif (f == 'private-code' and p[0] == 'xdg-decoration')
        outfile = 'wayland-' + p[0] + '-protocol.c'
      else
        outfile = 'wayland-' + x_name + '-protocol.c'
      endif
      s_wayland += custom_target('@0@ @1@'.format(p[0], f)
                               , command : ['wayland-scanner', f, '@INPUT@', '@OUTPUT@']
                               , input : xml
                               , output : outfile)
    endforeach
  endforeach
#  Win32
elif opt_display == 'win32'
  #——TODO:
  # ☐ Implement Win32 build
  error('Win32 build is not currently implemented.')
#  Cocoa
elif opt_display == 'cocoa'
  #——TODO:
  # ☐ Implement Cocoa build
  error('Cocoa build is not currently implemented.')
endif
#@ System Dependencies
if (sys_os == 'linux' or sys_os == 'sunos')
  foreach l : ['m', 'rt', 'dl']
    deps += sys_cc.find_library(l, required : true)
  endforeach
  deps += dependency('threads')
elif sys_os == bsd
  foreach l : ['m', 'rt']
    deps += sys_cc.find_library(l, required : true)
  endforeach
  deps += dependency('threads')
endif


### Configuration ###
cfg_data = configuration_data()
foreach d : ['osmesa', 'x11', 'wayland', 'win32', 'cocoa']
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
if opt_display == 'osmesa'
  s_display = ['src/null_init.c'
              ,'src/null_monitor.c'
              ,'src/null_window.c'
              ,'src/null_joystick.c'
              ,'src/posix_time.c'
              ,'src/posix_thread.c'
              ,'src/osmesa_context.c']
elif opt_display == 'x11'
  s_display = ['src/x11_init.c'
              ,'src/x11_monitor.c'
              ,'src/x11_window.c'
              ,'src/xkb_unicode.c'
              ,'src/posix_time.c'
              ,'src/posix_thread.c'
              ,'src/osmesa_context.c'
              ,'src/egl_context.c'
              ,'src/glx_context.c']
  if sys_os == 'linux'
    s_display += 'src/linux_joystick.c'
  else
    s_display += 'src/null_joystick.c'
  endif
elif opt_display == 'wayland'
  s_display = [s_wayland
              ,'src/wl_init.c'
              ,'src/wl_monitor.c'
              ,'src/wl_window.c'
              ,'src/xkb_unicode.c'
              ,'src/posix_time.c'
              ,'src/posix_thread.c'
              ,'src/osmesa_context.c'
              ,'src/egl_context.c']
  if sys_os == 'linux'
    s_display += 'src/linux_joystick.c'
  else
    s_display += 'src/null_joystick.c'
  endif
elif opt_display == 'win32'
#——TODO:
# ☐ Implement Win32 build routine
  s_display = ['src/win32_init.c'
              ,'src/win32_joystick.c'
              ,'src/win32_monitor.c'
              ,'src/win32_time.c'
              ,'src/win32_thread.c'
              ,'src/win32_window.c'
              ,'src/wgl_context.c']
elif opt_display == 'cocoa'
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
              , description : 'A multi-platform library for OpenGL windows and input'
              , url : 'https://www.glfw.org/'
              , filebase : 'glfw3')
endif
