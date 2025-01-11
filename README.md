# Linux

Ubuntu xfce 
https://github.com/Day21cyber/Linux/blob/main/Ubuntu%20xfce.sh

##sript
```copy
#!/bin/bash

# Memperbarui Termux
echo "Memperbarui Termux..."
pkg update && pkg upgrade -y

# Instalasi proot-distro dan paket pendukung
echo "Menginstal proot-distro dan paket pendukung..."
pkg install -y proot-distro wget curl git neovim tightvncserver lxqt openbox

# Menginstal Ubuntu melalui proot-distro
echo "Menginstal Ubuntu..."
proot-distro install ubuntu

# Masuk ke Ubuntu untuk konfigurasi
echo "Konfigurasi awal Ubuntu..."
proot-distro login ubuntu -- bash -c "
apt update && apt upgrade -y
apt install -y lxqt openbox tightvncserver dbus-x11 wget curl
"

# Konfigurasi VNC Server
echo "Mengatur VNC server..."
proot-distro login ubuntu -- bash -c "
mkdir -p ~/.vnc
echo '#!/bin/bash
xrdb ~/.Xresources
startlxqt &' > ~/.vnc/xstartup
chmod +x ~/.vnc/xstartup
tightvncserver :1
"

# Instalasi Visual Studio Code
echo "Menginstal Visual Studio Code..."
proot-distro login ubuntu -- bash -c "
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
rm microsoft.gpg
echo 'deb [arch=amd64] https://packages.microsoft.com/repos/code stable main' > /etc/apt/sources.list.d/vscode.list
apt update
apt install -y code
"

# Instalasi Firefox
echo "Menginstal Firefox..."
proot-distro login ubuntu -- bash -c "
apt install -y firefox
"

# Instalasi WPS Office
echo "Menginstal WPS Office..."
proot-distro login ubuntu -- bash -c "
wget -O wps-office.deb https://wdl1.pcfg.cache.wpscdn.com/wps-office_11.1.0.11664.XA_amd64.deb
apt install -y ./wps-office.deb
rm wps-office.deb
"

# Informasi pengguna
echo "Instalasi selesai! Untuk menjalankan Ubuntu dengan GUI:"
echo "1. Jalankan: proot-distro login ubuntu"
echo "2. Jalankan: tightvncserver :1"
echo "3. Gunakan aplikasi VNC Viewer di HP Anda dan sambungkan ke localhost:5901"
```
---
