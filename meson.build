project('raylib', 'c')

raylib_src = files(
  'src/raudio.c',
  'src/rcore.c',
  'src/rglfw.c',
  'src/rmodels.c',
  'src/rshapes.c',
  'src/rtext.c',
  'src/rtextures.c',
  'src/utils.c',
)

raylib_inc = include_directories('src')
rgfw_inc = include_directories('src/external/glfw/include')

os = host_machine.system()
os_is_emscripten = (os == 'emscripten')
os_windows = (os == 'windows')
os_is_linux = (os == 'linux')

c_args = ['-O2']
link_args = []

if os_windows
  link_args += '-lwinmm'
  link_args += '-lgdi32'
  link_args += '-lopengl32'
endif

if os_is_emscripten
  c_args += '-DPLATFORM_WEB'
else
  c_args += '-DPLATFORM_DESKTOP'
endif

if os_is_linux
  c_args += '-D_GLFW_X11'
  c_args += '-fPIC'
endif

raylib_lib = library(
  'raylib',
  raylib_src,
  include_directories: [raylib_inc, rgfw_inc],
  link_args: link_args,
  c_args: c_args,
)

raylib_dep = declare_dependency(
  link_with: raylib_lib,
  link_args: link_args,
  include_directories: [raylib_inc],
)
