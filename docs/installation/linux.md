# Linux

Razuna has been tested on Ubuntu (Server) 10.x, 11.x and 12.x. Thought there is nothing against running it on older versions as well. Furthermore, we've tested it with RedHat 6.x and CentOS 5.x & 6.x.
___
**Install Java**

If you haven't installed Java6 already, then please issue the following command below.

* Ubuntu

```
apt-get install software-properties-common
apt-get install python-software-properties
apt-add-repository ppa:webupd8team/java
apt-get update
apt-get install oracle-java7-installer
```

* RedHat 6.x

```
cd /opt
wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/7u75-b13/jdk-7u75-linux-x64.tar.gz"
tar xzf jdk-7u75-linux-x64.tar.gz
 
alternatives --install /usr/bin/java java /opt/jdk1.7.0_75/bin/java 2
alternatives --config java
```
___

**Edit environment variables**

Not a installation requirement per se, but we've seen that some Ubuntu servers throw environment variables errors. Simply edit the /etc/environment file and add:

* Ubuntu

```
JAVA_HOME=/usr/lib/jvm/java-7-oracle
```

**Note :** Make sure to have /urs/local/bin in your PATH environment as well!
___

**Install Ghost Script**

* Note (with Ghost Script) : Do **not** install Ghostscript with packages anymore as they are outdated. Follow the instructions below to install Ghostscript.

```
wget http://downloads.ghostscript.com/public/binaries/ghostscript-9.15-linux-x86_64.tgz
tar xzvf ghostscript-9.15-linux-x86_64.tgz
cd /usr/bin/
mv gs gs--
ln -s /opt/ghostscript-9.15-linux-x86_64/gs-915-linux_x86_64 gs
```

If you rather compile from source you can download the latest version Ghostscript at [http://ghostscript.com/releases/](http://ghostscript.com/releases/). Note: You need to download the source and not the pre-packaged one!

After unpacking follow it with a:

```
./configure
```
and a

```
make && make install
```

Make a symbolic link in "/usr/bin" for Ghostscript with:

```
ln -s /usr/local/bin/gs /usr/bin/gs
```
___

**Install ImageMagick**

Get the latest version from [http://www.imagemagick.org](http://www.imagemagick.org). Then install or check that all the needed libraries are installed with:

On most systems you should be able to do a simple:

* Ubuntu :

```
apt-get install imagemagick
```

or for RedHat

* RedHat :

```
yum install ImageMagick
```
___

**Install ImageMagick from source**

If you need to install from source you can follow the steps below:

```
yum install tcl-devel libpng-devel libjpeg-devel ghostscript-devel bzip2-devel freetype-devel libtiff-devel
```

Then configure ImageMagick with (command should be on one line):

```
configure --prefix=/usr/local --with-bzlib=yes --with-fontconfig=yes --with-freetype=yes --with-gslib=yes --with-gvc=yes \
--with-jpeg=yes --with-jp2=yes --with-png=yes --with-tiff=yes
```

Followed by a:

```
make && make install
```

If all worked well you should see something like this when issuing the command:

```
convert --version
Version: ImageMagick 6.5.7-5 2009-11-08 Q16 http://www.imagemagick.org
Copyright: Copyright (C) 1999-2009 ImageMagick Studio LLC
```
___

**Install FFMpeg**

**FFmpeg Installation for Ubuntu**

Actually it is very easy to install FFmpeg under Ubuntu with the apt-get command. Unfortunately, the default FFmpeg installation doesn't let you include the latest codecs which are needed by Razuna. Thus you have to compile FFmpeg yourself. Just follow the steps below. It is very easy!

```
Ubuntu Versions : All the below has been tested and is know to work with Ubuntu 10.04, 12.04 and 14.04 LTS.
```
**Install the Dependencies**

Uninstall x264, libx264-dev, and ffmpeg if they are already installed.

```
sudo apt-get remove ffmpeg x264 libx264-dev
```

Next, get all of the packages you will need to install FFmpeg and x264 (you may need to enable the universe and multiverse repositories):

```
sudo apt-get update
```

**Ubuntu 10.04 LTS**

```
sudo apt-get install build-essential subversion git-core checkinstall texi2html \
libfaac-dev libopencore-amrnb-dev libopencore-amrwb-dev libsdl1.2-dev libtheora-dev \
libvorbis-dev libx11-dev libxfixes-dev libxvidcore-dev zlib1g-dev libavcodec-dev
```

**Ubuntu 9.10**

```
sudo apt-get install build-essential subversion git-core checkinstall yasm texi2html \
libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libsdl1.2-dev \
libvorbis-dev libx11-dev libxfixes-dev libxvidcore-dev zlib1g-dev libavcodec-unstripped-52
```

**Install x264**

Get the most current source files, compile, and install. You can run "./configure --help" to see what additional features you can enable/disable.

* Ubuntu 10.04 LTS :

```
cd /opt
git clone git://git.videolan.org/x264.git
cd x264
./configure --enable-static --disable-opencl
make
sudo checkinstall --pkgname=x264 --default --pkgversion="3:$(./version.sh | \
awk -F'[" ]' '/POINT/{print $4"+git"$5}')" --backup=no --deldoc=yes
```

* Ubuntu 9.10

```
cd /opt
git clone git://git.videolan.org/x264.git
cd x264
./configure
make
sudo checkinstall --pkgname=x264 --pkgversion "1:0.svn`date +%Y%m%d`+`git rev-list HEAD -n 1 | head -c 7`" --backup=no --default
```
___
**Troubleshooting**

If the configure complains about yasm requiring version 1.2.x, then you need to download and build yasm with the latest build. Follow these instructions to do so (each line is a command!):

```
sudo apt-get install build-essential checkinstall
sudo apt-get build-dep yasm
cd /opt
wget http://www.tortall.net/projects/yasm/releases/yasm-1.2.0.tar.gz
tar xzfv yasm-1.2.0.tar.gz
cd yasm-1.2.0
./configure
make
sudo checkinstall --pakdir "$HOME/Desktop" --pkgname yasm --pkgversion 1.2.0 \
--backup=no --default
```

Now try to configure X264 again.
___

**Install libvpx**

This is used to encode and decode VP8 video (WebM).

```
cd /opt
git clone https://chromium.googlesource.com/webm/libvpx.git
cd libvpx
./configure
make
sudo checkinstall --pkgname=libvpx --pkgversion="`date +%Y%m%d%H%M`-git" --backup=no \
--default --deldoc=yes
```

**Install lame**

Used for MP3.

```
sudo apt-get remove libmp3lame-dev
sudo apt-get install nasm
cd /opt
wget http://downloads.sourceforge.net/project/lame/lame/3.98.4/lame-3.98.4.tar.gz
tar xzvf lame-3.98.4.tar.gz
cd lame-3.98.4
./configure --enable-nasm --disable-shared
make
sudo checkinstall --pkgname=lame-ffmpeg --pkgversion="3.98.4" --backup=no --default --deldoc=yes
```

**Install libtheora (only needed on Ubuntu 9.10)**

This is used to encode to Theora, the video type usually found in OGG/OGV files. The repository libtheora is too old, so it must be compiled.

```
sudo apt-get install libogg-dev
cd /opt
wget http://downloads.xiph.org/releases/theora/libtheora-1.1.1.tar.gz
tar xzvf libtheora-1.1.1.tar.gz
cd libtheora-1.1.1
./configure --disable-shared
make
sudo checkinstall --pkgname=libtheora --pkgversion "1.1.1" --backup=no --default
```

**Install FFMpeg**

Get the most current source files from the official FFmpeg SVN, compile, and install.

* Ubuntu 10.04/12.04/14/04 LTS :

```
cd /opt
git clone git://source.ffmpeg.org/ffmpeg.git
cd ffmpeg
git checkout release/2.5
./configure --enable-gpl --enable-version3 --enable-nonfree --enable-postproc \
--enable-libfaac --enable-libopencore-amrnb --enable-libopencore-amrwb \
--enable-libtheora --enable-libvorbis --enable-libx264 --enable-libxvid \
--enable-x11grab --enable-libvpx --enable-libmp3lame
make
sudo checkinstall --pkgname=ffmpeg --pkgversion="5:$(./version.sh)" --backup=no \
--deldoc=yes --default
hash x264 ffmpeg ffplay ffprobe
```

**Ubuntu 9.10**

```
cd /opt
git clone git://source.ffmpeg.org/ffmpeg.git
cd ffmpeg
git checkout release/2.5
./configure --enable-gpl --enable-version3 --enable-nonfree --enable-postproc --enable-libfaac --enable-libmp3lame --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libtheora --enable-libvorbis --enable-libvpx --enable-libx264 --enable-libxvid --enable-x11grab
make
sudo checkinstall --pkgname=ffmpeg --pkgversion "4:0.5+svn`date +%Y%m%d`" --backup=no --default
hash x264 ffmpeg ffplay
```

**Updating FFmpeg and x264**

Development of FFmpeg and x264 is active and an occasional update can give you new features and bug fixes. To update FFmpeg and x264 you will need to remove the packages, make distclean, update the source, recompile, and install.

To update x264:

```
sudo apt-get remove ffmpeg x264 libx264-dev libvpx
cd /opt/x264
make distclean
git pull
```

Now compile x264 as shown earlier in the guide starting with the x264 ./configure line. You can update libvpx if you installed that too:

```
cd /opt/libvpx
make clean
git pull
```
Now continue with the installation starting with the libvpx ./configure line. Now update FFmpeg:

```
cd /opt/ffmpeg
make distclean
git pull
```
Finish the installation starting with the FFmpeg ./configure line from above.

___


**FFMpeg Installation on CentOS and RedHat**

If you are upgrading from a previous version of Razuna you should always update your ImageMagick, Exiftool and Ffmpeg installation!

The following install steps have been proven to work on RedHat Enterprise Linux 6.2 and 6.5. You can check which version you are running with

```
cat /etc/redhat-release
```

Additionally, we assume that you are connected and registered with the Red Hat network and/or updated the system with the latest updates from the repositories. 

Follow this guide step by step!

* Install the additional repo :

```
rpm -Uhv http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el6.rf.x86_64.rpm
```

Update repository

```
yum -y update
```

* Install all necessary packages :

```
yum install glibc gcc gcc-c++ autoconf automake libtool git make nasm pkgconfig
yum install SDL-devel a52dec a52dec-devel alsa-lib-devel faac faac-devel faad2 faad2-devel
yum install freetype-devel giflib gsm gsm-devel imlib2 imlib2-devel lame lame-devel libICE-devel libSM-devel libX11-devel
yum install libXau-devel libXdmcp-devel libXext-devel libXrandr-devel libXrender-devel libXt-devel
yum install libogg libvorbis vorbis-tools mesa-libGL-devel mesa-libGLU-devel xorg-x11-proto-devel zlib-devel
yum install libtheora theora-tools
yum install ncurses-devel
yum install libdc1394 libdc1394-devel
yum install amrnb-devel amrwb-devel opencore-amr-devel 
```

* Install xvid :

```
cd /opt
wget http://downloads.xvid.org/downloads/xvidcore-1.3.2.tar.gz
tar xzvf xvidcore-1.3.2.tar.gz
cd xvidcore/build/generic
./configure --prefix="$HOME/ffmpeg_build"
make
make install
```

* Install LibOgg :

```
cd /opt
wget http://downloads.xiph.org/releases/ogg/libogg-1.3.1.tar.gz
tar xzvf libogg-1.3.1.tar.gz
cd libogg-1.3.1
./configure --prefix="$HOME/ffmpeg_build" --disable-shared
make
make install
```

* Install Libvorbis :

```
cd /opt
wget http://downloads.xiph.org/releases/vorbis/libvorbis-1.3.4.tar.gz
tar xzvf libvorbis-1.3.4.tar.gz
cd libvorbis-1.3.4
./configure --prefix="$HOME/ffmpeg_build" --with-ogg="$HOME/ffmpeg_build" --disable-shared
make
make install
```

* Install Libtheora:

```
cd /opt
wget http://downloads.xiph.org/releases/theora/libtheora-1.1.1.tar.gz
tar xzvf libtheora-1.1.1.tar.gz
cd libtheora-1.1.1
./configure --prefix="$HOME/ffmpeg_build" --with-ogg="$HOME/ffmpeg_build" --disable-examples --disable-shared --disable-sdltest --disable-vorbistest
make
make install
```

* Install Aacenc:

```
cd /opt
wget http://downloads.sourceforge.net/opencore-amr/vo-aacenc-0.1.2.tar.gz
tar xzvf vo-aacenc-0.1.2.tar.gz
cd vo-aacenc-0.1.2
./configure --prefix="$HOME/ffmpeg_build" --disable-shared
make
make install
```

* Install Yasm :

```
yum remove yasm
cd /opt
wget http://www.tortall.net/projects/yasm/releases/yasm-1.2.0.tar.gz
tar xzfv yasm-1.2.0.tar.gz
cd yasm-1.2.0
./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin"
make
make install
export "PATH=$PATH:$HOME/bin" 
```

* Install Libvpx :

```
cd /opt
git clone https://chromium.googlesource.com/webm/libvpx.git
cd libvpx
git checkout tags/v.1.3.0
./configure --prefix="$HOME/ffmpeg_build" --disable-examples
make
make install
```

* Install X264

```
cd /opt
git clone git://git.videolan.org/x264.git
cd x264
./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" --enable-static 
make
make install
```

Note: (Sometimes the network might be down. Then you can also grab it via wget at [ftp://ftp.videolan.org/pub/videolan/x264/snapshots/last_stable_x264.tar.bz2](ftp://ftp.videolan.org/pub/videolan/x264/snapshots/last_stable_x264.tar.bz2)) and then use "tar xvjf last_xxx" to extract.

* Configure Libraries:

```
export LD_LIBRARY_PATH=/usr/local/lib/
echo /usr/local/lib >> /etc/ld.so.conf.d/custom-libs.conf
ldconfig
```

* Compile FFmpeg (the configure options have to be on one line) :

```
cd /opt
git clone git://source.ffmpeg.org/ffmpeg.git
cd ffmpeg
git checkout release/2.5
PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig"
export PKG_CONFIG_PATH
./configure --prefix="$HOME/ffmpeg_build" --extra-cflags="-I$HOME/ffmpeg_build/include" --extra-ldflags="-L$HOME/ffmpeg_build/lib" --bindir="$HOME/bin" \
--extra-libs=-ldl --enable-version3 --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libvpx --enable-libfaac \
--enable-libmp3lame --enable-libtheora --enable-libvorbis --enable-libx264 --enable-libvo-aacenc --enable-libxvid --disable-ffplay \
--enable-gpl --enable-postproc --enable-nonfree --enable-avfilter --enable-pthreads
make
make install
```

(The --arch=x86_64 option should only be used if you are on a 64Bit System!)

You can also use their Github repository at [https://github.com/FFmpeg/FFmpeg.git](https://github.com/FFmpeg/FFmpeg.git).

That's it. This should give you a full functional FFMpeg installation for Razuna. Test it now with;

```
ffmpeg
```
This should give you the following back (yours might vary a bit);

```
ffmpeg version 2.2 Copyright (c) 2000-2014 the FFmpeg developers
  built on Mar 28 2014 01:28:21 with gcc 4.4.7 (GCC) 20120313 (Red Hat 4.4.7-4)
  configuration: --enable-version3 --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-libvpx --enable-libfaac --enable-libmp3lame --enable-libtheora --enable-libvorbis --enable-libx264 --enable-libvo-aacenc --enable-libxvid --disable-ffplay --enable-shared --enable-gpl --enable-postproc --enable-nonfree --enable-avfilter --enable-pthreads --extra-cflags=-fPIC
  libavutil      52. 66.100 / 52. 66.100
  libavcodec     55. 52.102 / 55. 52.102
  libavformat    55. 33.100 / 55. 33.100
  libavdevice    55. 10.100 / 55. 10.100
  libavfilter     4.  2.100 /  4.  2.100
  libswscale      2.  5.102 /  2.  5.102
  libswresample   0. 18.100 /  0. 18.100
  libpostproc    52.  3.100 / 52.  3.100
Hyper fast Audio and Video encoder
usage: ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfile}...
```

Try to convert a movie with;

```
ffmpeg -i movie.mov -vcodec libx264 -vpre hq -acodec libfaac movie.mp4
```

* Troubleshoot :

It could be that you run into issues with a message of "ffmpeg: error while loading shared libraries....:. This simply means that it can't find the required libraries, in short you need to add them to the linked library configuration.

Check what libraries are missing with:

```
ldd `which ffmpeg`
```

This will give you a list of libraries ffmpeg is using. If any of them are marked with "not found" then search for the missing library in question, e.g. "libswresample.so.0" with:

```
find / -name libswresample.so.0
```

Once you have the path simply add it to /etc/ld.so.conf and issue a "ldconfig".

This should get you ffmpeg up and running.
___
___
**Install Exiftool**

Go to [http://owl.phy.queensu.ca/~phil/exiftool/](http://owl.phy.queensu.ca/~phil/exiftool/) and download the latest version.

Once downloaded all you need to do is:

```
perl Makefile.PL
make
make test
make install
```

(Each line is a separate command)

Note: Some Perl installations may not contain the necessary files to complete the first step above.  But no worries: You can install ExifTool manually by moving 'exiftool' and the 'lib' directory to any directory in your current PATH (ie. /usr/bin). More information is available over at [http://owl.phy.queensu.ca/~phil/exiftool/](http://owl.phy.queensu.ca/~phil/exiftool/).

___
**Install DCRaw & ufraw (optional)**

Razuna is able to work with RAW images from different digital cameras. In order for Razuna to work with RAW images you will need to install "DCRAW" and "ufraw". To install those two libraries either download and compile them install them from your distribution repositories. Under Ubuntu this is done with:

* Ubuntu :

```
apt-get install dcraw
apt-get install ufraw
```

* RedHat :

```
yum install dcraw
```

___

**Install MP4Box (optional)**

MP4Box helps with automatic streaming for certain videos. It is part of the gpac package. Install it with:

* Ubuntu :

```
apt-get install gpac
```

* RedHat :

```
yum install gcc
yum install zlib*
yum install freeglut.x86_64  freeglut-devel.x86_64
wget http://repo.bstack.net/mp4box/gpac-0.4.5.tar.gz
wget http://repo.bstack.net/mp4box/gpac_extra_libs-0.4.5.tar.gz
tar -zxvf gpac-0.4.5.tar.gz
tar -zxvf gpac_extra_libs-0.4.5.tar.gz
mkdir /usr/local/src/gpac
mkdir /usr/local/src/gpac/extra_lib
cd gpac_extra_libs
cp -r * /usr/local/src/gpac/extra_lib
cd ..
cd gpac
chmod +x configure
./configure
make lib
make apps
make install lib
make install
cp bin/gcc/libgpac.so /usr/lib
```
___

**Troubleshooting**

You might run into the error "MP4Box: error while loading shared libraries: libgpac.so: cannot open shared object file: No such file or directory". Problem is that the shared library was compiled, but is not installed to /usr/local/lib. Solution is:

```
cd gpac
install -m644 bin/gcc/libgpac.so /usr/local/lib/libgpac.so
chmod +x /usr/local/lib/libgpac.so
ldconfig
```
___

**Setup Razuna standalone**

If you have not already done so, [download the latest Razuna release](http://razuna.org/download) from [http://razuna.org](http://razuna.org). We recommend to extract Razuna to the "/opt" directory, but you are free to place it wherever you see fit. The Razuna standalone server comes with Tomcat pre-configured.

___
**Start the Razuna server**

The final task left to do now is to startup the application server. In order to do so, navigate to the "bin" directory of the Razuna folder (/opt/razuna/tomcat/bin/) and start the server with:

```
./startup.sh
```
___
**Navigate to Razuna**

Once the server has successfully started you should navigate to [http://localhost:8080/razuna](http://localhost:8080/razuna) and you will be presented with the Firsttime Wizard to finish setup.



___

