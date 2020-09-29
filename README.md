# cross_compile_qt5_guide

```sh
apt install libgles2-mesa-dev libgbm-dev libdrm-dev 

apt install libudev-dev libinput-dev libxkbcommon-dev libts-dev libnss3-dev bluez libbluetooth-dev \
  libkrb5-dev libcups2-dev libfontconfig1-dev libdbus-1-dev

apt install libasound2-dev libspeechd-dev speech-dispatcher libjpeg-dev libpng-dev libtiff-dev \
  libwebp-dev libassimp-dev libharfbuzz-dev  libpulse-dev libopenal-dev libproxy-dev 
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

