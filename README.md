## 编译

编译这个项目，需要获取一些第三方的代码，所以需要首先执行：

	git submodule update --init

mupdf默认使用的是X11窗口，在Mac OS X下X11窗口不支持Fullscreen，也就意味着Splitview不能使用，要用原生的Cocoa窗口。

修改了Makefile相关的三个文件，直接make就可以了，生成使用Cocoa窗口的目标文件`build/release/mupdf-gl`。

## mupdf-gl中的修改

1. 修正了文件名超过15个汉字的crash问题
2. 命令行的跳转到指定<page>功能没有实现，但是help中却显示有这个功能？！ 好吧，现在我帮他们实现了
3. 其他一些细节问题，例如`h,j,k,l`的滚屏也没有实现，现在加上去了;修改jk的实现为可以连续滚屏，和vim的体验完全相同了。
4. 增加了背景色功能，可以任意指定色彩，在程序运行中，也可以随时用`C`来随机选择颜色;修改了默认颜色为绿色。
5. 增加了保存阅读页面位置的记录功能，打开文件如没有指定页面位置，就会自动跳转到上次的阅读页面
6. 修改了其他一些问题

## 使用方法

打开filename.pdf的文件，并定位到82页

	mupdf-gl filename.pdf 82

打开的同时设置阅读的背景色

	mupdf-gl -C 0xfdf6e3 filename.pdf

* `+,=` 放大
* `-` 缩小
* `w` 适合宽度
* `H` 适合高度
* `h,j,k,l` 移动
* `d,u,b,<space>` 翻页
* `v` 反转颜色(晚上用不错)
* `q` 退出
* ……

## 使用效果

### 用`o`打开和关闭书签栏

![Outline](http://ww3.sinaimg.cn/mw690/3e37e59cgw1f73rgqu058j20r40l8qdi.jpg)

### 用`[`和`]`进行左右旋转微调，再也不担心倾斜问题了

![before rotate](http://ww2.sinaimg.cn/mw690/3e37e59cgw1f73rgm7xudj20si0kudj0.jpg)


![after rotate](http://ww3.sinaimg.cn/mw690/3e37e59cgw1f73rgkit87j20si0kujur.jpg)

### 用`x,y`进行水平和垂直空白区裁剪（大写`X,Y`对裁剪区反向操作）

![](http://ww1.sinaimg.cn/mw690/3e37e59cgw1f7jv5yiybqj211y0lc7fn.jpg)

### 用`v`反色，夜间减少屏幕亮度刺眼

![no invert](http://ww3.sinaimg.cn/mw690/3e37e59cgw1f73rggc44ij20j70kuwk9.jpg)


![invert](http://ww1.sinaimg.cn/mw690/3e37e59cgw1f73rgj32akj20j70ku7a2.jpg)

### 随意设置背景色，总有适合你的

![solarized](http://ww4.sinaimg.cn/mw690/3e37e59cgw1f77e8jv2kjj20m20ku463.jpg)


![green](http://ww2.sinaimg.cn/mw690/3e37e59cgw1f77e8e4qxvj20m20kun4d.jpg)

### 打赏一杯咖啡

<div style="margin:0 auto;text-align:center;"><img src="http://ww4.sinaimg.cn/large/006tNbRwgy1ffro7wwx4qj30cd09c0tf.jpg" alt="捐赠" /></div>
<div style="margin:0 auto;text-align:center;padding:0 0 30px"><span title="Wechat"><img src="http://ww4.sinaimg.cn/large/006tNbRwgy1ffrnypm54hj319w1okadp.jpg" width="221" alt="Wechat"/></span><span title="alipay"><img src="http://ww2.sinaimg.cn/large/006tNbRwgy1ffroocv9ipj31401gsah1.jpg" width="221" alt="alipay"/></span></div>

---

ABOUT

MuPDF is a lightweight PDF, XPS, EPUB and CBZ viewer and parser/rendering
library.

The renderer in MuPDF is tailored for high quality anti-aliased graphics. It
renders text with metrics and spacing accurate to within fractions of a pixel
for the highest fidelity in reproducing the look of a printed page on screen.

MuPDF is also small, fast, and yet complete. We support PDF 1.7 with
transparency, encryption, hyperlinks, annotations, search and many other bells
and whistles. MuPDF can also read XPS documents (OpenXPS / ECMA-388),
EPUB and CBZ (Comic Book archive) files.

MuPDF is written to be both modular and portable; the example applications
are merely thin layers on top of the functionality offered by the library,
so custom viewers can be easily built for a wide range of platforms. Example
viewer applications are supplied for Windows, Linux, MacOS, iOS and Android.

MuPDF is deliberately designed to be threading library agnostic, while still
supporting multi-threaded operation. In the absence of a thread library
it will run single-threaded, but by adding one significant benefits in
rendering speed on multi-core platforms can be obtained.

Interactive features such as form filling, javascript and transitions
are in development and partially supported by the Android application.

LICENSE

MuPDF is Copyright 2006-2015 Artifex Software, Inc.

This program is free software: you can redistribute it and/or modify it under
the terms of the GNU Affero General Public License as published by the Free
Software Foundation, either version 3 of the License, or (at your option) any
later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU Affero General Public License along
with this program. If not, see <http://www.gnu.org/licenses/>.

For commercial licensing, including our "Indie Dev" friendly options,
please contact sales@artifex.com.

COMPILING

If you are compiling from source you will need several third party libraries:
freetype2, jbig2dec, libjpeg, openjpeg, and zlib. These libraries are contained
in the source archive. If you are using git, they are included as git
submodules.

You will also need the X11 headers and libraries if you're building on Linux.
These can typically be found in the xorg-dev package. Alternatively, if you
only want the command line tools, you can build with HAVE_X11=no.

The new OpenGL-based viewer also needs OpenGL headers and libraries. If you're
building on Linux, install the mesa-common-dev and libgl1-mesa-dev packages.
You'll also need several X11 development packages: xorg-dev, libxcursor-dev,
libxrandr-dev, and libxinerama-dev. To skip building the OpenGL viewer, build
with HAVE_GLFW=no.

DOWNLOAD

The latest development source is available directly from the git repository:

	git clone http://mupdf.com/repos/mupdf.git

In the mupdf directory, update the third party libraries:

	git submodule update --init

INSTALLING (UNIX)

Typing "make prefix=/usr/local install" will install the binaries, man-pages,
static libraries and header files on your system.

REPORTING BUGS AND PROBLEMS

The MuPDF developers hang out on IRC in the #ghostscript channel on
irc.freenode.net.

Report bugs on the ghostscript bugzilla, with MuPDF as the selected component.

	http://bugs.ghostscript.com/

If you are reporting a problem with PDF parsing, please include the problematic
file as an attachment.
