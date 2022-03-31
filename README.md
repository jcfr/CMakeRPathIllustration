CMakeRPathIllustration
======================

Small project illustrating how RPath features can be used within CMake

## Experiments

All experiments expect the variable `CMAKE` to be set:

```bash
CMAKE=/path/to/cmake
```

### Default

```bash
EXPERIMENT=default

(rm -rf CMakeRPathIllustration-${EXPERIMENT}-build && \
rm -rf CMakeRPathIllustration-${EXPERIMENT}-install && \
ROOT_DIR=$(pwd) && \
mkdir CMakeRPathIllustration-${EXPERIMENT}-build && cd $_ && \
CMAKE_INSTALL_PREFIX=${ROOT_DIR}/CMakeRPathIllustration-${EXPERIMENT}-install && \
${CMAKE} \
  -DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX} \
  ../CMakeRPathIllustration && \
\
make install && \
\
echo "build tree" && \
otool -L lib/MyWorld/libMyWorld.dylib && \
\
echo "install tree" && \
otool -L ../CMakeRPathIllustration-${EXPERIMENT}-install/lib/MyWorld/libMyWorld.dylib)
```

```bash
build tree
lib/MyWorld/libMyWorld.dylib:
	@rpath/libMyWorld.dylib (compatibility version 0.0.0, current version 0.0.0)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 902.1.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1281.100.1)
install tree
../CMakeRPathIllustration-default-install/lib/MyWorld/libMyWorld.dylib:
	@rpath/libMyWorld.dylib (compatibility version 0.0.0, current version 0.0.0)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 902.1.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1281.100.1)
```

## CMAKE_INSTALL_NAME_DIR set to value of CMAKE_INSTALL_PREFIX

```bash
EXPERIMENT=experiment1

(rm -rf CMakeRPathIllustration-${EXPERIMENT}-build && \
rm -rf CMakeRPathIllustration-${EXPERIMENT}-install && \
ROOT_DIR=$(pwd) && \
mkdir CMakeRPathIllustration-${EXPERIMENT}-build && cd $_ && \
CMAKE_INSTALL_PREFIX=${ROOT_DIR}/CMakeRPathIllustration-${EXPERIMENT}-install && \
${CMAKE} \
  -DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX} \
  -DCMAKE_INSTALL_NAME_DIR:PATH=${CMAKE_INSTALL_PREFIX} \
  ../CMakeRPathIllustration && \
\
make install && \
\
echo "build tree" && \
otool -L lib/MyWorld/libMyWorld.dylib && \
\
echo "install tree" && \
otool -L ../CMakeRPathIllustration-${EXPERIMENT}-install/lib/MyWorld/libMyWorld.dylib)
```

```bash
build tree
lib/MyWorld/libMyWorld.dylib:
	@rpath/libMyWorld.dylib (compatibility version 0.0.0, current version 0.0.0)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 902.1.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1281.100.1)
install tree
../CMakeRPathIllustration-experiment1-install/lib/MyWorld/libMyWorld.dylib:
	/tmp/CMakeRPathIllustration-experiment1-install/libMyWorld.dylib (compatibility version 0.0.0, current version 0.0.0)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 902.1.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1281.100.1)
```

## CMAKE_INSTALL_NAME_DIR set to value of CMAKE_INSTALL_PREFIX, CMAKE_MACOSX_RPATH set to OFF

```bash
EXPERIMENT=experiment2

(rm -rf CMakeRPathIllustration-${EXPERIMENT}-build && \
rm -rf CMakeRPathIllustration-${EXPERIMENT}-install && \
ROOT_DIR=$(pwd) && \
mkdir CMakeRPathIllustration-${EXPERIMENT}-build && cd $_ && \
CMAKE_INSTALL_PREFIX=${ROOT_DIR}/CMakeRPathIllustration-${EXPERIMENT}-install && \
${CMAKE} \
  -DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_INSTALL_PREFIX} \
  -DCMAKE_INSTALL_NAME_DIR:PATH=${CMAKE_INSTALL_PREFIX} \
  -DCMAKE_MACOSX_RPATH:BOOL=OFF \
  ../CMakeRPathIllustration && \
\
make install && \
\
echo "build tree" && \
otool -L lib/MyWorld/libMyWorld.dylib && \
\
echo "install tree" && \
otool -L ../CMakeRPathIllustration-${EXPERIMENT}-install/lib/MyWorld/libMyWorld.dylib)
```

```bash
build tree
lib/MyWorld/libMyWorld.dylib:
	/tmp/CMakeRPathIllustration-experiment2-build/lib/MyWorld/libMyWorld.dylib (compatibility version 0.0.0, current version 0.0.0)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 902.1.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1281.100.1)
install tree
../CMakeRPathIllustration-experiment2-install/lib/MyWorld/libMyWorld.dylib:
	/tmp/CMakeRPathIllustration-experiment2-install/libMyWorld.dylib (compatibility version 0.0.0, current version 0.0.0)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 902.1.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1281.100.1)
```

## License

This software is licensed under the terms of the [Apache Licence Version 2.0](LICENSE).

The license file was added at revision 1e7156b on 2022-03-31, but you may consider that the license applies to all prior revisions as well.
