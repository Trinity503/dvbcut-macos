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

