```# Container build for wine staging
 
apt update && apt install curl
echo "deb http://{{ubuntu-mirror}}/mirrors/stable/winehq bionic main" >> /etc/apt/sources.list.d/winehq.list
curl -o wine.key https://dl.winehq.org/wine-builds/winehq.key
apt-key add wine.key
dpkg --add-architecture i386
apt update && apt dist-upgrade
apt install --fix-broken
apt install wget unzip cabextract p7zip-full
x11-apps apt-transport-https \
        ca-certificates \
        cabextract \
        gosu \
        gpg-agent \
        p7zip \
        pulseaudio-utils \
        software-properties-common \
        unzip \
        wget vim \
        winbind \
        zenity
 
wget https://download.opensuse.org/repositories/Emulators:/Wine:/Debian/xUbuntu_18.04/amd64/libfaudio0_19.07-0~bionic_amd64.deb
wget https://download.opensuse.org/repositories/Emulators:/Wine:/Debian/xUbuntu_18.04/i386/libfaudio0_19.07-0~bionic_i386.deb
dpkg -i libfaudio0_19.07-0~bionic_*
apt install winehq-staging
wget https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks
ln -sf winetricks /usr/local/share/winetricks
useradd --create-home --user-group dockeruser
 
#commit and run again with shared X socket
export WINEARCH=win64
wineboot
winetricks corefonts dotnet472 d3dcompiler_47 --force --unattended
 
#docker container run --it -e DISPLAY:${DISPLAY} -v /tmp/.X11-unix:/tmp/.X11-unix -v /home/$(whoami)/.XAuthority:/home/dockeruser/.XAuthority
 
# change flux user id to UID and chown -R UID:GID /home/dockeruser
chmod +x /winetricks```
