###  GLFW test programs
#@ Build check
if not get_option('tests')
  subdir_done()
endif

#@ Constants
tst_include = include_directories('../include', '../src', '../deps')
glad_gl = '../deps/glad_gl.c'
glad_vulkan = '../deps/glad_vulkan.c'
getopt = '../deps/getopt.c'
tinycthread = '../deps/tinycthread.c'

#@ Flags
if is_posix
  c_flags = ['-D_XOPEN_SOURCE=700']
else
  c_flags = []
endif

#@ Test executables
tests = [['clipboard', [getopt, glad_gl], 'console'],
         ['events', [getopt, glad_gl], 'console'],
         ['msaa', [getopt, glad_gl], 'console'],
         ['glfwinfo', [getopt, glad_gl, glad_vulkan], ['console', 'vulkan']],
         ['iconify', [getopt, glad_gl], 'console'],
         ['monitors', [getopt, glad_gl], 'console'],
         ['reopen', glad_gl, 'console'],
         ['cursor', glad_gl, 'console'],
         ['empty', [tinycthread, glad_gl], 'gui'],
         ['gamma', glad_gl, 'gui'],
         ['icon', glad_gl, 'gui'],
         ['inputlag', [getopt, glad_gl], 'gui'],
         ['joysticks', glad_gl, 'gui'],
         ['opacity', glad_gl, 'gui'],
         ['tearing', glad_gl, 'gui'],
         ['threads', [tinycthread, glad_gl], 'gui'],
         ['timeout', glad_gl, 'gui'],
         ['title', glad_gl, 'gui'],
         ['triangle-vulkan', glad_vulkan, ['gui', 'vulkan']],
         ['windows', [getopt, glad_gl], 'gui']]
foreach t : tests
  name = t[0]
  src = [t[0] + '.c', t[1]]
  test_id = executable(name, src,
                       include_directories : tst_include,
                       c_args : c_flags,
                       dependencies : [glfw_dep, deps],
                       build_by_default : true,
                       install : I,
                       install_dir : opt_libdir / 'GLFW' / 'tests')
  test(name, test_id,
       is_parallel : false,
       suite : t[2])
endforeach
