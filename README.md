
Check out my entry on https://appdb.winehq.org when it's approved.
I am using Linux Mint Cinnamon 19 with an nVidia Graphic Card
In order to be able to install MoviePlus, you should use Wine 4.12.1 staging - couldn't get it to work with 4.15
I used the following tutorial for Serif's new program Affinity to solve a lot of the problems with the install.

Tutorial (Lots of credit to this guy, I worked out that it was likely that the process was probably similar to the Affinity install hence I used this): https://forum.affinity.serif.com/index.php?/topic/94180-running-affinity-on-linux-finally-works/&tab=comments#comment-501008

Download and extract the correct wine version

    curl -L https://lutris.nyc3.cdn.digita... > wine-lutris-vkchildwindow-4.12.1-x86_64.tar.xz
    
    tar xf wine-lutris-vkchildwindow-4.12.1-x86_64.tar.xz

Set the path to wine for winetricks to work correctly

    export WINE="$PWD/lutris-vkchildwindow-4.12.1-x86_64/bin/wine"

Remove the old wine prefix

    rm -rf ~/.wine
    
    alias wine=$WINE
    
    wine wineboot -i

Press "Cancel" when the window asking you to install "Mono" appears

Install Winetricks

Downloading the newest version of winetricks

    curl -L https://raw.githubusercontent.... > winetricks
    
    chmod +x winetricks

For the following section below you may be prompt to "Restart Now" or "Restart Later" always click "Restart Now"

To prevent errors from mono

`./winetricks remove_mono -`q

For the installer

    ./winetricks dotnet35sp1 -q

For the main application

    ./winetricks dotnet472 -q

Set windows to 8.1, since aero is not found if set to win7

    ./winetricks win81 -q

Run the install for MoviePlus

    wine movieplus.exe

You be prompted to install in the same way as on windows

Everything will appear to run without fault until the very end

At the very the installation will say it failed

DO NOT click "Finish"

kill the installation, as MoviePlus will delete install files if it think it failed to install

Find the installation directory for MoviePlus ( note: do not close or cancel the installation window )

Then to prevent the deletion of the install

Change to the Serif directory

    cd "~/.wine/drive_c/Program Files/Serif"

You'll see that MoviePlus is installed in this directory

Rename the directory "MoviePlus" to "MoviePlus1" to prevent the deletion of install files

    mv MoviePlus MoviePlus1

Now You close the installation window for MoviePlus

Then you can rename MoviePlus back to it's correct name

    mv MoviePlus1 MoviePlus

Now you can run MoviePlus

	wine "~/.wine/drive_c/Program Files/Serif/MoviePlus/X6/Program/MoviePlus.exe"

You may see various warning windows but you should be able to ignore most of these

I also had to install directx9 since it is required for MoviePlus to run more smoothly

	./winetricks d3dx9

Also consider changing your GPU memory size for wine, for example for 2048MB used the following

	./winetricks videomemorysize=2048

