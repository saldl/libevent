# NOTE

libevent upstream explicitly disables 'libevent_pthreads' when building
for Windows.

This repository exists for the sole purpose of building pthreads-enabled
libevent with mingw-w64.

Original README moved to `README_libevent.md`.

# Build Instructions

## NOTE

This build only covers what saldl needs. Shared libraries are disabled.
OpenSSL support is disabled. mingw-w64 is the only dependency.

## Win32

    bld_ver="`git describe --dirty`"
    bld_dir="libevent-${bld_ver#release-*}"-win32

    mkdir ${bld_dir}

    ./autogen.sh

    ./configure --prefix='' --host=i686-w64-mingw32 --disable-shared \
                --disable-openssl --disable-samples  --disable-libevent-regress

    make -j3


    make DESTDIR=${PWD}/${bld_dir} install
    zip --recurse-paths ${bld_dir}.zip ${bld_dir}


## Win64

    bld_ver="`git describe --dirty`"
    bld_dir="libevent-${bld_ver#release-*}"-win64

    mkdir ${bld_dir}

    ./autogen.sh

    ./configure --prefix='' --host=x86_64-w64-mingw32 --disable-shared \
                --disable-openssl --disable-samples  --disable-libevent-regress

    make -j3


    make DESTDIR=${PWD}/${bld_dir} install
    zip --recurse-paths ${bld_dir}.zip ${bld_dir}
