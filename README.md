# cross_compile_qt5_guide

```sh
apt install libgles2-mesa-dev libgbm-dev libdrm-dev 

apt install libudev-dev libinput-dev libxkbcommon-dev libts-dev libnss3-dev bluez libbluetooth-dev \
  libkrb5-dev libcups2-dev libfontconfig1-dev libdbus-1-dev

apt install libasound2-dev libspeechd-dev speech-dispatcher libjpeg-dev libpng-dev libtiff-dev \
  libwebp-dev libassimp-dev libharfbuzz-dev  libpulse-dev libopenal-dev libproxy-dev 
  
```
```
sudo apt install flite1-dev libspeechd-dev speech-dispatcher libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-good1.0-dev libdrm-dev flex ruby gperf bison libts-dev libdbus-1-dev libudev-dev libicu-dev libsqlite3-dev libxslt1-dev libssl-dev libnss3-dev libasound2-dev libavcodec-dev libavformat-dev libswscale-dev libpulse-dev libcpuset-dev freetds-dev libsqlite0-dev libpq-dev libiodbc2-dev libmysqlclient-dev firebird-dev libpng-dev libjpeg-dev libxdamage-dev libxrender-dev libxcb-render0-dev libxcb-render-util0-dev libxcb-shape0-dev libxcb-randr0-dev libxcb-xfixes0-dev libxcb-sync-dev libxcb-shm0-dev libxcb-icccm4-dev libxcb-keysyms1-dev libxcb-image0-dev libxkbcommon-dev libxkbcommon-x11-dev libfontconfig1-dev libfreetype-dev libfreetype6-dev libxi-dev libxext-dev libx11-dev libx11-xcb-dev libxcb1-dev libsm-dev libice-dev libglib2.0-dev libgst-dev libxcb-sync0-dev libfontconfig1-dev libxfixes-dev libxcb-glx0-dev 

sudo apt-get install libopenal1 libopenal-dev libbluetooth-dev libkrb5-dev libassimp-dev libsdl2-dev  libinput-dev libxcb-xinerama0-dev libxcb-xinerama0 libatspi2.0-dev libxcomposite-dev libxcursor-dev libxcb-cursor-dev libclippoly-dev 

sudo apt-get install libsctp-dev libmd4c-dev libxcb-xinput-dev libwayland-dev libre2-dev libopus-dev libvpx-dev libsnappy-dev libminizip-dev libevent-dev libjsoncpp-dev libprotobuf-dev liblcms2-dev

sudo apt-get install libclipper-dev libwayland-dev libwayland-egl-backend-dev waylandpp-dev libwayland-egl1-mesa libwayland-egl++0 libvulkan-dev mesa-vulkan-drivers libgegl-dev libgbm-dev libegl1-mesa libegl1 libgles2 libgles2-mesa libegl1-mesa-dev libgles2-mesa-dev libglvnd-dev libgles1 mesa-common-dev

```

```sh
max_usb_current=1
hdmi_force_hotplug=1
hdmi_group=2
hdmi_mode=87
hdmi_timings= 1024 0 168 32 120 600 0 15 6 14 0 0 0 60 0 51200000 3
hdmi_drive=1
```

```
sudo sed -i "s/raspbian.raspberrypi.org/mirrors.bfsu.edu.cn\/raspbian/g" /etc/apt/sources.list
sudo sed -i "s/archive.raspberrypi.org\/debian/mirrors.bfsu.edu.cn\/raspberrypi/g" /etc/apt/sources.list.d/raspi.list

```

```
rsync -avz pi@192.168.3.5:/lib rootfs
rsync -avz pi@192.168.3.5:/usr/include rootfs/usr
rsync -avz pi@192.168.3.5:/usr/lib rootfs/usr
rsync -avz pi@192.168.3.5:/opt/vc rootfs/opt

```

```
mv rootfs/usr/lib/arm-linux-gnueabihf/libEGL.so.1.0.0 rootfs/usr/lib/arm-linux-gnueabihf/libEGL.so.1.0.0_backup
ln -s rootfs/opt/vc/lib/libEGL.so rootfs/usr/lib/arm-linux-gnueabihf/libEGL.so.1.0.0

mv rootfs/usr/lib/arm-linux-gnueabihf/libGLESv2.so.2.0.0 rootfs/usr/lib/arm-linux-gnueabihf/libGLESv2.so.2.0.0_backup
ln -s rootfs/opt/vc/lib/libGLESv2.so rootfs/usr/lib/arm-linux-gnueabihf/libGLESv2.so.2.0.0

ln -s rootfs/opt/vc/lib/libEGL.so rootfs/opt/vc/lib/libEGL.so.1
ln -s rootfs/opt/vc/lib/libGLESv2.so rootfs/opt/vc/lib/libGLESv2.so.2

wget https://raw.githubusercontent.com/riscv/riscv-poky/master/scripts/sysroot-relativelinks.py
chmod +x sysroot-relativelinks.py
sysroot-relativelinks.py rootfs
```

```
// client
ssh-keygen -t rsa 
cat ~/.ssh/id_rsa.pub | ssh -o StrictHostKeyChecking=no pi@192.168.3.5 "mkdir -p .ssh && chmod 700 .ssh && cat >> .ssh/authorized_keys"

