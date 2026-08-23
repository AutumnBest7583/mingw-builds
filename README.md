# MinGW 构建 [![x86_64 and i686 发布构建](https://github.com/niXman/mingw-builds/actions/workflows/build_cmake.yml/badge.svg)](https://github.com/niXman/mingw-builds/actions/workflows/build_cmake.yml)

> 本分叉已将其缩减成单一编译目标：`x86_64-posix-seh-ucrt`，并**尝试**启用本地语言支持（`--enable-nls`）
> 
> 本自述文档和原文的差异：
> 1. 将两个"参考"的网址，通过 Markdown URL 标签移动到引用位置
> 2. 最后更新于 UTC+8 2026-08-23 16:00，可能和最新版本出现偏差

这些脚本由 [MinGW-Builds 项目](https://github.com/niXman/mingw-builds/) 提供，是设计给 i686/x86_64 主机进行构建 i686/x86_64 MinGW-W64 编译器

这些脚本是根据 ['BSD 3' 许可协议](http://www.opensource.org/licenses/BSD-3-Clause) 分发的.

使用这些由 MinGW-W64 项目提供的脚本需要

1. Windows-64位 或 Linux + Wine-64位

2. 安装 MSYS2 :
  `http://sourceforge.net/projects/msys2/`
  (MSYS2 wiki: https://www.msys2.org/wiki/MSYS2-installation/)

3. 获取这个脚本到 `<msys root>/home/<user>/mingw-builds`:
  `cd && git clone <paste correct url>`

4. 在 MSYS2 文件结构中删除或重命名 `/mingw32` 和 `/mingw64` 目录.

5. 在 `PATH` 环境变量中，删除任何指向预安装的 MinGW 路径

6. 转到 MinGW-builds 根目录:
  `cd && cd mingw-builds`

7. 选项:
```
  --mode=[gcc|python|clang]-<version> - what package to build with version.
  --arch=<i686|x86_64>                - 构建架构.
  --buildroot=<path>                  - 使用 '<path>' 作为构建路径.
                                        By default used MSYS user home directory.
  --fetch-only                        - 仅下载全部资源但是不构建.
  --update-sources                    - 在构建之前尝试从仓库更新源.
  --exceptions=<model>                - 异常处理模型.
                                        可用: dwarf, seh(仅 gcc>=4.8.0), sjlj, dwarfseh (按架构选择).
  --use-lto                           - 使用链接时优化（LTO）构建.
  --no-strip                          - don't strip executables during install.
  --no-multilib                       - 构建没有 multilib 支持的 GCC (DWARF 和 SEH 异常模型的默认值).
  --static-gcc                        - 构建静态 GCC.
  --dyn-deps                          - 构建带有动态依赖的 GCC.
  --rt-version=<v3..v14>              - 用于构建的 mingw-w64 运行时的版本
  --rev=N                             - 构建版本的数量.
  --with-testsuite                    - run testsuite for packages that contain flags for it.
  --threads=<posix|win32>             - 使用的线程模型.
  --enable-languages=<langs>          - GCC 支持的编程语言的逗号分隔的列表
                                        可用语言: ada,c,c++,fortran,objc,obj-c++
  --enable-wildcard                   - 由 mingw-w64 运行时启用通配符展开
  --with-default-win32-winnt=<ver>    - 工具链目标的默认 Windows 版本
```
  For more options run: "./build --help"

8. 运行:
*  `./build --mode=gcc-4.8.1 --arch=i686` 用于构建 i686-MinGW-w64
*  `./build --mode=gcc-4.8.1 --arch=x86_64` 用于构建 x86_64-MinGW-w64
*  `./build --mode=gcc-4.8.1 --arch=x86_64 --preload` 用于预加载源和构建 x86_64-MinGW-w64
*  `./build --mode=gcc-4.8.1 --arch=i686 --exceptions=dwarf` 用于构建带有 DWARF 异常处理的 i686-MinGW-w64

例如, 经过构建过程的 i686-gcc-4.7.2 将被创建在以下目录：
```
  <buildroot>/i686-4.7.2-release-posix-sjlj-rev1/build
  <buildroot>/i686-4.7.2-release-posix-sjlj-rev1/libs
  <buildroot>/i686-4.7.2-release-posix-sjlj-rev1/logs
  <buildroot>/i686-4.7.2-release-posix-sjlj-rev1/prefix
```

对于 x86_64：
```
  <buildroot>/x86_64-4.7.2-release-posix-sjlj-rev1/build
  <buildroot>/x86_64-4.7.2-release-posix-sjlj-rev1/libs
  <buildroot>/x86_64-4.7.2-release-posix-sjlj-rev1/logs
  <buildroot>/x86_64-4.7.2-release-posix-sjlj-rev1/prefix
```

源路径:
  `<buildroot>/src`


The archives with the built MinGW will be created in `<buildroot>/archives/`

目前，成功地构建以下版本:
```
  gcc-4.6.4
  gcc-4.7.0
  gcc-4.7.1
  gcc-4.7.2
  gcc-4.7.3
  gcc-4.7.4
  gcc-4.8.0
  gcc-4.8.1
  gcc-4.8.2
  gcc-4.8.3
  gcc-4.8.4
  gcc-4.8.5
  gcc-4.9.0
  gcc-4.9.1
  gcc-4.9.2
  gcc-4.9.3
  gcc-4.9.4
  gcc-5.1.0
  gcc-5.2.0
  gcc-5.3.0
  gcc-5.4.0
  gcc-5.5.0
  gcc-6.1.0
  gcc-6.2.0
  gcc-6.3.0
  gcc-6.4.0
  gcc-6.5.0
  gcc-7.1.0
  gcc-7.2.0
  gcc-7.3.0
  gcc-7.4.0
  gcc-7.5.0
  gcc-8.1.0
  gcc-8.2.0
  gcc-8.3.0
  gcc-8.4.0
  gcc-8.5.0
  gcc-9.1.0
  gcc-9.2.0
  gcc-9.3.0
  gcc-9.4.0
  gcc-9.5.0
  gcc-10.1.0
  gcc-10.2.0
  gcc-10.3.0
  gcc-10.4.0
  gcc-10.5.0
  gcc-11.1.0
  gcc-11.2.0
  gcc-11.3.0
  gcc-11.4.0
  gcc-11.5.0
  gcc-12.1.0
  gcc-12.2.0
  gcc-12.3.0
  gcc-12.4.0
  gcc-12.5.0
  gcc-13.1.0
  gcc-13.2.0
  gcc-13.3.0
  gcc-13.4.0
  gcc-14.1.0
  gcc-14.2.0
  gcc-14.3.0
  gcc-14.4.0
  gcc-15.1.0
  gcc-15.2.0
  gcc-15.3.0
  gcc-16.1.0
  gcc-16.2.0
  gcc-4.6-branch (currently 4.6.5 prerelease)
  gcc-4.7-branch (currently 4.7.5 prerelease)
  gcc-4.8-branch (currently 4.8.6 prerelease)
  gcc-4.9-branch (currently 4.9.5 prerelease)
  gcc-5-branch (currently 5.5.1 prerelease)
  gcc-6-branch (currently 6.5.1 prerelease)
  gcc-7-branch (currently 7.5.1 prerelease)
  gcc-8-branch (currently 8.5.1 prerelease)
  gcc-9-branch (currently 9.5.1-prerelease)
  gcc-10-branch (currently 10.5.1-prerelease)
  gcc-11-branch (currently 11.5.1-prerelease)
  gcc-12-branch (currently 12.5.1-prerelease)
  gcc-13-branch (currently 13.4.1-prerelease)
  gcc-14-branch (currently 14.4.1-prerelease)
  gcc-15-branch (currently 15.3.1-prerelease)
  gcc-16-branch (currently 16.2.1-prerelease)
  gcc-trunk (currently 17.0.0 snapshot)
```

Builds also contains patches for building Python 2.7.9 and 3.4.3 versions for support gdb pretty printers.
Big thanks for these patches to:
```
  2010-2013 Roumen Petrov, Руслан Ижбулатов
  2012-2015 Ray Donnelly, Alexey Pavlov
```
