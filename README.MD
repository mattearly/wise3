# Build

## Linux Mint 18.3

dependency needed

    sudo apt-get install libglib-2.0-dev

change makefiles to address glib correctly

    //replace all instances of `glib-config --clfags` with $(pkg-config --cflags glib-2.0)
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