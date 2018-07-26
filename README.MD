# Build

## Linux Mint 18.3

dependency needed

    sudo apt-get install libglib-2.0-dev

change makefiles to address glib correctly

    //replace all instances of `glib-config --cflags` with $(pkg-config --cflags glib-2.0)
    grep -rl '`glib-config --cflags`' src | xargs sed -i 's/`glib-config --cflags`/$(pkg-config --cflags glib-2.0)/g'

    //replace all instances of `glib-config --libs` with $(pkg-config --libs glib-2.0)
    grep -rl '`glib-config --libs`' src | xargs sed -i 's/`glib-config --cflags`/$(pkg-config --libs glib-2.0)/g'

build

    export WISECONFIGDIR=~/path/to/wisecfg/
    cd src
    make all
    cd dyc
    make dyc
    make linux
    sudo cp dyc usr/bin/local  
    cd ../
    make init
    make all

    * note1: if it says some objects cannot be found, but they are where they are supposed to be, move them to trash and let them rebuild.  I had to do this for dnal.o, dnaalign.o, and seqaligndisplay.o.  `make all` in the src/ dir rebuilds them.

    * note2: cannot find `/usr/bin/ld: cannot find -ldyna_glib`
