PRAOSP Project - BASED SOSP Project
-------------------
Disclaimer
-------------------
I recommend using a Linux machine (Ubuntu) with 16gb or more. If it fails, put 32gb that will run smoothly.

This project is inspired by the AOSP and SOSP Project! It does not use the SilverCore kernel because the bixo consumes a lot of battery mlk!!

Install the build packages:
-----------------------------

    sudo apt-get install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev

Install the repo command:
-----------------------------

    mkdir -p ~/bin
    mkdir -p ~/PRAOSP
    curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
    chmod a+x ~/bin/repo

GIT config (nickname, e-mail):
-----------------------------

    git config --global user.email "mail@domain.com"
    git config --global user.name "login"

To initialize your local repository use:
---------------------------------------
    cd ~/PRAOSP
    repo init -u https://github.com/HeroRickyGAMES/PRAOSP-MANIFEST.git -b praosp-13

Then to sync up:
----------------

    repo sync -j16 --no-clone-bundle
    
Turn on caching to speed up build :
-----------------------------------
    export USE_CCACHE=1
    ccache -M 150G
    
    where 50G corresponds to 50GB of cache. This needs to be run once. Anywhere from 25GB-100GB will result in very noticeably increased build speeds (for instance, a typical 1hr build time can be reduced to 20min). If you’re only building for one device, 25GB-50GB is fine. If you plan to build for several devices that do not share the same kernel source, aim for 75GB-100GB. This space will be permanently occupied on your drive, so take this into consideration.

You can also enable the optional ccache compression. While this may involve a slight performance slowdown, it increases the number of files that fit in the cache. To enable it, run:

    ccache -o compression=true

Start the build :
-----------------
    source build/envsetup.sh
    lunch praosp_devicecodename-userdebug
    make -j8 otapackage
