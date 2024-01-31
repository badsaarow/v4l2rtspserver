# how to build

## compile

```bash
export PATH=/opt/riscv/eyenix/bin:$PATH

cmake -DCMAKE_SYSTEM_NAME=Linux -DCMAKE_C_COMPILER=riscv64-linux-gnu-gcc -DCMAKE_CXX_COMPILER=riscv64-linux-gnu-g++ -DCMAKE_FIND_ROOT_PATH_MODE_PROGRAM=NEVER -DCMAKE_FIND_ROOT_PATH_MODE_INCLUDE=ONLY -DCMAKE_FIND_ROOT_PATH_MODE_LIBRARY=ONLY -DCMAKE_FIND_ROOT_PATH_MODE_PACKAGE=ONLY .

make install \
```

error
```bash
CMake Error at CMakeLists.txt:161 (IF):
  if given arguments:

    "STREQUAL" "x86_64"

  Unknown arguments specified
```

```bash

cmake -DCMAKE_SYSTEM_PROCESSOR=x86_64 -DCMAKE_SYSTEM_NAME=Linux -DCMAKE_C_COMPILER=riscv64-linux-gnu-gcc -DCMAKE_CXX_COMPILER=riscv64-linux-gnu-g++ -DCMAKE_FIND_ROOT_PATH_MODE_PROGRAM=NEVER -DCMAKE_FIND_ROOT_PATH_MODE_INCLUDE=ONLY -DCMAKE_FIND_ROOT_PATH_MODE_LIBRARY=ONLY -DCMAKE_FIND_ROOT_PATH_MODE_PACKAGE=ONLY .
```

error
```bash
CMake Error at CMakeLists.txt:161 (IF):
  if given arguments:

    "STREQUAL" "x86_64"

  Unknown arguments specified
```


```bash
cmake --no-warn-unused-cli -DCMAKE_TOOLCHAIN_FILE=riscv.toolchain -DCMAKE_BUILD_TYPE:STRING=Debug -DCMAKE_EXPORT_COMPILE_COMMANDS:BOOL=TRUE -DCMAKE_C_COMPILER:FILEPATH=/usr/bin/riscv64-linux-gnu-gcc -DCMAKE_CXX_COMPILER:FILEPATH=/usr/bin/riscv64-linux-gnu-g++ -S/home/sungyong/workspace/gitlab/ihancore/v4l2rtspserver -B/home/sungyong/workspace/gitlab/ihancore/v4l2rtspserver/build -G "Unix Makefiles"

```

```bash
[  4%] Building CXX object CMakeFiles/libv4l2rtspserver.dir/src/ALSACapture.cpp.o
In file included from /home/sungyong/workspace/gitlab/ihancore/v4l2rtspserver/src/ALSACapture.cpp:16:
/home/sungyong/workspace/gitlab/ihancore/v4l2rtspserver/inc/ALSACapture.h:18:10: fatal error: alsa/asoundlib.h: No such file or directory
   18 | #include <alsa/asoundlib.h>
      |          ^~~~~~~~~~~~~~~~~~
compilation terminated.
make[2]: *** [CMakeFiles/libv4l2rtspserver.dir/build.make:2834: CMakeFiles/libv4l2rtspserver.dir/src/ALSACapture.cpp.o] Error 1
make[1]: *** [CMakeFiles/Makefile2:130: CMakeFiles/libv4l2rtspserver.dir/all] Error 2

```
```bash
sudo pacman -S alsa-lib
```

```bash
/usr/lib/gcc/riscv64-linux-gnu/12.2.0/../../../../riscv64-linux-gnu/bin/ld: cannot find -lstdc++: No such file or directory
collect2: error: ld returned 1 exit status
make[2]: *** [CMakeFiles/v4l2rtspserver.dir/build.make:99: v4l2rtspserver] Error 1
make[1]: *** [CMakeFiles/Makefile2:104: CMakeFiles/v4l2rtspserver.dir/all] Error 2
make: *** [Makefile:166: all] Error 2
```

```bash
cmake --no-warn-unused-cli -DCMAKE_TOOLCHAIN_FILE=riscv.toolchain -DCMAKE_BUILD_TYPE:STRING=Debug -DCMAKE_EXPORT_COMPILE_COMMANDS:BOOL=TRUE -DCMAKE_C_COMPILER:FILEPATH=/opt/riscv/eyenix/bin/riscv64-eyenix-elf-gcc -DCMAKE_CXX_COMPILER:FILEPATH=/opt/riscv/eyenix/bin/riscv64-eyenix-elf-g++ -S/home/sungyong/workspace/gitlab/ihancore/v4l2rtspserver -B/home/sungyong/workspace/gitlab/ihancore/v4l2rtspserver/build -G "Unix Makefiles"
```