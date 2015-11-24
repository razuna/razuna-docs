# MacOS X

Razuna has been tested with MacOS 10.5 and since then with any newer version. Our team develops on the Mac platform, so we can securely say it runs with the latest system (currently 10.8.2).

** Install Java :**

Latest MacOS X releases don't come with Java pre-installed anymore. Thus before you can run Razuna you need to install Java. MacOS X automatically detects a call to Java and will prompt you to download it the first time. Both Java 6 and Java7 works with Razuna.

**Install HomeBrew :**

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

**Install Ghostscript :**

```
brew install ghostscript
```

**Install ImageMagick :**

```
brew install libtiff
brew install imagemagick --with-libtiff
```

**Install FFmpeg :**

```
brew install ffmpeg --use-clang --with-libvorbis --with-libvpx --use-gcc  --with-libx264 --with-flac --with-theora
```

**Install Exiftool :**

```
brew install exiftool
```

**Install Dcraw :**

```
brew install dcraw
```

**Install UFraw :**

```
brew install ufraw
```

**Install MP4Box :**

```
brew install MP4Box
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

 