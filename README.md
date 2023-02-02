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
brew install qt5
brew link qt5 --force
xcode-select --install
```

## 2. Pull repository
```
git clone https://github.com/bernhardu/dvbcut-deb/
cd dvbcut-deb
```

## 3. Compile
```
autoconf
./configure
```


## 4. Change Compiler and Settings
   Edit the Makefile in the src directory and change the line
```
CXX=g++
```
to
```
CXX=clang++ -std=c++14 -stdlib=libc++
```
.

If you don't do this, you will get errors that say, that c++11 is required and not there. c++11 itself is not enough, you have to use at least 14. Perhapt some guru can explain, why g++ doesn't work.

## 5. Run "make"
```
make
```
(You also can update make with: brew install make && echo PATH="/usr/local/opt/make/libexec/gnubin:$PATH")
   
You should now have a "dvbcut"-file in the src-directory. Try tu run it.

## 6. Run "make install"
```
make install
```

This installs dvbcut for the use in the terminal.
   
## 7. Create a DVBCUT.APP for your Applications-folder:
Get the App-Container here from this repository.
```
git clone https://github.com/erhardma/dvbcut-macos/
```
Copy the "dvbcut"-file from your src-directory to this App-Container to the Contents/MACOS-folder (right click - Show Contents "Paketinhalt anzeigen") and you are finished.

