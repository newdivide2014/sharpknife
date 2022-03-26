Linux inotify详解
https://blog.csdn.net/breakout_alex/article/details/89028868

```c++
int fd = inotify_init ();
int wd = inotify_add_watch (fd, path, mask);
int ret = inotify_rm_watch (fd, wd);
```
https://blog.csdn.net/daiyudong2020/article/details/51695502
==https://blog.csdn.net/u011279649/article/details/52016555==
==https://blog.csdn.net/liuhengxiao/article/details/44171697==
IN_IGNORED：监控被显式移除（调用inotify_rm_watch()），或者自动移除（文件被删除或者文件系统被卸载）
https://blog.csdn.net/hanjw05/article/details/53860132
IN_ALL_EVENTS	以上所有flag的集合

---

加密原始文件
`sh ../bmgjx/bin/dae_bmgjx.sh 8 /test/123.key userauth.txt userauth.txt.enc 1`

编译加密解密调用openssl
` g++ zbtest.cpp -I/usr/local/ssl/include -lssl -lcrypto -ldl -L/usr/local/ssl/lib  -I. -L/work/bmgjx/lib/  -lcryptokeymgr`

` g++ Untitled-1.cpp  -I/usr/local/ssl/include -lssl -lcrypto -ldl -L/usr/local/ssl/lib  -I. -L/work/bmgjx/lib/  -lcryptokeymgr`

---
```sh
 C++: munmap_chunk(): invalid pointer
```

2017年2月22日 中午
 336 字  1 分钟
指针问题绝对是C++ 中最令人头疼的问题之一。 最近在写一个程序，编译通过，运行的时候出现这个错误。很明显是指针的问题，并且确定是在 delete[] 一个指针的时候发生的错误（可以用gdb调试进行错误定位），但就是不知道问题出在哪儿。网上基本给出两种意见：

指针在运行过程中被修改。
指针在delete[] （free）之前已经被 delete[] （free）过了。
仔细检查之后发现并不存在这俩问题。最后经过逐行排查，发现是在给指针所指向的数组赋值的时候访问越界，给超过边界的内存赋值。但是访问越界的时候不会直接报出错误，等到delete的时候程序认为指针已经被修改了（所指向的内存发生了变化），所以会报错。这么来看这个问题本质上还是属于上面提到的第一种，只是比较隐蔽和直觉相悖，难以发现。

访问指针也有可能修改指针的，切记。

常见指针错误一定要熟悉并尽可能避免，详细总结可参考下面文章：

参考链接：

C/C++常见指针错误 and 内存访问越界

 C/C++
 Bug C++
如果你对本文有任何疑问或建议，欢迎联系我。本博客所有文章除特别声明外，均为原创文章，未经授权请勿转载！

---

ninja
https://ninja-build.org/
build from source:

```bash
git clone git://github.com/ninja-build/ninja.git && cd ninja
git checkout release
cat README.md
./configure.py --bootstrap
```

This will generate the `ninja` binary and a `build.ninja` file you can now use
to build Ninja with itself.

 CMake

```
cmake -Bbuild-cmake -H.
cmake --build build-cmake
```

---

google
```sh
fipscheck-1.4.1-6.el7.aarch64 has missing requires of fipscheck-lib(aarch-64) = ('0', '1.4.1', '6.el7')
fipscheck-1.4.1-6.el7.aarch64 has missing requires of libfipscheck.so.1()(64bit)
newt-0.52.15-4.el7.aarch64 has missing requires of libslang.so.2()(64bit)
newt-0.52.15-4.el7.aarch64 has missing requires of libslang.so.2(SLANG2)(64bit)
nss-sysinit-3.36.0-7.1.el7_6.aarch64 has missing requires of nss = ('0', '3.36.0', '7.1.el7_6')
nss-tools-3.36.0-7.1.el7_6.aarch64 has missing requires of nss(aarch-64) = ('0', '3.36.0', '7.1.el7_6')
p11-kit-trust-0.23.5-3.el7.aarch64 has missing requires of libtasn1.so.6()(64bit)
p11-kit-trust-0.23.5-3.el7.aarch64 has missing requires of libtasn1.so.6(LIBTASN1_0_3)(64bit)
4:perl-5.16.3-294.el7_6.aarch64 has missing requires of perl(threads::shared)
polkit-pkla-compat-0.1-4.el7.aarch64 has missing requires of libpolkit-gobject-1.so.0()(64bit)
pygpgme-0.3-9.el7.aarch64 has missing requires of libgpgme.so.11()(64bit)
pygpgme-0.3-9.el7.aarch64 has missing requires of libgpgme.so.11(GPGME_1.0)(64bit)
pygpgme-0.3-9.el7.aarch64 has missing requires of libgpgme.so.11(GPGME_1.1)(64bit)
rpm-build-libs-4.11.3-35.el7.aarch64 has missing requires of rpm-libs(aarch-64) = ('0', '4.11.3', '35.el7')
yum-3.4.3-161.el7.centos.noarch has missing requires of yum-metadata-parser >= ('0', '1.1.0', None)
yum-3.4.3-161.el7.centos.noarch has missing requires of yum-plugin-fastestmirror
Error: check all
```



libcom_err-devel.aarch64 
 su -c 'yum install fipscheck-lib.aarch64  pinentry.aarch64  libcom_err.aarch64'

libtasn1
polkit-pkla-compat
rpm-build-libs
yum install polkit

---
fipscheck-1.4.1-6.el7.aarch64 has missing requires of fipscheck-lib(aarch-64) = ('0', '1.4.1', '6.el7')
fipscheck-1.4.1-6.el7.aarch64 has missing requires of libfipscheck.so.1()(64bit)
newt-0.52.15-4.el7.aarch64 has missing requires of libslang.so.2()(64bit)
newt-0.52.15-4.el7.aarch64 has missing requires of libslang.so.2(SLANG2)(64bit)
nss-sysinit-3.36.0-7.1.el7_6.aarch64 has missing requires of nss = ('0', '3.36.0', '7.1.el7_6')
nss-tools-3.36.0-7.1.el7_6.aarch64 has missing requires of nss(aarch-64) = ('0', '3.36.0', '7.1.el7_6')
p11-kit-trust-0.23.5-3.el7.aarch64 has missing requires of libtasn1.so.6()(64bit)
p11-kit-trust-0.23.5-3.el7.aarch64 has missing requires of libtasn1.so.6(LIBTASN1_0_3)(64bit)
4:perl-5.16.3-294.el7_6.aarch64 has missing requires of perl(threads::shared)
polkit-pkla-compat-0.1-4.el7.aarch64 has missing requires of libpolkit-gobject-1.so.0()(64bit)
pygpgme-0.3-9.el7.aarch64 has missing requires of libgpgme.so.11()(64bit)
pygpgme-0.3-9.el7.aarch64 has missing requires of libgpgme.so.11(GPGME_1.0)(64bit)
pygpgme-0.3-9.el7.aarch64 has missing requires of libgpgme.so.11(GPGME_1.1)(64bit)
rpm-build-libs-4.11.3-35.el7.aarch64 has missing requires of rpm-libs(aarch-64) = ('0', '4.11.3', '35.el7')
yum-3.4.3-161.el7.centos.noarch has missing requires of yum-metadata-parser >= ('0', '1.1.0', None)
yum-3.4.3-161.el7.centos.noarch has missing requires of yum-plugin-fastestmirror
Error: check all




libcom_err-devel.aarch64 
 su -c 'yum install fipscheck-lib.aarch64  pinentry.aarch64  libcom_err.aarch64'

libtasn1
polkit-pkla-compat
rpm-build-libs
yum install polkit

---

 git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
 export PATH="$PATH:/path/to/depot_tools"

 fetch --nohooks chromium
 git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
 export PATH="$PATH:/path/to/depot_tools"

 fetch --nohooks --no-history chromium


 1.报错：
depot_tools/bootstrap_python3: 行 32: bootstrap-3.8.0.chromium.8_bin/python3/bin/python3: 没有那个文件或目录

2.解决：

emacs  depot_tools/bootstrap_python3

-BOOTSTRAP_PYTHON_BIN="${BOOTSTRAP_PATH}/python3/bin/python3"
+BOOTSTRAP_PYTHON_BIN="/usr/bin/python3"

---
Alternatively, you can build GN from source with a C++17 compiler:

    git clone https://gn.googlesource.com/gn
    cd gn
    python build/gen.py
    ninja -C out
    # To run tests:
    out/gn_unittests



ninja: no work to do.
ERROR at //printing/BUILD.gn:411:14: Script returned non-zero exit code.
      libs = exec_script("cups_config_helper.py",
             ^----------
Current dir: /work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/
Command: python /work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/printing/cups_config_helper.py --libs-for-gn /work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/build/linux/debian_sid_arm64-sysroot
Returned 1 and printed out:

cups-config not found: /work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/build/linux/debian_sid_arm64-sysroot/usr/bin/cups-config


[root@localhost gn]# find /work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/ -name cups-config      
/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/printing/usr/bin/cups-config


subprocess.check_call(['tar', 'xf', tarball, '-C', sysroot])

/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/Debug/gn gen /work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/Debug --args='target_cpu="arm64″' --root=/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212

[root@localhost gn]# ./bootstrap/bootstrap.py   -s --gn-gen-args=' custom_toolchain="//build/arm64"'  --build-path=out/

**************************************
/work/bao/git/devrte/runtime/gcc-9.2.0/bin/g++
****************************************
ninja: Entering directory `/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/gn_build'
ninja: no work to do.
ERROR Unresolved dependencies.
//:gn_all(//build/toolchain/linux:clang_arm64)
  needs //printing:printing_unittests(//build/toolchain/linux:clang_arm64)

Traceback (most recent call last):
  File "./bootstrap/bootstrap.py", line 139, in <module>
    sys.exit(main(sys.argv[1:]))
  File "./bootstrap/bootstrap.py", line 133, in main
    '--args=%s' % gn_gen_args, "--root=" + SRC_ROOT
  File "/usr/lib64/python2.7/subprocess.py", line 542, in check_call
    raise CalledProcessError(retcode, cmd)
subprocess.CalledProcessError: Command '['/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/gn', 'gen', '/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/', '--args= is_debug=false', '--root=/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212']' returned non-zero exit status 1

注释掉这俩行
[root@localhost chromium-90.0.4430.212]# grep -rn "\/\/printing:printing_unittests"
BUILD.gn:153:      "//printing:printing_unittests",
BUILD.gn:914:      "//printing:printing_unittests",

/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/gn gen out/Default



['/path/to/depot_tools', '/usr/lib64/python36.zip', '/usr/lib64/python3.6', '/usr/lib64/python3.6/lib-dynload', '/usr/local/lib/python3.6/site-packages', '/usr/lib64/python3.6/site-packages', '/usr/lib/python3.6/site-packages'] /path/to/depot_tools/ninja -C out/Default chrome -j 18

/path/to/depot_tools /usr/lib64/python36.zip /usr/lib64/python3.6 /usr/lib64/python3.6/lib-dynload   /usr/local/lib/python3.6/site-packages /usr/lib64/python3.6/site-packages   /usr/lib/python3.6/site-packages  /work/bao/git/ninja/ninja -C out/Default chrome -j 18


/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/gn gen out/Default/ --args=' custom_toolchain="//build/arm64"'


 autoninja -C out/Default chrome



gcc: error: unrecognized command line option ‘-mllvm’        yum install llvm-devel
gcc: error: find-bad-constructs: No such file or directory   clang_use_chrome_plugins=false


./configure --prefix=/work/bao/git/test/gcc-install/  \
--enable-bootstrap --enable-shared --enable-threads=posix --enable-checking=release \
--enable-multilib --with-system-zlib --enable-__cxa_atexit --enable-libunwind-exceptions --enable-gnu-unique-object --enable-linker-build-id \
--enable-languages=c,c++ \
--enable-plugin --enable-initfini-array --disable-libgcj --enable-gnu-indirect-function 

./configure -enable-languages=c,c++ -enbale-multilib -enable-checking=release


Arm Config for build
源码路径：
src/build/config/arm.gni

../../base/third_party/libevent/buffer.c:42:10: fatal error: sys/types.h: No such file or directory
   42 | #include <sys/types.h>
此时想到 gn 的编译往往不用系统的运行时库，而是依赖 chromium 仓库中独立的库。
在 buildtools/third_party/libc++/ 目录下找到了其 BUILD.gn 文件，从而追踪到了 locale.o 的源文件 locale.cpp，在该文件中添加 iswblank 的一行测试代码导致编译失败，此时可以看到编译 release 的详细参数：
————————————————
版权声明：本文为CSDN博主「kph_Hajash」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/chuanglan/article/details/103724473/

arm-linux-gnueabihf

./build/linux/debian_sid_arm-sysroot/usr/include/arm-linux-gnueabihf/


vi out/Default/args.gn

      1 custom_toolchain = "//build/arm64"
      2
      3 current_os = "linux"
      4 current_cpu = "arm64"
      5 is_clang = false
      7 enable_nacl=false
      8 is_debug=false
      9 symbol_level=0
     10 is_component_build=true
     11 use_sysroot = false

-mfloat-abi=hard

build/config/compiler/BUILD.gn:844:          "-mfloat-abi=$arm_float_abi",
build/config/compiler/BUILD.gn:1104:          "-mfloat-abi=hard",


    850     } else if (current_cpu == "arm64") {
    851       if (is_clang && !is_android && !is_nacl && !is_fuchsia) {
    852         cflags += [ "--target=aarch64-linux-gnu"]
    853         ldflags += [ "--target=aarch64-linux-gnu" ]
    854       }
    855       if (!is_nacl) {               add this
    856         cflags += [                add this
    857           # "-march=$arm_arch",    add this
    858           "-mfloat-abi=hard",      add this
    859         ]                          add this
    860       }

gnu/stubs.h

```c++
/* This file selects the right generated file of `__stub_FUNCTION' macros
  based on the architecture being compiled for. */

#include <bits/wordsize.h>

#if __WORDSIZE == 32
# include <gnu/stubs-32.h>
#elif __WORDSIZE == 64
# include <gnu/stubs-64.h>
#els
# error "unexpected value for __WORDSIZE macro"
#endif
~    
```



```sh
FAILED: obj/base/base_static/base_switches.o
/work/bao/git/devrte/runtime/gcc-9.2.0/bin/g++ -MMD -MF obj/base/base_static/base_switches.o.d -DUSE_UDEV -DUSE_AURA=1 -DUSE_GLIB=1 -DUSE_NSS_CERTS=1 -DUSE_OZONE=1 -DUSE_X11=1 -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE -D_LARGEFILE64_SOURCE -D__STDC_CONSTANT_MACROS -D__STDC_FORMAT_MACROS -D_FORTIFY_SOURCE=2 -DCOMPONENT_BUILD -D_LIBCPP_ABI_UNSTABLE -D_LIBCPP_ABI_VERSION=Cr -D_LIBCPP_ENABLE_NODISCARD -D_LIBCPP_HAS_NO_VENDOR_AVAILABILITY_ANNOTATIONS -DCR_LIBCXX_REVISION=8fa87946779682841e21e2da977eccfb6cb3bded -DCR_SYSROOT_HASH=d20fa0b1c7afe1e67272c9c67837d080ca30d18f -DNDEBUG -DNVALGRIND -DDYNAMIC_ANNOTATIONS_ENABLED=0 -I../.. -Igen -fno-strict-aliasing --param=ssp-buffer-size=4 -fstack-protector -funwind-tables -fPIC -pipe -pthread -Wno-builtin-macro-redefined -D__DATE__= -D__TIME__= -D__TIMESTAMP__= -Wall -Werror -Wno-unused-local-typedefs -Wno-maybe-uninitialized -Wno-deprecated-declarations -Wno-comments -Wno-packed-not-aligned -Wno-missing-field-initializers -Wno-unused-parameter -fno-omit-frame-pointer -g0 -fno-builtin-abs -fvisibility=hidden -O2 -fno-ident -fdata-sections -ffunction-sections -std=gnu++14 -Wno-narrowing -Wno-class-memaccess -fno-exceptions -fno-rtti -nostdinc++ -isystem../../buildtools/third_party/libc++/trunk/include -isystem../../buildtools/third_party/libc++abi/trunk/include --sysroot=../../build/linux/debian_sid_arm64-sysroot -fvisibility-inlines-hidden -c ../../base/base_switches.cc -o obj/base/base_static/base_switches.o
In file included from ../../build/linux/debian_sid_arm64-sysroot/usr/include/features.h:485,
                 from ../../build/linux/debian_sid_arm64-sysroot/usr/include/unistd.h:25,
                 from ../../build/build_config.h:70,
                 from ../../base/base_switches.h:10,
                 from ../../base/base_switches.cc:5:
../../build/linux/debian_sid_arm64-sysroot/usr/include/gnu/stubs.h:7:11: fatal error: gnu/stubs-soft.h: No such file or directory
```
```c++
7 | # include <gnu/stubs-soft.h>
```

Local changes:
     14 - Copied buildtools/third_party/libc++/trunk/src/include/refstring.h to
     15   buildtools/third_party/libc++abi/libcxx/src/include/refstring.h to work
     16   around https://llvm.org/PR49313
~

./build/linux/debian_sid_arm64-sysroot/usr/include/gnu/stubs.h +7
```c++
      6 #if !defined __ARM_PCS_VFP
      7 //# include <gnu/stubs-soft.h>              delete this
      8 #endif
      9 #if defined __ARM_PCS_VFP
     10 # include <gnu/stubs-hard.h>
     11 #endif
```
```sh
 error: cast from ‘const char*’ to ‘std::__type_info_implementations::__non_unique_arm_rtti_bit_impl::__type_name_t’ {aka ‘unsigned int’} loses precision [-fpermissive]
  238 |       return reinterpret_cast<__type_name_t>(__v);

   error: cast from ‘const char*’ to {aka ‘unsigned int’} loses precision [-fpermissive] reinterpret_cast
```
   build/config/sysroot.gni +42
vi out/Default/args.gn 
add this
use_sysroot = true
```c++
typedef uintptr_t __type_name_t;
    230
    231     _LIBCPP_INLINE_VISIBILITY _LIBCPP_ALWAYS_INLINE
    232     static const char* __type_name_to_string(__type_name_t __v) _NOEXCEPT {
    233       return reinterpret_cast<const char*>(__v &
    234           ~__non_unique_rtti_bit::value);
    235     }
    236     _LIBCPP_INLINE_VISIBILITY _LIBCPP_ALWAYS_INLINE
    237     static __type_name_t __string_to_type_name(const char* __v) _NOEXCEPT {
    238       return reinterpret_cast<__type_name_t>(__v);
    239     }
```

buildtools/third_party/libc++/trunk/include/typeinfo:155:
```c++
// This implementation of type_info does not assume always a unique copy of
    148 // the RTTI for a given type inside a program. It packs the pointer to the
    149 // type name into a uintptr_t and reserves the high bit of that pointer (which
    150 // is assumed to be free for use under the ABI in use) to represent whether
    151 // that specific copy of the RTTI can be assumed unique inside the program.
    152 // To implement equality-comparison of type_infos, we check whether BOTH
    153 // type_infos are guaranteed unique, and if so, we simply compare the addresses
    154 // of their type names instead of doing a deep string comparison, which is
    155 // faster. If at least one of the type_infos can't guarantee uniqueness, we
    156 // have no choice but to fall back to a deep string comparison.
    157 //
    158 // This implementation is specific to ARM64 on Apple platforms.
    159 //
    160 // Note that the compiler is the one setting (or unsetting) the high bit of
    161 // the pointer when it constructs the type_info, depending on whether it can
    162 // guarantee uniqueness for that specific type_info.
    163
    164 // This value can be overriden in the __config_site. When it's not overriden,
    165 // we pick a default implementation based on the platform here.


    228   struct __non_unique_arm_rtti_bit_impl {
    229     //typedef uintptr_t __type_name_t;
    230     typedef unsigned long __type_name_t;             change this
    231
    232     _LIBCPP_INLINE_VISIBILITY _LIBCPP_ALWAYS_INLINE
    233     static const char* __type_name_to_string(__type_name_t __v) _NOEXCEPT {
    234       return reinterpret_cast<const char*>(__v &
    235           ~__non_unique_rtti_bit::value);
    236     }
    237     _LIBCPP_INLINE_VISIBILITY _LIBCPP_ALWAYS_INLINE
    238     static __type_name_t __string_to_type_name(const char* __v) _NOEXCEPT {
    239       return reinterpret_cast<__type_name_t>(__v);
    240     }
```

atk pangocairo
yum install pango-devel
yum install cairo-devel

atk-bridge-2.0
atk-bridge-2.0 API由at-spi2-atk提供，而不是由ATK提供
yum install at-spi2-atk-devel

gtk+-3.0
yum install gtk3-devel

libgbm
yum install mesa-libgbm-devel

/usr/bin/ld.gold: warning: ignoring --threads: /usr/bin/ld.gold was compiled without thread support
/usr/bin/ld.gold: warning: ignoring --thread-count: /usr/bin/ld.gold was compiled without thread support
vi build/config/compiler/BUILD.gn
  64   # Enable fatal linker warnings. Building Chromium with certain versions
     65   # of binutils can cause linker warning.
     66   # TODO(thakis): Set this to true unconditionally once lld/MachO bring-up
     67   # is along far enough that it no longer emits linker warnings.
     68   fatal_linker_warnings = !(is_apple && use_lld)

---
```
FAILED: obj/v8/cppgc_base/heap-consistency.o
...
In file included from ../../v8/include/cppgc/heap-state.h:8:0,
                 from ../../v8/include/cppgc/internal/write-barrier.h:8,
                 from ../../v8/include/cppgc/heap-consistency.h:10,
                 from ../../v8/src/heap/cppgc/heap-consistency.cc:5:
../../v8/include/v8config.h:466:22: error: expected identifier before ‘[’ token
 #define V8_NODISCARD [[nodiscard]]
```
里面有c++17的语法
vi ./v8/include/v8config.h +466

```c++
 // Annotate a class or constructor indicating the caller must assign the
 // constructed instances.
 // Apply to the whole class like:
 //   class V8_NODISCARD Foo() { ... };
 // or apply to just one constructor like:
 //   V8_NODISCARD Foo() { ... };
 // [[nodiscard]] comes in C++17 but supported in clang with -std >= c++11.
 //#if V8_HAS_CPP_ATTRIBUTE_NODISCARD                //注释掉了这三行
 //#define V8_NODISCARD [[nodiscard]]
 //#else
```
---




```sh
In file included from /usr/include/string.h:636,
                 from ../../buildtools/third_party/libc++/trunk/include/string.h:60,
                 from ../../buildtools/third_party/libc++/trunk/include/cstring:60,
                 from ../../buildtools/third_party/libc++/trunk/include/utility:203,
                 from ../../buildtools/third_party/libc++/trunk/include/memory:674,
                 from ../../buildtools/third_party/libc++/trunk/include/functional:511,
                 from ../../third_party/perfetto/include/perfetto/ext/base/thread_task_runner.h:20,
                 from ../../third_party/perfetto/src/base/thread_task_runner.cc:19:
In function ‘char* strncpy(char*, const char*, size_t)’,
    inlined from ‘bool perfetto::base::MaybeSetThreadName(const string&)’ at ../../third_party/perfetto/include/perfetto/ext/base/thread_utils.h:50:10,
    inlined from ‘void perfetto::base::ThreadTaskRunner::RunTaskThread(std::__Cr::function<void(perfetto::base::UnixTaskRunner*)>)’ at ../../third_party/perfetto/src/base/thread_task_runner.cc:85:29:
/usr/include/bits/string3.h:120:34: error: ‘char* __builtin___strncpy_chk(char*, const char*, long unsigned int, long unsigned int)’ output may be truncated copying between 1 and 15 bytes from a string of length 22 [-Werror=stringop-truncation]
  120 |   return __builtin___strncpy_chk (__dest, __src, __len, __bos (__dest));
      |          ~~~~~~~~~~~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
cc1plus: all warnings being treated as errors
```
```gn
   1630 # chromium_code ---------------------------------------------------------------
   1631 #
   1632 # Toggles between higher and lower warnings for code that is (or isn't)
   1633 # part of Chromium.
   1634
   1635 config("chromium_code") {
   1636   if (is_win) {
   1637     cflags = [ "/W4" ]  # Warning level 4.
   1638
   1639     if (is_clang) {
   1640       # Opt in to additional [[nodiscard]] on standard library methods.
   1641       defines = [ "_HAS_NODISCARD" ]
   1642     }
   1643   } else {
   1644     cflags = [ "-Wall" ]
   1645     if (treat_warnings_as_errors) {

######    1646       # cflags += [ "-Werror" ]                                ==change this==
```

./third_party/llvm/compiler-rt/lib/sanitizer_common/sanitizer_stoptheworld_linux_libcdep.cpp:38:#include <sys/user.h>  // for user_regs_struct


/usr/include/user.h
```c
      1 /* Copyright (C) 2009-2020 Free Software Foundation, Inc.
      2
      3    This file is part of the GNU C Library.
      4
      5    The GNU C Library is free software; you can redistribute it and/or
      6    modify it under the terms of the GNU Lesser General Public License as
      7    published by the Free Software Foundation; either version 2.1 of the
      8    License, or (at your option) any later version.
      9
     10    The GNU C Library is distributed in the hope that it will be useful,
     11    but WITHOUT ANY WARRANTY; without even the implied warranty of
     12    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
     13    Lesser General Public License for more details.
     14
     15    You should have received a copy of the GNU Lesser General Public
     16    License along with the GNU C Library; if not, see
     17    <https://www.gnu.org/licenses/>.  */
     18
     19 #ifndef _SYS_USER_H
     20 #define _SYS_USER_H     1
     21
     22 struct user_regs_struct
     23 {
     24   unsigned long long regs[31];
     25   unsigned long long sp;
     26   unsigned long long pc;
     27   unsigned long long pstate;
     28 };
     29
     30 struct user_fpsimd_struct
     31 {
     32   __uint128_t  vregs[32];
     33   unsigned int fpsr;
     34   unsigned int fpcr;
     35 };
     36
     37 #endif
```

---

没有`node`
```
python  ./third_party/node/node.py  ./third_party/devtools-frontend/src/scripts/build/ninja/copy-files.js /work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/third_party/devtools-frontend/src/front_end /work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/Default/gen/third_party/devtools-frontend/src/front_end Tests.js,devtools_compatibility.js

['../../third_party/node/linux/node-linux-x64/bin/node', '../../third_party/node/node_modules/rollup/dist/bin/rollup', '/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/Default/gen/chrome/browser/resources/extensions/preprocessed/extensions.js', '--format', 'esm', '--dir', '/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/Default/gen/chrome/browser/resources/extensions/tmpNyLw74', '--entryFileNames', '[name].rollup.js', '--sourcemap', '--sourcemapExcludeSources', '--config', '/work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/out/Default/gen/chrome/browser/resources/extensions/tmpNyLw74/rollup.config.js', '--silent']
```
### node不能用

```c++
     13 def GetBinaryPath():
     14   return os_path.join(os_path.dirname(__file__), *{
     15     'Darwin': ('mac', 'node-darwin-x64', 'bin', 'node'),
     16     # 'Linux': ('linux', 'node-linux-x64', 'bin', 'node'),     ==change this==
     17     'Linux': ('linux', 'node', 'bin', 'node'),
     18     'Windows': ('win', 'node.exe'),
     19   }[platform.system()])
     20
```
```sh
ln -sf /work/bao/git/node-v10.16.3-linux-arm64/bin/node /work/bao/chromium/chrom_unrpm/chromium-90/chromium-90.0.4430.212/third_party/node/linux/node/bin/
```
```
FAILED: obj/v8/v8_cppgc_shared/push_registers_asm.o
/work/bao/git/test/gcc-install/bin/g++ -MMD -MF obj/v8/v8_cppgc_shared/push_registers_asm.o.d -DUSE_UDEV -DUSE_AURA=1 -DUSE_GLIB=1 -DUSE_NSS_CERTS=1 -DUSE_OZONE=1 -DUSE_X11=1 -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE -D_LARGEFILE64_SOURCE -D__STDC_CONSTANT_MACROS -D__STDC_FORMAT_MACROS -D_FORTIFY_SOURCE=2 -DCOMPONENT_BUILD -D_LIBCPP_ABI_UNSTABLE -D_LIBCPP_ABI_VERSION=Cr -D_LIBCPP_ENABLE_NODISCARD -D_LIBCPP_HAS_NO_VENDOR_AVAILABILITY_ANNOTATIONS -DCR_LIBCXX_REVISION=8fa87946779682841e21e2da977eccfb6cb3bded -DNDEBUG -DNVALGRIND -DDYNAMIC_ANNOTATIONS_ENABLED=0 -DV8_TYPED_ARRAY_MAX_SIZE_IN_HEAP=64 -DENABLE_MINOR_MC -DV8_INTL_SUPPORT -DV8_USE_EXTERNAL_STARTUP_DATA -DV8_ATOMIC_OBJECT_FIELD_WRITES -DV8_ATOMIC_MARKING_STATE -DV8_ENABLE_LAZY_SOURCE_POSITIONS -DV8_WIN64_UNWINDING_INFO -DV8_ENABLE_REGEXP_INTERPRETER_THREADED_DISPATCH -DV8_SNAPSHOT_COMPRESSION -DV8_ENABLE_WEBASSEMBLY -DV8_COMPRESS_POINTERS -DV8_31BIT_SMIS_ON_64BIT_ARCH -DV8_DEPRECATION_WARNINGS -DCPPGC_CAGED_HEAP -DV8_TARGET_ARCH_ARM64 -DV8_HAVE_TARGET_OS -DV8_TARGET_OS_LINUX -DDISABLE_UNTRUSTED_CODE_MITIGATIONS -DBUILDING_V8_SHARED -DV8_COMPRESS_POINTERS -DV8_31BIT_SMIS_ON_64BIT_ARCH -DV8_DEPRECATION_WARNINGS -DCPPGC_CAGED_HEAP -DUSING_V8_BASE_SHARED -I../.. -Igen -I../../v8 -I../../v8/include -Igen/v8 -Igen/v8/include -Igen/v8/include -fno-strict-aliasing --param=ssp-buffer-size=4 -fstack-protector -funwind-tables -fPIC -pipe -pthread -Wno-builtin-macro-redefined -D__DATE__= -D__TIME__= -D__TIMESTAMP__= -Wall -Wno-unused-local-typedefs -Wno-maybe-uninitialized -Wno-deprecated-declarations -Wno-comments -Wno-packed-not-aligned -Wno-missing-field-initializers -Wno-unused-parameter -fno-omit-frame-pointer -g0 -fno-builtin-abs -fvisibility=hidden -Wno-strict-overflow -Wno-return-type -Wno-int-in-bool-context -O3 -fno-ident -fdata-sections -ffunction-sections -std=gnu++14 -Wno-narrowing -Wno-class-memaccess -fno-exceptions -fno-rtti -nostdinc++ -isystem../../buildtools/third_party/libc++/trunk/include -isystem../../buildtools/third_party/libc++abi/trunk/include -fvisibility-inlines-hidden -c ../../v8/src/heap/base/asm/arm64/push_registers_asm.cc -o obj/v8/v8_cppgc_shared/push_registers_asm.o
{standard input}: Assembler messages:
{standard input}:15: Error: operand 1 should be a floating-point register -- `stp fp,lr,[sp,#-16]!'
{standard input}:16: Error: operand 1 should be an integer register -- `mov fp,sp'
{standard input}:20: Error: operand 1 should be an integer register -- `ldr lr,[sp,#8]'
{standard input}:21: Error: operand 1 should be an integer register -- `ldr fp,[sp],#96'
[2595/42232] ACTION //third_party/devtools...rypoint-bundle-rollup(//build/arm64:arm64)
zzzzzzzzzzzzzz
['../../third_party/node/linux/node/bin/node', '../../third_party/devtools-frontend/src/node_modules/rollup/dist/bin/rollup', '--silent', '--plugin', 'terser', '--config', '../../third_party/devtools-frontend/src/front_end/rollup.config.js', '--input', 'gen/third_party/devtools-frontend/src/front_end/ui/ui.prebundle.js', '--file', 'gen/third_party/devtools-frontend/src/front_end/ui/ui.js']
BBBBBBBBBBBB
[2606/42232] ACTION //content/common:mojo_bindings__parser(//build/arm64:arm64)
ninja: build stopped: subcommand failed.
```
---

```
obj/third_party/angle/angle_glslang_wrapper/glslang_wrapper_utils.o:glslang_wrapper_utils.cpp:function rx::GlslangTransformSpirvCode(std::__Cr::function<angle::Result (rx::GlslangError)> const&, rx::GlslangSpirvOptions const&, rx::ShaderInterfaceVariableInfoMap const&, std::__Cr::vector<unsigned int, std::__Cr::allocator<unsigned int> > const&, std::__Cr::vector<unsigned int, std::__Cr::allocator<unsigned int> >*): error: undefined reference to 'rx::(anonymous namespace)::SpirvTransformFeedbackCodeGenerator::kXfbDecorations'
```
vi third_party/angle/src/libANGLE/renderer/glslang_wrapper_utils.cpp +2119
```c++
 constexpr size_t SpirvTransformFeedbackCodeGenerator::kXfbDecorationCount;  //add this
 constexpr spv::Decoration SpirvTransformFeedbackCodeGenerator::kXfbDecorations[kXfbDecorationCount];   //add this
```

---

```sh
FAILED: obj/v8/v8_cppgc_shared/push_registers_asm.o
/work/bao/git/test/gcc-install/bin/g++ -MMD -MF obj/v8/v8_cppgc_shared/push_registers_asm.o.d -DUSE_UDEV -DUSE_AURA=1 -DUSE_GLIB=1 -DUSE_NSS_CERTS=1 -DUSE_OZONE=1 -DUSE_X11=1 -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE -D_LARGEFILE64_SOURCE -D__STDC_CONSTANT_MACROS -D__STDC_FORMAT_MACROS -D_FORTIFY_SOURCE=2 -DCOMPONENT_BUILD -D_LIBCPP_ABI_UNSTABLE -D_LIBCPP_ABI_VERSION=Cr -D_LIBCPP_ENABLE_NODISCARD -D_LIBCPP_HAS_NO_VENDOR_AVAILABILITY_ANNOTATIONS -DCR_LIBCXX_REVISION=8fa87946779682841e21e2da977eccfb6cb3bded -DNDEBUG -DNVALGRIND -DDYNAMIC_ANNOTATIONS_ENABLED=0 -DV8_TYPED_ARRAY_MAX_SIZE_IN_HEAP=64 -DENABLE_MINOR_MC -DV8_INTL_SUPPORT -DV8_USE_EXTERNAL_STARTUP_DATA -DV8_ATOMIC_OBJECT_FIELD_WRITES -DV8_ATOMIC_MARKING_STATE -DV8_ENABLE_LAZY_SOURCE_POSITIONS -DV8_WIN64_UNWINDING_INFO -DV8_ENABLE_REGEXP_INTERPRETER_THREADED_DISPATCH -DV8_SNAPSHOT_COMPRESSION -DV8_ENABLE_WEBASSEMBLY -DV8_COMPRESS_POINTERS -DV8_31BIT_SMIS_ON_64BIT_ARCH -DV8_DEPRECATION_WARNINGS -DCPPGC_CAGED_HEAP -DV8_TARGET_ARCH_ARM64 -DV8_HAVE_TARGET_OS -DV8_TARGET_OS_LINUX -DDISABLE_UNTRUSTED_CODE_MITIGATIONS -DBUILDING_V8_SHARED -DV8_COMPRESS_POINTERS -DV8_31BIT_SMIS_ON_64BIT_ARCH -DV8_DEPRECATION_WARNINGS -DCPPGC_CAGED_HEAP -DUSING_V8_BASE_SHARED -I../.. -Igen -I../../v8 -I../../v8/include -Igen/v8 -Igen/v8/include -Igen/v8/include -fno-strict-aliasing --param=ssp-buffer-size=4 -fstack-protector -funwind-tables -fPIC -pipe -pthread -Wno-builtin-macro-redefined -D__DATE__= -D__TIME__= -D__TIMESTAMP__= -Wall -Wno-unused-local-typedefs -Wno-maybe-uninitialized -Wno-deprecated-declarations -Wno-comments -Wno-packed-not-aligned -Wno-missing-field-initializers -Wno-unused-parameter -fno-omit-frame-pointer -g0 -fno-builtin-abs -fvisibility=hidden -Wno-strict-overflow -Wno-return-type -Wno-int-in-bool-context -O3 -fno-ident -fdata-sections -ffunction-sections -std=gnu++14 -Wno-narrowing -Wno-class-memaccess -fno-exceptions -fno-rtti -nostdinc++ -isystem../../buildtools/third_party/libc++/trunk/include -isystem../../buildtools/third_party/libc++abi/trunk/include -fvisibility-inlines-hidden -c ../../v8/src/heap/base/asm/arm64/push_registers_asm.cc -o obj/v8/v8_cppgc_shared/push_registers_asm.o
{standard input}: Assembler messages:
{standard input}:15: Error: operand 1 should be a floating-point register -- `stp fp,lr,[sp,#-16]!'
{standard input}:16: Error: operand 1 should be an integer register -- `mov fp,sp'
{standard input}:20: Error: operand 1 should be an integer register -- `ldr lr,[sp,#8]'
{standard input}:21: Error: operand 1 should be an integer register -- `ldr fp,[sp],#96'
[18/35519] CXX obj/v8/v8_base_without_compiler/code-generator-arm64.o
```
没有解决

---

PushAllRegistersAndIterateStack

  PushAllRegistersAndIterateStack(this, visitor, &IteratePointersImpl);


---
ninja
```
git clone git://github.com/ninja-build/ninja.git && cd ninja
git checkout release
$ cat README.md

./configure.py --bootstrap
```
---

```gn
[root@localhost chromium-90.0.4430.212]# cat  build/arm64/BUILD.gn
import("//build/toolchain/gcc_toolchain.gni")

gcc_toolchain("arm64") {
#  toolchain_args = {
#    current_cpu = "arm64"
#    current_os = "linux"
#  }
#  extra_cflags = "-O2"
#  cc = "/work/bao/git/devrte/runtime/gcc-9.2.0/bin/gcc"
#  cxx = "/work/bao/git/devrte/runtime/gcc-9.2.0/bin/g++"
#
#  ar = "/user/bin/ar"
#  ld = cxx



# toolprefix = "aarch64-unknown-linux-gnu-"
toolprefix = "/work/bao/git/test/gcc-install/bin/"
cc = "${toolprefix}gcc"
cxx = "${toolprefix}g++"
ar = "${toolprefix}gcc-ar"
ld = cxx
nm = "${toolprefix}gcc-nm"

toolchain_args = {
    current_cpu = "arm64"
    current_os = "linux"

     # reclient does not support gcc.
     use_rbe = false
     is_clang = false
   }
}

```

---

```
FAILED: obj/third_party/angle/translator/ReplaceForShaderFramebufferFetch.o
/usr/bin/g++ -MMD -MF 
obj/third_party/angle/translator/ReplaceForShaderFramebufferFetch.o.d -DANGLE_ENABLE_ESSL -DANGLE_ENABLE_GLSL -DANGLE_ENABLE_VULKAN -DANGLE_ENABLE_SWIFTSHADER -DUSE_UDEV -DUSE_AURA=1 -DUSE_GLIB=1 -DUSE_NSS_CERTS=1 -DUSE_OZONE=1 -DUSE_X11=1 -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE -D_LARGEFILE64_SOURCE -D__STDC_CONSTANT_MACROS -D__STDC_FORMAT_MACROS -D_FORTIFY_SOURCE=2 -DCOMPONENT_BUILD -D_LIBCPP_ABI_UNSTABLE -D_LIBCPP_ABI_VERSION=Cr -D_LIBCPP_ENABLE_NODISCARD -D_LIBCPP_HAS_NO_VENDOR_AVAILABILITY_ANNOTATIONS -DCR_LIBCXX_REVISION=8fa87946779682841e21e2da977eccfb6cb3bded -DCR_SYSROOT_HASH=92dd6b554df680bd27110d06ae3fc21fa5fd6588 -DNDEBUG -DNVALGRIND -DDYNAMIC_ANNOTATIONS_ENABLED=0 -DANGLE_IS_64_BIT_CPU -DANGLE_IS_LINUX -I../../third_party/angle/include -I../../third_party/angle/src -I../../third_party/angle/include -I../../third_party/angle/src/common/third_party/base -Igen/angle -I../../third_party/angle/include -fno-strict-aliasing --param=ssp-buffer-size=4 -fstack-protector -funwind-tables -fPIC -pipe -pthread -m64 -march=x86-64 -msse3 -Wno-builtin-macro-redefined -D__DATE__= -D__TIME__= -D__TIMESTAMP__= -Wall -Werror -Wno-unused-local-typedefs -Wno-maybe-uninitialized -Wno-deprecated-declarations -Wno-comments -Wno-packed-not-aligned -Wno-missing-field-initializers -Wno-unused-parameter -O2 -fno-ident -fdata-sections -ffunction-sections -fno-omit-frame-pointer -g0 -fno-builtin-abs -fvisibility=hidden -std=gnu++14 -Wno-narrowing -Wno-class-memaccess -fno-exceptions -fno-rtti -nostdinc++ -isystem../../buildtools/third_party/libc++/trunk/include -isystem../../buildtools/third_party/libc++abi/trunk/include --sysroot=../../build/linux/debian_sid_amd64-sysroot -fvisibility-inlines-hidden -c ../../third_party/angle/src/compiler/translator/tree_ops/vulkan/ReplaceForShaderFramebufferFetch.cpp -o obj/third_party/angle/translator/ReplaceForShaderFramebufferFetch.o
../../third_party/angle/src/compiler/translator/tree_ops/vulkan/ReplaceForShaderFramebufferFetch.cpp:459:17: error: ‘sh::ImmutableString sh::{anonymous}::ReplaceSubpassInputUtils::getInputAttachmentArrayName()’ defined but not used [-Werror=unused-function]
 ImmutableString ReplaceSubpassInputUtils::getInputAttachmentArrayName()
                 ^~~~~~~~~~~~~~~~~~~~~~~~
cc1plus: error: unrecognized command line option ‘-Wno-class-memaccess’ [-Werror]
cc1plus: error: unrecognized command line option ‘-Wno-packed-not-aligned’ [-Werror]
cc1plus: all warnings being treated as errors
[5/48628] CXX obj/third_party/angle/translator/OutputGLSLBase.o
ninja: build stopped: subcommand failed.
```

```c++
    458 /*
    459 ImmutableString ReplaceSubpassInputUtils::getInputAttachmentArrayName()
    460 {
    461     constexpr ImmutableString suffix("Array");
    462     std::stringstream nameStream = sh::InitializeStream<std::stringstream>();
    463     nameStream << sh::vk::kInputAttachmentName << suffix << mInputAttachmentArra        yIdSeq++;
    464     return ImmutableString(nameStream.str());
    465 }
    466 */

```
---

../../third_party/pdfium/core/fxcodec/jpx/cjpx_decoder.cpp:73:10: error: could not convert ‘data’ from ‘fxcodec::{anonymous}::OpjImageRgbData’ to ‘Optional<fxcodec::{anonymous}::OpjImageRgbData> {aka pdfium::Optional<fxcodec::{anonymous}::OpjImageRgbData>}’

vi ./third_party/pdfium/core/fxcodec/jpx/cjpx_decoder.cpp +73
```c++
     59 Optional<OpjImageRgbData> alloc_rgb(size_t size) {
          //OpjImageRgbData data;  change this
     60   Optional<OpjImageRgbData> data;
          //data.r.reset(static_cast<int*>(opj_image_data_alloc(size)));
     61   data.value().r.reset(static_cast<int*>(opj_image_data_alloc(size)));
          //if(!data.r)
     62   if (!data.value().r)
     63     return {};
     64
          //
     65   data.value().g.reset(static_cast<int*>(opj_image_data_alloc(size)));
          //
     66   if (!data.value().g)
     67     return {};
     68   
          //
     69   data.value().b.reset(static_cast<int*>(opj_image_data_alloc(size)));
          //
     70   if (!data.value().b)
     71     return {};
     72
     73   return data;
     74 }
```

---

```sh
python "../../build/toolchain/gcc_solink_wrapper.py" --readelf="readelf" --nm="/usr/bin/nm"  --sofile="./libcloud_policy_proto_generated_compile.so" --tocfile="./libcloud_policy_proto_generated_compile.so.TOC" --output="./libcloud_policy_proto_generated_compile.so" -- /usr/bin/g++ -shared -Wl,-soname="libcloud_policy_proto_generated_compile.so" -Wl,--fatal-warnings -Wl,--build-id -fPIC -Wl,-z,noexecstack -Wl,-z,relro -Wl,-z,defs -Wl,--as-needed -fuse-ld=gold -Wl,--threads -Wl,--thread-count=4 -m64 -Werror -lprotobuf -Wl,-O2 -Wl,--gc-sections -rdynamic -nodefaultlibs --sysroot=../../build/linux/debian_sid_amd64-sysroot -L../../build/linux/debian_sid_amd64-sysroot/usr/local/lib/x86_64-linux-gnu -L../../build/linux/debian_sid_amd64-sysroot/lib/x86_64-linux-gnu -L../../build/linux/debian_sid_amd64-sysroot/usr/lib/x86_64-linux-gnu -Wl,-rpath=\$ORIGIN -o "./libcloud_policy_proto_generated_compile.so" @"./libcloud_policy_proto_generated_compile.so.rsp"



obj/components/policy/proto/libpolicy_common_definitions_compile_proto.a(obj/components/policy/proto/policy_common_definitions_compile_proto/policy_common_definitions.pb.o):policy_common_definitions.pb.cc:function enterprise_management::StringList::ByteSizeLong() const: error: undefined reference to 'google::protobuf::RepeatedPtrField
<std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> > >::size() const'
```

打了个patch就好了

```sh
patch -p1 <../../chromium-78-protobuf-RepeatedPtrField-export.patch
```

patch里面的内容是：

```diff
diff --git a/third_party/protobuf/src/google/protobuf/repeated_field.h b/third_party/protobuf/src/google/protobuf/repeated_field.h
index b5b193c..4434854 100644
--- a/third_party/protobuf/src/google/protobuf/repeated_field.h
+++ b/third_party/protobuf/src/google/protobuf/repeated_field.h
@@ -804,7 +804,7 @@ class StringTypeHandler {
 // RepeatedPtrField is like RepeatedField, but used for repeated strings or
 // Messages.
 template <typename Element>
-class RepeatedPtrField final : private internal::RepeatedPtrFieldBase {
+class PROTOBUF_EXPORT RepeatedPtrField final : private internal::RepeatedPtrFieldBase {
  public:
   RepeatedPtrField();
   explicit RepeatedPtrField(Arena* arena);
```



---

没有`gperf`
```
subprocess.CalledProcessError: Command '['gperf', '--key-positions=*', '-P', '-n', '-m', '50', '-D']' returned non-zero exit status 127
```

下载一个
```
http://ftp.gnu.org/pub/gnu/gperf/gperf-3.1.tar.gz
tar -xvf gperf-3.1.tar.gz
cd gperf-3.1
./configure
make && make install
```
---

```
FAILED: gen/third_party/devtools-frontend/src/front_end/devtools_app.html gen/third_party/devtools-frontend/src/front_end/inspector.html gen/third_party/devtools-frontend/src/front_end/js_app.html gen/third_party/devtools-frontend/src/front_end/ndb_app.html gen/third_party/devtools-frontend/src/front_end/node_app.html gen/third_party/devtools-frontend/src/front_end/toolbox.html gen/third_party/devtools-frontend/src/front_end/worker_app.html
python ../../third_party/node/node.py ../../third_party/devtools-frontend/src/scripts/build/generate_html_entrypoint.js --template ../../third_party/devtools-frontend/src/front_end/entrypoint_template.html --out-directory gen/third_party/devtools-frontend/src/front_end
++++++++
('%s', ['../../third_party/node/linux/node-linux-x64/bin/node', '../../third_party/devtools-frontend/src/scripts/build/generate_html_entrypoint.js', '--template', '../../third_party/devtools-frontend/src/front_end/entrypoint_template.html', '--out-directory', 'gen/third_party/devtools-frontend/src/front_end'])
++++++++
Traceback (most recent call last):
  File "../../third_party/node/node.py", line 47, in <module>
    RunNode(sys.argv[1:])
  File "../../third_party/node/node.py", line 27, in RunNode
    cmd, cwd=os.getcwd(), stdout=subprocess.PIPE, stderr=subprocess.PIPE)
  File "/usr/lib64/python2.7/subprocess.py", line 394, in __init__
    errread, errwrite)
  File "/usr/lib64/python2.7/subprocess.py", line 1047, in _execute_child
    raise child_exception
OSError: [Errno 2] No such file or directory
[6/43218] CXX x64/obj/third_party/protobuf/protobuf_full/proto_writer.o
ninja: build stopped: subcommand failed.
```

```
++++++++
('%s', ['../../third_party/node/linux/node-linux-x64/bin/node', '../../third_party/devtools-frontend/src/scripts/build/generate_html_entrypoint.js', '--template', '../../third_party/devtools-frontend/src/front_end/entrypoint_template.html', '--out-directory', 'gen/third_party/devtools-frontend/src/front_end'])
++++++++

这里目录的名字node-linux-x64注意一下，路径找不到bin/node
```



```
vi out/Default/obj//components/policy/proto/policy_common_definitions_compile_proto.ninja
去掉Werror
```



---

```sh
python "../../build/toolchain/gcc_solink_wrapper.py" --readelf="readelf" --nm="/usr/bin/nm"  --sofile="./libGLESv2.so" --tocfile="./libGLESv2.so.TOC" --output="./libGLESv2.so" -- /usr/bin/g++ -shared -Wl,-soname="libGLESv2.so" -Wl,--fatal-warnings -Wl,--build-id -fPIC -Wl,-z,noexecstack -Wl,-z,relro -Wl,-z,defs -Wl,--as-needed -fuse-ld=gold -Wl,--threads -Wl,--thread-count=4 -m64 -Werror -Wl,-O2 -Wl,--gc-sections -rdynamic -nodefaultlibs --sysroot=../../build/linux/debian_sid_amd64-sysroot -L../../build/linux/debian_sid_amd64-sysroot/usr/local/lib/x86_64-linux-gnu -L../../build/linux/debian_sid_amd64-sysroot/lib/x86_64-linux-gnu -L../../build/linux/debian_sid_amd64-sysroot/usr/lib/x86_64-linux-gnu -Wl,-rpath=\$ORIGIN -o "./libGLESv2.so" @"./libGLESv2.so.rsp"

/usr/bin/ld.gold: error: obj/third_party/angle/angle_glslang_wrapper/glslang_wrapper_utils.o: requires dynamic R_X86_64_PC32 reloc against '_ZN2rx12_GLOBAL__N_135SpirvTransformFeedbackCodeGenerator15kXfbDecorationsE' which may overflow at runtime; recompile with -fPIC

obj/third_party/angle/angle_glslang_wrapper/glslang_wrapper_utils.o:glslang_wrapper_utils.cpp:function rx::GlslangTransformSpirvCode(std::__Cr::function<angle::Result (rx::GlslangError)> const&, rx::GlslangSpirvOptions const&, rx::ShaderInterfaceVariableInfoMap const&, std::__Cr::vector<unsigned int, std::__Cr::allocator<unsigned int> > const&, std::__Cr::vector<unsigned int, std::__Cr::allocator<unsigned int> >*): error: undefined reference to 'rx::(anonymous namespace)::SpirvTransformFeedbackCodeGenerator::kXfbDecorations'

obj/third_party/angle/angle_glslang_wrapper/glslang_wrapper_utils.o:glslang_wrapper_utils.cpp:function 
rx::GlslangTransformSpirvCode(std::__Cr::function<angle::Result (
rx::GlslangError)> const&, 
rx::GlslangSpirvOptions const&, 
rx::ShaderInterfaceVariableInfoMap const&, std::__Cr::vector<unsigned int, std::__Cr::allocator<unsigned int> > const&, std::__Cr::vector<unsigned int, std::__Cr::allocator<unsigned int> >*)
: error: undefined reference to 'rx::(anonymous namespace)::SpirvTransformFeedbackCodeGenerator::kXfbDecorations'
```

vi ./third_party/angle/src/libANGLE/renderer/glslang_wrapper_utils.cpp +4540

```sh
4538 constexpr size_t SpirvTransformFeedbackCodeGenerator::kXfbDecorationCount;  add this 
4539 constexpr spv::Decoration pirvTransformFeedbackCodeGenerator::kXfbDecorations[kXfbDecorationCount];   add this
```



---

```shell
../../third_party/pdfium/xfa/fxfa/fm2js/cxfa_fmexpression.cpp: In member function ‘Optional<CFX_WideTextBuf> CXFA_FMAST::ToJavaScript() const’:
../../third_party/pdfium/xfa/fxfa/fm2js/cxfa_fmexpression.cpp:781:12: error: could not convert ‘js’ from ‘CFX_WideTextBuf’ to ‘Optional<CFX_WideTextBuf> {aka pdfium::Optional<CFX_WideTextBuf>}’
```

 vi third_party/pdfium/pdfium.gni +48

```gni

  # Build PDFium either with or without XFA Forms support.
  # pdf_enable_xfa = pdf_enable_xfa_override
  pdf_enable_xfa = false			# change this
```

---

去掉烦人的Werror报错

```gn
[root@localhost chromium-90.0.4430.212]# grep -rn "Werror" build/config/compiler/
build/config/compiler/BUILD.gn:1645:      cflags += [ "-Werror" ]
build/config/compiler/BUILD.gn:1650:      ldflags = [ "-Werror" ]
build/config/compiler/BUILD.gn:1735:    # GCC may emit unsuppressible warnings so don't add -Werror for no chromium
build/config/compiler/BUILD.gn:1738:      cflags += [ "-Werror" ]
build/config/compiler/BUILD.gn:1739:      ldflags = [ "-Werror" ]
[root@localhost chromium-90.0.4430.212]# vi build/config/compiler/BUILD.gn +1645
[root@localhost chromium-90.0.4430.212]# vi build/config/compiler/BUILD.gn +1735
[root@localhost chromium-90.0.4430.212]# vi build/config/compiler/BUILD.gn +1738
```

---

```sh
../../components/services/storage/dom_storage/legacy_dom_storage_database.cc: In member function ‘bool storage::LegacyDomStorageDatabase::LazyOpen(bool)’:
../../components/services/storage/dom_storage/legacy_dom_storage_database.cc:162:24: sorry, unimplemented: non-trivial designated initializers not supported
       .cache_size = 500});
```

https://blog.csdn.net/zuicong5568/article/details/77944474

 vi ./components/services/storage/dom_storage/legacy_dom_storage_database.cc +162

```c++
  db_ = std::make_unique<sql::Database>(sql::DatabaseOptions{
      // This database should only be accessed from the process hosting the
      // storage service, so exclusive locking is appropriate.
      .exclusive_locking = true,
      .wal_mode = base::FeatureList::IsEnabled(sql::features::kEnableWALModeByDefault),  //ADD THIS
      .page_size = 4096,
      .cache_size = 500});
```

---

```sh
../../base/containers/flat_tree.h:150:23: error: uninitialized variable ‘extractor’ in ‘constexpr’ function
       GetKeyFromValue extractor;
```

vi ./base/containers/flat_tree.h +153

```c++
	 struct value_compare {
     constexpr bool operator()(const value_type& left,		
                              const value_type& right) const {
//      GetKeyFromValue extractor;  CHANGE THIS 
      GetKeyFromValue extractor = GetKeyFromValue();	//ADD THIS
      return comp(extractor(left), extractor(right));
    }
```



---



```sh
../../components/blocklist/opt_out_blocklist/sql/opt_out_store_sql.cc: In member function ‘virtual void blocklist::OptOutStoreSQL::LoadBlockList(std::__Cr::unique_ptr<blocklist::BlocklistData>, blocklist::LoadBlockListCallback)’:
../../components/blocklist/opt_out_blocklist/sql/opt_out_store_sql.cc:402:26: sorry, unimplemented: non-trivial designated initializers not supported
         .cache_size = 250});
```

vi ./components/blocklist/opt_out_blocklist/sql/opt_out_store_sql.cc +402

```c++
  if (!db_) {
    db_ = std::make_unique<sql::Database>(sql::DatabaseOptions{
        .exclusive_locking = true,
        // The entry size should be between 11 and 10 + x bytes, where x is the
        // the length of the host name string in bytes.
        // The total number of entries per host is bounded at 32, and the total
        // number of hosts is currently unbounded (but typically expected to be
        // under 100). Assuming average of 100 bytes per entry, and 100 hosts,
        // the total size will be 4096 * 78. 250 allows room for extreme cases
        // such as many host names or very long host names. The average case
        // should be much smaller as users rarely visit hosts that are not in
        // their top 20 hosts. It should be closer to 32 * 100 * 20 for most
        // users, which is about 4096 * 15. The total size of the database will
        // be capped at 3200 entries.
        .wal_mode = base::FeatureList::IsEnabled(sql::features::kEnableWALModeByDefault),	//ADD THIS
        .page_size = 4096,
        .cache_size = 250});
  }
```



---

```sh
./components/policy/core/common/registry_dict.cc: In function ‘base::Optional<base::Value> policy::ConvertRegistryValue(const base::Value&, const policy::Schema&)’:
../../components/policy/core/common/registry_dict.cc:53:14: error: could not convert ‘result’ from ‘base::Value’ to ‘base::Optional<base::Value>’
       return result;
              ^~~~~~
../../components/policy/core/common/registry_dict.cc:62:14: error: could not convert ‘result’ from ‘base::Value’ to ‘base::Optional<base::Value>’
       return result;
              ^~~~~~
../../components/policy/core/common/registry_dict.cc:115:16: error: could not convert ‘result’ from ‘base::Value’ to ‘base::Optional<base::Value>’
         return result;
```

vi ./components/policy/core/common/registry_dict.cc +53

```c++
	 43		if (value.type() == schema.type()) {
     44     // Recurse for complex types.
     45     if (value.is_dict()) {
     46       //base::Value result(base::Value::Type::DICTIONARY); //CHANGE THIS
     47       base::Optional<base::Value> result(base::Value::Type::DICTIONARY);
     48       for (const auto& entry : value.DictItems()) {
     49         base::Optional<base::Value> converted =
     50             ConvertRegistryValue(entry.second, schema.GetProperty(entry.first));
     51         if (converted.has_value())
     52           result.value().SetKey(entry.first, std::move(converted.value())); //这里加了.value()
     53       }
```

---

```sh
../../components/policy/core/common/schema.cc: In static member function ‘static base::Optional<base::Value> policy::Schema::ParseToDictAndValidate(const string&, int, std::__Cr::string*)’:
../../components/policy/core/common/schema.cc:1441:10: error: could not convert ‘json’ from ‘base::Value’ to ‘base::Optional<base::Value>’
   return json;
```

vi ./components/policy/core/common/schema.cc +1441

```c++
base::Optional<base::Value> Schema::ParseToDictAndValidate(
    const std::string& schema,
    int validator_options,
    std::string* error) {
  base::JSONReader::ValueWithError value_with_error =
      base::JSONReader::ReadAndReturnValueWithError(
          schema, base::JSONParserOptions::JSON_ALLOW_TRAILING_COMMAS);
  *error = value_with_error.error_message;

  if (!value_with_error.value)
    return base::nullopt;
  base::Optional<base::Value> json = std::move(value_with_error.value.value());//CHANGE THIS 加了base::Optional<>
  if (!json.value().is_dict()) {		// ADD value()
    *error = "Schema must be a JSON object";
    return base::nullopt;
  }
  if (!IsValidSchema(json.value(), validator_options, error)) //ADD value()
    return base::nullopt;
  return json;
}
```

---

```sh
./components/favicon/core/favicon_database.cc:256:29: sorry, unimplemented: non-trivial designated initializers not supported
            .cache_size = 32}) {}
                             ^
../../components/favicon/core/favicon_database.cc:256:29: sorry, unimplemented: non-trivial designated initializers not supported
```

vi ./components/favicon/core/favicon_database.cc +256

```c++
FaviconDatabase::FaviconDatabase()
    : db_({// Run the database in exclusive mode. Nobody else should be
           // accessing the database while we're running, and this will give
           // somewhat improved perf.
           .exclusive_locking = true,
           // Favicons db only stores favicons, so we don't need that big a page
           // size or cache.
           .wal_mode = base::FeatureList::IsEnabled(sql::features::kEnableWALModeByDefault),	//ADD THIS
           .page_size = 2048,
           .cache_size = 32}) {}

FaviconDatabase::~FaviconDatabase() {
  // The DBCloseScoper will delete the DB and the cache.
}
```

---

```sh
../../components/offline_pages/task/sql_store_base.cc:104:64: sorry, unimplemented: non-trivial designated initializers not supported
                                              .cache_size = 500}),
                                                                ^
../../components/offline_pages/task/sql_store_base.cc:104:64: sorry, unimplemented: non-trivial designated initializers not supported
```

vi ./components/offline_pages/task/sql_store_base.cc +104

```c++
void SqlStoreBase::Initialize(base::OnceClosure pending_command) {
  OnOpenStart(last_closing_time_);

  DCHECK_EQ(initialization_status_, InitializationStatus::kNotInitialized);
  initialization_status_ = InitializationStatus::kInProgress;

  // This is how we reset a pointer and provide deleter. This is necessary to
  // ensure that we can close the store more than once.
  db_ = DatabaseUniquePtr(new sql::Database({// These values are default.
                                             .exclusive_locking = true,
                                             .wal_mode = base::FeatureList::IsEnabled(sql::features::kEnableWALModeByDefault), //ADD THIS
                                             .page_size = 4096,
                                             .cache_size = 500}),
                          base::OnTaskRunnerDeleter(background_task_runner_));

  base::PostTaskAndReplyWithResult(
      background_task_runner_.get(), FROM_HERE,
      base::BindOnce(&InitializeSync, db_.get(), db_file_path_, histogram_tag_,
                     GetSchemaInitializationFunction()),
      base::BindOnce(&SqlStoreBase::InitializeDone,
                     weak_ptr_factory_.GetWeakPtr(),
                     std::move(pending_command)));
}
```



---

解压完了先把patch打上

```sh
chromium-60.0.3112.78-jpeg-nomangle.patch
chromium-60.0.3112.78-no-libpng-prefix.patch
chromium-67.0.3396.62-gn-system.patch
patch -p1 <../../chromium-70.0.3538.67-sandbox-pie.patch
patch -p1 <../../chromium-71.0.3578.98-py2-bootstrap.patch

patch -p1 <../../chromium-71.0.3578.98-widevine-r3.patch
patch -p1 <../../chromium-75.0.3770.100-epel7-stdc++.patch
patch -p1 <../../chromium-76.0.3809.100-gcc-remoting-constexpr.patch
patch -p1 <../../chromium-77.0.3865.75-gcc-include-memory.patch
patch -p1 <../../chromium-77.0.3865.75-no-zlib-mangle.patch
patch -p1 <../../chromium-77-clang.patch
patch -p1 <../../chromium-78.0.3904.70-gcc9-drop-rsp-clobber.patch
patch -p1 <../../chromium-78-protobuf-RepeatedPtrField-export.patch
patch -p1 <../../chromium-80.0.3987.132-el7-noexcept.patch
patch -p1 <../../chromium-80.0.3987.87-missing-cstdint-header.patch
patch -p1 <../../chromium-81.0.4044.92-unbundle-zlib.patch
patch -p1 <../../chromium-83.0.4103.61-disable-fontconfig-cache-magic.patch
patch -p1 <../../chromium-84.0.4147.105-gn-gcc-cleanup.patch
patch -p1 <../../chromium-84.0.4147.125-aarch64-clearkeycdm-binutils-workaround.patch
patch -p1 <../../chromium-84.0.4147.125-i686-fix_textrels.patch
patch -p1 <../../chromium-84.0.4147.125-remoting-cstring.patch
patch -p1 <../../chromium-84.0.4147.89-epel7-old-cups.patch
patch -p1 <../../chromium-85.0.4183.83-el7-old-libdrm.patch
patch -p1 <../../chromium-86.0.4240.75-fedora-user-agent.patch
patch -p1 <../../chromium-86.0.4240.75-fix-vaapi-on-intel.patch
patch -p1 <../../chromium-86.0.4240.75-vaapi-i686-fpermissive.patch
patch -p1 <../../chromium-88.0.4324.182-gcc-fix-swiftshader-libEGL-visibility.patch
patch -p1 <../../chromium-88.0.4324.182-rawhide-gcc-std-max-fix.patch
patch -p1 <../../chromium-89.0.4389.72-enable-hardware-accelerated-mjpeg.patch
patch -p1 <../../chromium-89.0.4389.72-initial_prefs-etc-path.patch
patch -p1 <../../chromium-89.0.4389.72-missing-cstring-header.patch
patch -p1 <../../chromium-89.0.4389.72-norar.patch

patch -p1 <../../chromium-89.0.4389.82-rhel8-force-disable-use_gnome_keyring.patch
patch -p1 <../../chromium-89.0.4389.82-support-futex_time64.patch
patch -p1 <../../chromium-89-EnumTable-crash.patch
patch -p1 <../../chromium-90.0.4430.72-fstatfix.patch
patch -p1 <../../chromium-90.0.4430.72-widevine-no-download.patch
patch -p1 <../../chromium-90.0.4430.93-epel7-erase-fix.patch
patch -p1 <../../chromium-90.0.4430.93-epel7-old-headers-workarounds.patch
patch -p1 <../../chromium-90.0.4430.93-epel8-aarch64-libpng16-symbol-prefixes.patch
patch -p1 <../../chromium-90-angle-constexpr.patch
patch -p1 <../../chromium-90-CrossThreadCopier-qualification.patch
patch -p1 <../../chromium-90-quantization_utils-include.patch
patch -p1 <../../chromium-90-ruy-include.patch
patch -p1 <../../chromium-90-TokenizedOutput-include.patch

patch -p1 <../../chromium-gcc11.patch
```
---

```sh
../../components/qr_code_generator/qr_code_generator.cc:671:10: error: could not convert ‘code’ from ‘QRCodeGenerator::GeneratedCode’ to ‘base::Optional<QRCodeGenerator::GeneratedCode>’
   return code;
```

vi components/qr_code_generator/qr_code_generator.cc +671

```c++
//  GeneratedCode code; //DELETE THIS
  base::Optional<QRCodeGenerator::GeneratedCode> code;
  code.value().data = base::span<uint8_t>(&d_[0], version_info_->total_size()); //ADD THIS value()
  code.value().qr_size = version_info_->size;									//ADD THIS value()
  return code;
```

---

```sh
../../net/dns/dns_query.cc:88:10: error: could not convert ‘merged_opt_rdata’ from ‘net::OptRecordRdata’ to ‘base::Optional<net::OptRecordRdata>’
   return merged_opt_rdata;
```

vi ./net/dns/dns_query.cc +88

```c++
base::Optional<OptRecordRdata> AddPaddingIfNecessary(
    const OptRecordRdata* opt_rdata,
    DnsQuery::PaddingStrategy padding_strategy,
    size_t no_opt_buffer_size) {
  // If no input OPT record rdata and no padding, no OPT record rdata needed.
  if (!opt_rdata && padding_strategy == DnsQuery::PaddingStrategy::NONE)
    return base::nullopt;

  base::Optional<OptRecordRdata> merged_opt_rdata; //ADD THIS: base::Optional<OptRecordRdata>
  if (opt_rdata)
    merged_opt_rdata.value().AddOpts(*opt_rdata); //ADD value()

  size_t unpadded_size = no_opt_buffer_size + OptRecordSize(&(merged_opt_rdata.value())); //ADD value()
  size_t padding_size = DeterminePaddingSize(unpadded_size, padding_strategy);

  if (padding_size > 0) {
    // |opt_rdata| must not already contain padding if DnsQuery is to add
    // padding.
    DCHECK(!merged_opt_rdata.value().ContainsOptCode(dns_protocol::kEdnsPadding)); //ADD value()
    // OPT header is the minimum amount of padding.
    DCHECK(padding_size >= OptRecordRdata::Opt::kHeaderSize);

    merged_opt_rdata.value().AddOpt(OptRecordRdata::Opt( //ADD value()
        dns_protocol::kEdnsPadding,
        std::string(padding_size - OptRecordRdata::Opt::kHeaderSize, 0)));
  }

  return merged_opt_rdata;
}
```

---

```sh
./buildtools/third_party/libc++/trunk/include/memory:824:9: error: use of deleted function ‘base::Value::Value(const base::Value&)’
         ::new ((void*)__p) _Up(_VSTD::forward<_Args>(__args)...);
         ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In file included from ../../base/trace_event/trace_config_category_filter.h:13:0,
                 from ../../base/trace_event/trace_config.h:20,
                 from ../../base/trace_event/trace_log.h:27,
                 from ../../base/trace_event/trace_event.h:29,
                 from ../../skia/ext/event_tracer_impl.cc:7:
../../base/values.h:169:3: note: declared here
   Value(const Value&) = delete;
   ^~~~~
```

因为用了delete的函数，所以报错了。

vi base/values.h +169

```c++
  Value& operator=(Value&& that) noexcept;
//  Value(const Value&) = delete;  去掉delete就好了
  Value(const Value&) = delete;		
  Value& operator=(const Value&) = delete;
```

---

```sh
../../buildtools/third_party/libc++/trunk/include/memory:824:9: error: use of deleted function ‘std::__Cr::pair<_T1, _T2>::pair(const std::__Cr::pair<_T1, _T2>&) [with _T1 = std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> >; _T2 = std::__Cr::unique_ptr<base::Value>]’
         ::new ((void*)__p) _Up(_VSTD::forward<_Args>(__args)...);
         ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
In file included from ../../buildtools/third_party/libc++/trunk/include/memory:674:0,
                 from ../../base/trace_event/trace_event.h:15,
                 from ../../skia/ext/event_tracer_impl.cc:7:
../../buildtools/third_party/libc++/trunk/include/utility:309:5: note: ‘std::__Cr::pair<_T1, _T2>::pair(const std::__Cr::pair<_T1, _T2>&) [with _T1 = std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> >; _T2 = std::__Cr::unique_ptr<base::Value>]’ is implicitly deleted because the default definition would be ill-formed:
     pair(pair const&) = default;
```

vi buildtools/third_party/libc++/trunk/include/utility +309

```c++
#if !defined(_LIBCPP_CXX03_LANG)
    pair(pair const&) = default;	
    //pair(pair&&) = default;	//注释掉 移动构造
#else
  // Use the implicitly declared copy constructor in C++03
#endif
```

---

```sh
../../ui/gfx/x/x11_window_event_manager.cc:24:75: sorry, unimplemented: non-trivial designated initializers not supported
           .window = window, .event_mask = static_cast<EventMask>(new_mask)})
```

vi ./ui/gfx/x/generated_protos/xproto.h +1477

```c++
struct ChangeWindowAttributesRequest {
  Window window{};
  base::Optional<EventMask> event_mask{}; //与16行的换了下顺序
  base::Optional<Pixmap> background_pixmap{};
  base::Optional<uint32_t> background_pixel{};
  base::Optional<Pixmap> border_pixmap{};
  base::Optional<uint32_t> border_pixel{};
  base::Optional<Gravity> bit_gravity{};
  base::Optional<Gravity> win_gravity{};
  base::Optional<BackingStore> backing_store{};
  base::Optional<uint32_t> backing_planes{};
  base::Optional<uint32_t> backing_pixel{};
  base::Optional<Bool32> override_redirect{};    
  base::Optional<Bool32> save_under{};
//  base::Optional<EventMask> event_mask{};
  base::Optional<EventMask> do_not_propogate_mask{};
  base::Optional<ColorMap> colormap{};
  base::Optional<Cursor> cursor{};
};
```

---

```sh
../../media/renderers/paint_canvas_video_renderer.h:261:58:   required from here
../../third_party/skia/include/core/SkRefCnt.h:141:14: error: invalid use of incomplete type ‘class media::VideoTextureBacking’
         obj->ref();
         ~~~~~^~~
In file included from ../../media/renderers/video_resource_updater.cc:44:0:
../../media/renderers/paint_canvas_video_renderer.h:44:7: note: forward declaration of ‘class media::VideoTextureBacking’
 class VideoTextureBacking;
 -------------------------------------------------------------------------------------------------------------
 ../../media/renderers/paint_canvas_video_renderer.h:261:25:   required from here
../../third_party/skia/include/core/SkRefCnt.h:141:14: error: invalid use of incomplete type ‘class media::VideoTextureBacking’
         obj->ref();
         ~~~~~^~~
In file included from ../../media/renderers/video_resource_updater.cc:44:0:
../../media/renderers/paint_canvas_video_renderer.h:44:7: note: forward declaration of ‘class media::VideoTextureBacking’
 class VideoTextureBacking;
```

vi third_party/skia/include/core/SkRefCnt.h +142

```c++
template <typename T> static inline T* SkSafeRef(T* obj) {
    if (obj) {
 //       obj->ref();			//注释掉了，不知道后面会不会有影响 CHANGE THIS
    }
    return obj;
}

/** Check if the argument is non-null, and if so, call obj->unref()
 */
template <typename T> static inline void SkSafeUnref(T* obj) {
    if (obj) {
   //     obj->unref(); //注释掉了，不知道后面会不会有影响 CHANGE THIS
    }
}
```

---

```sh
../../buildtools/third_party/libc++/trunk/include/memory:824:9: error: use of deleted function ‘std::__Cr::pair<_T1, _T2>::pair(const std::__Cr::pair<_T1, _T2>&) [with _T1 = std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> >; _T2 = std::__Cr::unique_ptr<base::Value>]’
         ::new ((void*)__p) _Up(_VSTD::forward<_Args>(__args)...);
         ^~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```



vi buildtools/third_party/libc++/trunk/include/utility +309

```c++
 #if !defined(_LIBCPP_CXX03_LANG)
  //pair(pair const&) = default;	//把这俩行都注释掉 改成下面这样
  pair(pair const&);				//ADD THIS
  //pair(pair&&) = default;
#else
  // Use the implicitly declared copy constructor in C++03
#endif
```



---

```sh
./ui/gfx/x/xproto_util.h:94:36: sorry, unimplemented: non-trivial designated initializers not supported
   return connection->ChangeProperty(
          ~~~~~~~~~~~~~~~~~~~~~~~~~~^
       ChangePropertyRequest{.window = static_cast<Window>(window),
       ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
                             .property = name,
                             ~~~~~~~~~~~~~~~~~
                             .type = type,
                             ~~~~~~~~~~~~~
                             .format = CHAR_BIT * sizeof(T),
                             ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
                             .data_len = values.size(),
                             ~~~~~~~~~~~~~~~~~~~~~~~~~~
                             .data = base::RefCountedBytes::TakeVector(&data)});
```

vi ./ui/gfx/x/generated_protos/xproto.h +1647

```c++
//修改的结构体
.src_window = static_cast<X11::Window>(0),
 .c_class = x11::WindowClass::InputOutput,
.type = static_cast<x11::Atom>(x11::Atom::None),
```

---



```c++
x11::Future<void> x11::XProto::CreateWindow(
const uint8_t&, 
const x11::Window&, 
const x11::Window&, 
const int16_t&, 
const int16_t&, 
const uint16_t&,
const uint16_t&, 
const uint16_t&, 
const x11::WindowClass&, 
const x11::VisualId&, 
const base::Optional<x11::Pixmap>&, 
const base::Optional<unsigned int>&, 
const base::Optional<x11::Pixmap>&, 
const base::Optional<unsigned int>&, 
const base::Optional<x11::Gravity>&, 
const base::Optional<x11::Gravity>&, 
const base::Optional<x11::BackingStore>&, 
const base::Optional<unsigned int>&, 
const base::Optional<unsigned int>&, 
const base::Optional<x11::Bool32>&, 
const base::Optional<x11::Bool32>&, 
const base::Optional<x11::EventMask>&, 
const base::Optional<x11::EventMask>&, 
const base::Optional<x11::ColorMap>&, 
const base::Optional<x11::Cursor>&)


    	.depth = 0,
        .wid = window,
        .parent = connection->default_root(),
        .x = -100,
        .y = -100,
        .width = 10,
        .height = 10,
        .border_width = 0,
        .c_class = x11::WindowClass::InputOnly,
        .visual = static_cast<x11::VisualId>(0),
        .background_pixmap = x11::Pixmap::None,
        .background_pixel = 0,
        .border_pixmap = x11::Pixmap::None,
        .border_pixel = 0,
        .bit_gravity = x11::Gravity::BitForget,
        .win_gravity = x11::Gravity::BitForget,
        .backing_store = x11::BackingStore::NotUseful,
        .backing_planes = 0,
        .backing_pixel = 0,
        .override_redirect = Bool32(true),

	   .background_pixmap = x11::Pixmap::None,
        .background_pixel = 0,
        .border_pixmap = x11::Pixmap::None,
        .border_pixel = 0,
        .bit_gravity = x11::Gravity::BitForget,
        .win_gravity = x11::Gravity::BitForget,
        .backing_store = x11::BackingStore::NotUseful,
        .backing_planes = 0,
        .backing_pixel = 0,
        .override_redirect = x11::Bool32(false),
        .save_under = x11::Bool32(false),
        .event_mask = x11::EventMask::Exposure});


newUserStr=qianduoduo;
8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
    
    reinterpret_cast
```

---

09-22

```c++
MakeFixedFlatSet<base::StringPiece>(<brace-enclosed initializer list>)
template<class Key, long unsigned int N, class Compare> constexpr base::fixed_flat_set<Key, N, Compare> base::MakeFixedFlatSet(std::__Cr::common_type_t<Key> (&&)[N], const Compare&)
```

 vim services/network/public/cpp/cross_origin_read_blocking.cc +314 

```c++
251 const auto& GetNeverSniffedMimeTypes() {
 252   static constexpr auto kNeverSniffedMimeTypes = base::MakeFixedFlatSet<
 253       base::StringPiece, 34>({		//添加， 34
```

---

```sh
obj/mojo/core/impl_for_embedder/channel_linux.o:channel_linux.cc:function mojo::core::ChannelLinux::UpgradesEnabled(): error: undefined reference to 'mojo::core::kMojoLinuxChannelSharedMem'
```

vi mojo/core/embedder/features.cc

```c++
#if defined(OS_POSIX) && !defined(OS_NACL) && !defined(OS_MAC)
// zb #if defined(OS_LINUX) || defined(OS_CHROMEOS) || defined(OS_ANDROID)	
COMPONENT_EXPORT(MOJO_CORE_EMBEDDER_FEATURES)
const base::Feature kMojoLinuxChannelSharedMem{
    "MojoLinuxChannelSharedMem", base::FEATURE_DISABLED_BY_DEFAULT};
COMPONENT_EXPORT(MOJO_CORE_EMBEDDER_FEATURES)
const base::FeatureParam<int> kMojoLinuxChannelSharedMemPages{
    &kMojoLinuxChannelSharedMem, "MojoLinuxChannelSharedMemPages", 4};
// zb #endif  // defined(OS_LINUX) || defined(OS_CHROMEOS) || defined(OS_ANDROID)

COMPONENT_EXPORT(MOJO_CORE_EMBEDDER_FEATURES)
const base::Feature kMojoPosixUseWritev{"MojoPosixUseWritev",
                                        base::FEATURE_DISABLED_BY_DEFAULT};
#endif  // defined(OS_POSIX) && !defined(OS_NACL) && !defined(OS_MAC)
```

---



```sh
obj/mojo/core/impl_for_embedder/channel_linux.o:channel_linux.cc:function mojo::core::ChannelLinux::UpgradesEnabled(): error: undefined reference to 'mojo::core::kMojoLinuxChannelSharedMem'
collect2: error: ld returned 1 exit status
```

vim mojo/core/channel_linux.cc

```c++
extern const base::Feature kMojoLinuxChannelSharedMem;
```

---



````sh
obj/skia/skia/SkSLSPIRVCodeGenerator.o:SkSLSPIRVCodeGenerator.cpp:function SkSL::SPIRVCodeGenerator::writeInstructions(SkSL::Program const&, SkSL::OutputStream&): error: undefined reference to 'std::__Cr::pair<SkSL::Variable const* const, unsigned int>::pair(std::__Cr::pair<SkSL::Variable const* const, unsigned int> const&)'
````

头文件里加这个

```c++
#include <utility>
```

---

```sh
gen/components/ui_devtools/base_string_adapter.cc: In static member function ‘static void ui_devtools::protocol::StringUtil::WriteString(const String&, std::__Cr::vector<unsigned char>*)’:
gen/components/ui_devtools/base_string_adapter.cc:164:23: error: reference to ‘span’ is ambiguous
   cbor::EncodeString8(span<uint8_t>(StringUtil::CharactersUTF8(str),
                       ^~~~
In file included from ../../buildtools/third_party/libc++/trunk/include/memory:676:0,
                 from gen/components/ui_devtools/base_string_adapter.h:10,
                 from gen/components/ui_devtools/base_string_adapter.cc:7:
../../buildtools/third_party/libc++/trunk/include/iterator:1577:68: note: candidates are: template<class _Tp, long unsigned int <anonymous> > class std::__Cr::span
     template <class _Tp, size_t> friend class _LIBCPP_TEMPLATE_VIS span;
                                                                    ^~~~
In file included from ../../third_party/inspector_protocol/crdtp/parser_handler.h:9:0,
                 from ../../third_party/inspector_protocol/crdtp/cbor.h:15,
                 from ../../third_party/inspector_protocol/crdtp/protocol_core.h:14,
                 from gen/components/ui_devtools/base_string_adapter.h:18,
                 from gen/components/ui_devtools/base_string_adapter.cc:7:
../../third_party/inspector_protocol/crdtp/span.h:21:7: note:                 template<class T> class crdtp::span
 class span {
       ^~~~
gen/components/ui_devtools/base_string_adapter.cc:164:35: error: expected primary-expression before ‘>’ token
   cbor::EncodeString8(span<uint8_t>(StringUtil::CharactersUTF8(str),
```

vi out/Default/gen/components/ui_devtools/base_string_adapter.cc +164

```c++
void StringUtil::WriteString(const String& str, std::vector<uint8_t>* bytes) {
  cbor::EncodeString8(crdtp::span<uint8_t>(StringUtil::CharactersUTF8(str),	//添加crdtp::
                                    StringUtil::CharacterCount(str)),
                      bytes);
}
```

---



28029

26364

---

09-23

:ui::ImeTextSpan

vim out/Default/gen/ui/base/ime/mojom/text_input_state.mojom.h +403

```c++
401 template <typename T, ImeTextSpanInfo::EnableIfSame<T>*>
402 bool operator<(const T& lhs, const T& rhs) {
403   if (lhs.(::ui::ImeTextSpan::span) < rhs.(::ui::ImeTextSpan::span)) //添加命名空间, 不行的
404     return true;
405   if (rhs.span < lhs.span)
406     return false;
407   if (lhs.bounds < rhs.bounds)
408     return true;
409   if (rhs.bounds < lhs.bounds)
410     return false;
411   return false;
412 }
```

---

```sh
../../device/fido/cable/cable_discovery_data.cc:121:10: error: could not convert ‘pairing’ from ‘std::__Cr::unique_ptr<device::cablev2::Pairing>’ to ‘base::Optional<std::__Cr::unique_ptr<device::cablev2::Pairing> >’
   return pairing;
```

vim device/fido/cable/cable_discovery_data.cc +121

```c++
#include <utility>
```



---



```sh
../../device/fido/device_response_converter.cc:117:10: error: could not convert ‘response’ from ‘device::AuthenticatorMakeCredentialResponse’ to ‘base::Optional<device::AuthenticatorMakeCredentialResponse>’
   return response;
```

这问题终于解决啦啊啊啊啊

vim device/fido/authenticator_make_credential_response.cc +61

```c++
AuthenticatorMakeCredentialResponse  response(
       transport_used, AttestationObject(std::move(authenticator_data),
                                         std::move(fido_attestation_statement)));
   response.is_resident_key = false;
   base::Optional<AuthenticatorMakeCredentialResponse> tmp_response(std::move(response));//zb 添加此行 std::move()把左值变成右值
   return tmp_response;
```



---



```sh
../../device/fido/device_response_converter.cc:117:10: error: could not convert ‘response’ from ‘device::AuthenticatorMakeCredentialResponse’ to ‘base::Optional<device::AuthenticatorMakeCredentialResponse>’
   return response;
```

vim device/fido/device_response_converter.cc +117

```c++
base::Optional<AuthenticatorMakeCredentialResponse> tmp_response(std::move(response));//zb
   //return response;
   return tmp_response;
```



---

```sh
error :span need 2 args
```

vim ui/base/ime/mojom/text_input_state.mojom +15

```c++
 struct ImeTextSpanInfo {
    ui.mojom.ImeTextSpan TMPspan; //这个变量更换了名字
    gfx.mojom.Rect bounds;
 };

```

---

```c++
error: undefined reference to 'std::__Cr::pair<std::__Cr::unique_ptr<base::ModuleCache::Module const, std::__Cr::default_delete<base::ModuleCache::Module const> >*, long>::pair(std::__Cr::pair<std::__Cr::unique_ptr<base::ModuleCache::Module const, std::__Cr::default_delete<base::ModuleCache::Module const> >*, long> const&)'

obj/base/base/process_memory_dump.o:process_memory_dump.cc:function base::trace_event::ProcessMemoryDump::TakeAllDumpsFrom(base::trace_event::ProcessMemoryDump*): error: undefined reference to 'std::__Cr::pair<base::trace_event::MemoryAllocatorDumpGuid const, base::trace_event::ProcessMemoryDump::MemoryAllocatorDumpEdge>::pair(std::__Cr::pair<base::trace_event::MemoryAllocatorDumpGuid const, base::trace_event::ProcessMemoryDump::MemoryAllocatorDumpEdge> const&)'

std::__Cr::pair<std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> > const&, 
base::Value const&>::pair(std::__Cr::pair<std::__Cr::basic_string<char, std::__Cr::char_traits<char>, 
std::__Cr::allocator<char> > const&, base::Value const&> const&)


    
std::__Cr::pair<base::trace_event::MemoryAllocatorDumpGuid const, base::trace_event::ProcessMemoryDump::MemoryAllocatorDumpEdge>::pair(std::__Cr::pair<base::trace_event::MemoryAllocatorDumpGuid const, base::trace_event::ProcessMemoryDump::MemoryAllocatorDumpEdge> const&)
    
obj/base/base/field_trial_param_associator.o:field_trial_param_associator.cc:function 
base::FieldTrialParamAssociator::AssociateFieldTrialParams(
std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> > const&, 
    
std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> > const&, 
    
std::__Cr::map<std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> >, std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> >, std::__Cr::less<std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> > >, std::__Cr::allocator<std::__Cr::pair<std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> > const, std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> > > > > const&): 

error: undefined reference to '

std::__Cr::pair<std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> >, std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> > >::pair(std::__Cr::pair<std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> >, std::__Cr::basic_string<char, std::__Cr::char_traits<char>, std::__Cr::allocator<char> > > const&)'

    
python "../../build/toolchain/gcc_solink_wrapper.py" --readelf="readelf" --nm="/usr/bin/nm"  --sofile="./libbase.so" --tocfile="./libbase.so.TOC" --output="./libbase.so" -- /usr/bin/g++ -std=gnu++14 -shared -Wl,-soname="libbase.so" -Wl,--fatal-warnings -Wl,--build-id -fPIC -Wl,-z,noexecstack -Wl,-z,relro -Wl,-z,defs -Wl,--as-needed -fuse-ld=gold -Wl,--threads -Wl,--thread-count=4 -m64 -Werror -rdynamic -nodefaultlibs --sysroot=../../build/linux/debian_sid_amd64-sysroot -L../../build/linux/debian_sid_amd64-sysroot/usr/local/lib/x86_64-linux-gnu -L../../build/linux/debian_sid_amd64-sysroot/lib/x86_64-linux-gnu -L../../build/linux/debian_sid_amd64-sysroot/usr/lib/x86_64-linux-gnu -Wl,-rpath=\$ORIGIN -Wl,-O2 -Wl,--gc-sections -L../../build/linux/debian_sid_amd64-sysroot/usr/lib/x86_64-linux-gnu -o "./libbase.so" @"./libbase.so.rsp"

std::__Cr::pair<int, base::TimeDelta>::pair(std::__Cr::pair<int, base::TimeDelta>&&)'
    
    
    cp build/linux/debian_sid_amd64-sysroot/usr/include/c++/10/utility build/linux/debian_sid_amd64-sysroot/usr/include/.
    
    Copied buildtools/third_party/libc++/trunk/src/include/refstring.h to
 15   buildtools/third_party/libc++abi/libcxx/src/include/refstring.h to work
 16   around https://llvm.org/PR49313
solibs = ./libabsl.so ./libboringssl.so ./libperfetto.so ./libicui18n.so ./libc++.so

    
    
    'std::__Cr::pair<base::WaitableEvent*, unsigned long>::pair(std::__Cr::pair<base::WaitableEvent*, unsigned long>&&)'
    

    'std::__Cr::pair<int, base::TimeDelta>::pair(std::__Cr::pair<int, base::TimeDelta>&&)'

    'std::__Cr::pair<base::trace_event::MemoryAllocatorDumpGuid const, base::trace_event::ProcessMemoryDump::MemoryAllocatorDumpEdge>::pair(std::__Cr::pair<base::trace_event::MemoryAllocatorDumpGuid const, base::trace_event::ProcessMemoryDump::MemoryAllocatorDumpEdge> const&)'


```

https://gcc.gnu.org/onlinedocs/libstdc%2B%2B/manual/using_dual_abi.html

vim buildtools/third_party/libc++/trunk/include/utility

```c++
 308 #if !defined(_LIBCPP_CXX03_LANG)
 309     //pair(pair const&) = default;
 310     pair(pair const&);      //改成这样了
 311     //pair(pair&&) = default;
 312     //pair(pair const&);
```

---



