# how to build

## Modification for risc-v eyenix
- 
## compile
```bash
cmake --no-warn-unused-cli -DCMAKE_BUILD_TYPE:STRING=Debug -DCMAKE_EXPORT_COMPILE_COMMANDS:BOOL=TRUE -DCMAKE_C_COMPILER:FILEPATH=/opt/riscv/eyenix/bin/riscv64-eyenix-linux-gnu-gcc -DCMAKE_CXX_COMPILER:FILEPATH=/opt/riscv/eyenix/bin/riscv64-eyenix-linux-gnu-g++ -S/home/sungyong/workspace/gitlab/ihancore/v4l2rtspserver -B/home/sungyong/workspace/gitlab/ihancore/v4l2rtspserver/build -G "Unix Makefiles"

cd build
make
```

## usage
```bash
root@en675: build# ./v4l2rtspserver -
./v4l2rtspserver [-v[v]] [-Q queueSize] [-O file]
                  [-I interface] [-P RTSP port] [-p RTSP/HTTP port] [-m multicast url] [-u unicast url] [-M multicast addr] [-c] [-t timeout] [-T] [-S[duration]]
                  [-r] [-w] [-s] [-f[format] [-W width] [-H height] [-F fps] [device] [device]
         -v               : verbose
         -vv              : very verbose
         -Q <length>      : Number of frame queue  (default 5)
         -O <output>      : Copy captured frame to a file or a V4L2 device
         -b <webroot>     : path to webroot
         RTSP/RTP options
         -I <addr>        : RTSP interface (default autodetect)
         -P <port>        : RTSP port (default 8554)
         -p <port>        : RTSP over HTTP port (default 0)
         -U <user>:<pass> : RTSP user and password
         -R <realm>       : use md5 password 'md5(<username>:<realm>:<password>')
         -u <url>         : unicast url (default unicast)
         -m <url>         : multicast url (default multicast)
         -M <addr>        : multicast group:port (default is random_address:20000)
         -c               : don't repeat config (default repeat config before IDR frame)
         -t <timeout>     : RTCP expiration timeout in seconds (default 65)
         -S[<duration>]   : enable HLS & MPEG-DASH with segment duration  in seconds (default 2)
         -x <sslkeycert>  : enable RTSPS & SRTP
         V4L2 options
         -r               : V4L2 capture using read interface (default use memory mapped buffers)
         -w               : V4L2 capture using write interface (default use memory mapped buffers)
         -B               : V4L2 capture using blocking mode (default use non-blocking mode)
         -s               : V4L2 capture using live555 mainloop (default use a reader thread)
         -f               : V4L2 capture using current capture format (-W,-H,-F are ignored)
         -f<format>       : V4L2 capture using format (-W,-H,-F are used)
         -W <width>       : V4L2 capture width (default 0)
         -H <height>      : V4L2 capture height (default 0)
         -F <fps>         : V4L2 capture framerate (default 25)
         -G <w>x<h>[x<f>] : V4L2 capture format (default 0x0x25)
         Devices :
         [V4L2 device][,ALSA device] : V4L2 capture device or/and ALSA capture device (default /dev/video0,/dev/video0)
```

## troubleshooting

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

```bash
```bash
cmake --no-warn-unused-cli -DCMAKE_TOOLCHAIN_FILE=riscv.toolchain -DCMAKE_BUILD_TYPE:STRING=Debug -DCMAKE_EXPORT_COMPILE_COMMANDS:BOOL=TRUE -DCMAKE_C_COMPILER:FILEPATH=/opt/riscv/eyenix/bin/riscv64-eyenix-elf-gcc -DCMAKE_CXX_COMPILER:FILEPATH=/opt/riscv/eyenix/bin/riscv64-eyenix-elf-g++ -S/home/sungyong/workspace/gitlab/ihancore/v4l2rtspserver -B/home/sungyong/workspace/gitlab/ihancore/v4l2rtspserver/build -G "Unix Makefiles"
```
- fail by THREAD

