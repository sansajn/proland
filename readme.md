# About

Fork of [Proland](https://gitlab.inria.fr/neyret/proland) library with SCons build support.

PROLAND LIBRARIES

This directory contains the Proland core library, several "plugins" for
this library, and demos using this library and plugins. Each directory
has its own licence, source tree, examples, documentation and project 
files. The directories are mostly independent, except for some 
dependencies between plugins (and between all the plugins and the core
library).

# Build

Build and install following dependencies *Ork* and *Anttweakbar*.
> TODO: add links to repositories

To build Proland run

```bash
scons -j8
```

command.

Binaries are build in plugins example folder (e.g. `core/examples` or `terrain/examples`, ...).

## Issues

1. libGLEW collision

```
forest/sources/proland/preprocess/trees/PreprocessTreeTables.o -lork -lanttweakbar -lGL -lGLU -lglut -lGLEW -lX11 -ltiff -lpthread
/bin/ld: warning: libGLEW.so.1.5, needed by /usr/local/lib/libork.so, may conflict with libGLEW.so.2.2
/bin/ld: warning: libGLEW.so.1.5, needed by /usr/local/lib/libork.so, may conflict with libGLEW.so.2.2
```

there we want explicitly link against `libGLEW.so.1.5` and not `libGLEW.so.2.2` (by `-lGLEW`)

# Run

```bash
cd core/examples/helloworld
./HelloWorld
```

## Issues

1. `FrameBuffer` error, running sample ends with

```console
$ ./HelloWorld 
INFO [RESOURCE] Loading resource 'defaultScheduler'
INFO [RESOURCE] Loaded file 'helloworld.xml'
INFO [RESOURCE] Loaded file 'helloworld.xml'
INFO [RESOURCE] Loading resource 'scene'
INFO [RESOURCE] Loading resource 'cameraMethod'
INFO [RESOURCE] Loading resource 'myTerrain'
INFO [RESOURCE] Loading resource 'quad.mesh'
INFO [RESOURCE] Loaded file './quad.mesh'
INFO [RESOURCE] Loading resource 'updateTerrainMethod'
INFO [RESOURCE] Loading resource 'drawTerrainMethod'
INFO [RESOURCE] Loading resource 'terrainShader'
INFO [RESOURCE] Loaded file './terrainShader.glsl'
INFO [COMPILER] Compiled module 'terrainShader'
INFO [RESOURCE] Loading resource 'terrainShader;'
ERROR [RENDER] OpenGL error 1282, returned string 'invalid operation'
invalid operation
HelloWorld: ork/render/Program.cpp:660: void ork::Program::initUniforms(): Assertion `FrameBuffer::getError() == 0' failed.
Aborted (core dumped)
```

this is the same issue as in a case of *Ork* samples.

