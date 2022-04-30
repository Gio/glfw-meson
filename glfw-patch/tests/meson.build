###  GLFW test programs
#@ Build check
if opt_tests == false
  subdir_done()
endif

#@ Constants
relpath = '../'
incdirs = [include_directories(relpath + 'include')
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

#@ Test executables
tst_clipboard = build_target('clipboard'
                            , [relpath + 'tests/clipboard.c', getopt, glad_gl]
                            , include_directories : incdirs
                            , dependencies : [glfw_dep, deps]
                            , build_by_default : false
                            , install : false
                            , target_type : 'executable')
tst_events = build_target('events'
                         , [relpath + 'tests/events.c', getopt, glad_gl]
                         , include_directories : incdirs
                         , dependencies : [glfw_dep, deps]
                         , build_by_default : false
                         , install : false
                         , target_type : 'executable')
tst_msaa = build_target('msaa'
                       , [relpath + 'tests/msaa.c', getopt, glad_gl]
                       , include_directories : incdirs
                       , c_args : c_flags
                       , dependencies : [glfw_dep, deps]
                       , build_by_default : false
                       , install : false
                       , target_type : 'executable')
tst_glfwinfo = build_target('glfwinfo'
                           , [relpath + 'tests/glfwinfo.c', getopt, glad_gl, glad_vulkan]
                           , include_directories : incdirs
                           , dependencies : [glfw_dep, deps]
                           , build_by_default : false
                           , install : false
                           , target_type : 'executable')
tst_iconify = build_target('iconify'
                          , [relpath + 'tests/iconify.c', getopt, glad_gl]
                          , include_directories : incdirs
                          , dependencies : [glfw_dep, deps]
                          , build_by_default : false
                          , install : false
                          , target_type : 'executable')
tst_monitors = build_target('monitors'
                           , [relpath + 'tests/monitors.c', getopt, glad_gl]
                           , include_directories : incdirs
                           , dependencies : [glfw_dep, deps]
                           , build_by_default : false
                           , install : false
                           , target_type : 'executable')
tst_reopen = build_target('reopen'
                         , [relpath + 'tests/reopen.c', glad_gl]
                         , include_directories : incdirs
                         , dependencies : [glfw_dep, deps]
                         , build_by_default : false
                         , install : false
                         , target_type : 'executable')
tst_cursor = build_target('cursor'
                         , [relpath + 'tests/cursor.c', glad_gl]
                         , include_directories : incdirs
                         , c_args : c_flags
                         , dependencies : [glfw_dep, deps]
                         , build_by_default : false
                         , install : false
                         , target_type : 'executable')
tst_empty = build_target('empty'
                        , [relpath + 'tests/empty.c', tinycthread, glad_gl]
                        , include_directories : incdirs
                        , dependencies : [glfw_dep, deps]
                        , build_by_default : false
                        , install : false
                        , target_type : 'executable')
tst_gamma = build_target('gamma'
                        , [relpath + 'tests/gamma.c', glad_gl]
                        , include_directories : incdirs
                        , dependencies : [glfw_dep, deps]
                        , build_by_default : false
                        , install : false
                        , target_type : 'executable')
tst_icon = build_target('icon'
                       , [relpath + 'tests/icon.c', glad_gl]
                       , include_directories : incdirs
                       , dependencies : [glfw_dep, deps]
                       , build_by_default : false
                       , install : false
                       , target_type : 'executable')
tst_inputlag = build_target('inputlag'
                           , [relpath + 'tests/inputlag.c', getopt, glad_gl]
                           , include_directories : incdirs
                           , dependencies : [glfw_dep, deps]
                           , build_by_default : false
                           , install : false
                           , target_type : 'executable')
tst_joysticks = build_target('joysticks'
                            , [relpath + 'tests/joysticks.c', glad_gl]
                            , include_directories : incdirs
                            , dependencies : [glfw_dep, deps]
                            , build_by_default : false
                            , install : false
                            , target_type : 'executable')
tst_opacity = build_target('opacity'
                          , [relpath + 'tests/opacity.c', glad_gl]
                          , include_directories : incdirs
                          , dependencies : [glfw_dep, deps]
                          , build_by_default : false
                          , install : false
                          , target_type : 'executable')
tst_tearing = build_target('tearing'
                          , [relpath + 'tests/tearing.c', glad_gl]
                          , include_directories : incdirs
                          , dependencies : [glfw_dep, deps]
                          , build_by_default : false
                          , install : false
                          , target_type : 'executable')
tst_threads = build_target('threads'
                          , [relpath + 'tests/threads.c', tinycthread, glad_gl]
                          , include_directories : incdirs
                          , dependencies : [glfw_dep, deps]
                          , build_by_default : false
                          , install : false
                          , target_type : 'executable')
tst_timeout = build_target('timeout'
                          , [relpath + 'tests/timeout.c', glad_gl]
                          , include_directories : incdirs
                          , dependencies : [glfw_dep, deps]
                          , build_by_default : false
                          , install : false
                          , target_type : 'executable')
tst_title = build_target('title'
                        , [relpath + 'tests/title.c', glad_gl]
                        , include_directories : incdirs
                        , dependencies : [glfw_dep, deps]
                        , build_by_default : false
                        , install : false
                        , target_type : 'executable')
tst_trianglevulkan = build_target('triangle-vulkan'
                                  , [relpath + 'tests/triangle-vulkan.c', glad_vulkan]
                                  , include_directories : incdirs
                                  , dependencies : [glfw_dep, deps]
                                  , build_by_default : false
                                  , install : false
                                  , target_type : 'executable')
tst_windows = build_target('windows'
                          , [relpath + 'tests/windows.c', getopt, glad_gl]
                          , include_directories : incdirs
                          , dependencies : [glfw_dep, deps]
                          , build_by_default : false
                          , install : false
                          , target_type : 'executable')

#@ Build testsuite
# Console test 
test('clipboard'
    , tst_clipboard
    , is_parallel : false
    , suite : ['console', 'glfw'])
test('events'
    , tst_events
    , is_parallel : false
    , suite : ['console', 'glfw'])
test('msaa'
    , tst_msaa
    , is_parallel : false
    , suite : ['console', 'glfw'])
test('glfwinfo'
    , tst_glfwinfo
    , is_parallel : false
    , suite : ['console', 'vulkan', 'glfw'])
test('iconify'
    , tst_iconify
    , is_parallel : false
    , suite : ['console', 'glfw'])
test('monitors'
    , tst_monitors
    , is_parallel : false
    , suite : ['console', 'glfw'])
test('reopen'
    , tst_reopen
    , is_parallel : false
    , suite : ['console', 'glfw'])
test('cursor'
    , tst_cursor
    , is_parallel : false
    , suite : ['console', 'glfw'])

# GUI test suite
test('empty'
    , tst_empty
    , is_parallel : false
    , suite : ['gui', 'glfw'])
test('gamma'
    , tst_gamma
    , is_parallel : false
    , suite : ['gui', 'glfw'])
test('icon'
    , tst_icon
    , is_parallel : false
    , suite : ['gui', 'glfw'])
test('inputlag'
    , tst_inputlag
    , is_parallel : false
    , suite : ['gui', 'glfw'])
test('joysticks'
    , tst_joysticks
    , is_parallel : false
    , suite : ['gui', 'glfw'])
test('opacity'
    , tst_opacity
    , is_parallel : false
    , suite : ['gui', 'glfw'])
test('tearing'
    , tst_tearing
    , is_parallel : false
    , suite : ['gui', 'glfw'])
test('threads'
    , tst_threads
    , is_parallel : false
    , suite : ['gui', 'glfw'])
test('timeout'
    , tst_timeout
    , is_parallel : false
    , suite : ['gui', 'glfw'])
test('title'
    , tst_title
    , is_parallel : false
    , suite : ['gui', 'glfw'])
test('triangle-vulkan'
    , tst_trianglevulkan
    , is_parallel : false
    , suite : ['vulkan'])
test('windows'
    , tst_windows
    , is_parallel : false
    , suite : ['gui', 'glfw'])
