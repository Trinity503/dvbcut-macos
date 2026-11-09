# dvbcut-macos

This explains, how to compile dvbcut (latest tested version: 0.74) from bernhardu/dvbcut-deb on macos (tested with macos ventura and macos monterey).

## 1. Install needed files

```
brew install autoconf
brew install libao
brew install boost
brew install a52dec
brew install mplayer
brew install mad
brew install ffmpeg
brew install pkg-config
brew install qt5
brew link qt5 --force
xcode-select --install
```

All installs in a single command:

```
brew install autoconf libao boost a52dec mplayer mad ffmpeg pkg-config qt5 && brew link qt5 --force && xcode-select --install
```

## 2. Pull repository

```
git clone https://github.com/bernhardu/dvbcut-deb/
cd dvbcut-deb
```

## 3. Compile

```
autoconf
./configure CXXFLAGS=-std=c++14
```

Thanks to Thomas Perl for the help with the CXXFLAG!


On Silicon-Chips:

In die configure.ac vor "dln checks for libraries" Folgendes eintragen:

```
AC_ARG_WITH([mad-prefix],
  [AS_HELP_STRING([--with-mad-prefix=PREFIX],
                  [prefix where libmad is installed])],
  [mad_prefix="$withval"],
  [mad_prefix=""])

AS_IF([test -n "$mad_prefix"], [
  CPPFLAGS="$CPPFLAGS -I$mad_prefix/include"
  LDFLAGS="$LDFLAGS -L$mad_prefix/lib"
])

AC_ARG_WITH([a52-prefix],
  [AS_HELP_STRING([--with-a52-prefix=PREFIX],
                  [prefix where liba52 is installed])],
  [a52_prefix="$withval"],
  [a52_prefix=""])

AS_IF([test -n "$a52_prefix"], [
  CPPFLAGS="$CPPFLAGS -I$a52_prefix/include"
  LDFLAGS="$LDFLAGS -L$a52_prefix/lib"
])
```

Danach evtl. 

```
autoreconf -fi
```

```
./configure \
  --with-ffmpeg-prefix="$(brew --prefix ffmpeg)" \
  --with-mad-prefix="$(brew --prefix mad)" \
  --with-a52-prefix="$(brew --prefix a52dec)" \
  INSTALL=/usr/bin/install \
  CXXFLAGS=-std=c++14

```

  

## 

## 4. Run "make"

```
make
```

If necessary you also can update make with: 

```
brew install make && echo PATH="/usr/local/opt/make/libexec/gnubin:$PATH"
```

You should now have a "dvbcut"-file in the src-directory. Try tu run it.

## 5. Run "make install"

```
make install
```

This installs dvbcut for the use in the terminal.

## 6. Create a DVBCUT.APP for your Applications-folder:

Get the App-Container here from this repository.

```
git clone https://github.com/erhardma/dvbcut-macos/
```

Copy the "dvbcut"-file from your src-directory to this App-Container to the Contents/MACOS-folder (right click - Show Contents "Paketinhalt anzeigen") and you are finished.
If the icon does not work, open the DVBCut.app with Command + I and then drag the Icon-file in Contents/Resources on the Icon in the Window, which you opened with Command + I.
