# 10 things to do after you get your ClockworkPi uConsole

Unless you bought your uConsole from ebay for way too much money or you bought it from a sketchy Alliexpress seller, you probably waited months to receive it. Once you have it, the question is, what now? Well, The first thing you probably did was assemble it, I am not going to cover that, there are plenty of Youtube videos out there for that. I am going to cover the things I had to do after I assembled it to get it where I wanted it to be in terms of software and usability. Here are the 10 things you can do to improve your uConsole experience. This list does require some working knowledge of Linux and Raspberry Pi's in general.

As a side note, I have provided Amazon links to the products I purchased for my uConsole. These products are not the "Best in Class" or anything like that. They are simply what I bought and they seem to work for my purposes.

1. Get the Community OS image

The first thing to do is to boot to the SD card sent with the uConsole, if you did not get an SD card, get a 32GB SD card and download the stock image.

https://github.com/clockworkpi/uConsole/tree/master#uconsole-os-images

Burn it to the SD card and boot your uConsole with it. Test it out, make sure everything works. Now shut it down, remove this card and set it aside. This is your base line, if something goes wrong you can always boot off this SD card to make sure your problem is not just wonky software.

Next get a 64, 128 or bigger SD card, a 32 GB SD will fill up fast. Go download the community image.

https://forum.clockworkpi.com/t/bookworm-6-6-y-for-the-uconsole-and-devterm/13235

This image is based on a much newer version of the Raspberry Pi image along with an updated kernel. Burn this image to the larger SD card. Use it to boot up your uConsole and make sure everything works.

2. Update your system

Having an up to date system is paramount for any system, run these commands on a regular basis.

    sudo apt update
    sudo apt upgrade

If you run an upgrade and loose Wi-Fi after the system is rebooted, you can fix this by opening a terminal and running "sudo raspi-config", then going to Advanced Options > Network Config and selecting dhcpcd instead of Network Manager, then reboot. If you don’t see that option in raspi-config, update the tool by hitting update it will then showup. 

3. Install useful programs

The first set of programs are text mode programs that I find useful, the second set are GUI programs I use. Adjust according to taste.

    sudo apt install mc links cmus htop neofetch tmux ffmpeg net-tools build-essential lame zsh mailutils git default-jre tty-clock calcurse git wget curl flex bison bc libavcodec-extra -y

    sudo apt install synaptic tilix audacious flameshot thunderbird filezilla transmission remmina gdebi thonny vlc zim code -y

4. Change Desktop Environment (DE)

I am not a big fan of Wayfire or Wayland. If you want to change your DE to something else, use Tasksel to install the DE of your choice. I would also select Debian desktop environment, this will install things like LibreOffice and GIMP, but if you prefer a minimal setup, then leave it unchecked.

    sudo tasksel

If you do this, if the default Display Manager does not let you change your DE, for that you will need to install sddm.

    sudo apt install sddm

The problem with sddm is when you reboot it will be sideways, so follow the next set of instructions to correct the screen orientation for sddm before you reboot.

    sudo echo "xrandr --output DSI-1 --rotate right" >>  /usr/share/sddm/scripts/Xsetup
    sudo echo "[X11]" >> /var/lib/sddm/state.conf
    sudo echo "DisplayCommand=/usr/share/sddm/scripts/Xsetup" >> /var/lib/sddm/state.conf

Once you have logged into your new DE, you will likely have to go to the display settings and rotate the display.

5. Safely Overclock your uConsole

The Raspberry Pi Compute Module CPU speed is 1.5 Ghz, and the GPU speed is 500 Mhz. Most people find this barely usable. You can kick this up by overclocking your CPU and GPU. I have done this many times with various Raspberry Pi 4's and I have never had a problem with these settings. While this speed is still not great, you will find the system much more usable. Run the following command;

    sudo nano /boot/firmware/config.txt

add these lines to the bottom of the file, save and reboot.

    over_voltage=6
    arm_freq=2000
    gpu_freq=750
    gpu_mem=256

After your reboot run;

    vcgencmd measure_clock arm

To make sure your CPU is running at 2 Ghz. You can try to set the CPU speed higher using arm_freq=2147, but not all devices will handle this speed gracefully. If you are going to experiment, please do so carefully and don't blame me if your shit breaks.

6. Setup Firewall

If you are going to be using your uConsole in public places, you will want to take some steps to secure it from bad actors. Before you enable the firewall, you will want to allow ssh connections through your firewall so you can connect to it remotely.

    apt install ufw
    sudo ufw allow ssh
    sudo ufw enable

7. Secure ssh access to your system

Next you will want to setup your uConsole so it will only accept ssh connections from system you want it to. First log into your uConsole from the system you want to access it from, then log back out, then run the following command to generate a private and public key set.

    ssh-keygen

Just hit enter three times to generate the keys. Next you will want to copy your public key to your uConsole with the following command;

    ssh-copy-id remote_username@remote_server_ip_address

Now you should be able to log in using ssh, but the uConsole will not require a password. Repeat these steps from each machine you want to remotely access the uConsole from. Once you have done that, you will now want to disable password authentication so that only connections from systems that the uConsole has a key for will be allowed to log in. Run the following command;

    sudo nano /etc/ssh/sshd_config

Search for the line "#PasswordAuthentication yes", delete the # and change yes to no. Save the file and then reboot the system.

8. Install Flatpak

Raspberry Pi OS has the same issue as Debian, the packages tend to fall behind long before a new release is made.  If you have programs that you want to stay up to date on, Flatpak is the way to do it.

    sudo apt install flatpak
    flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo

Now you can install programs from the Flatpak repo, which will be more up to date without breaking your install. For instance, if you want to install Discord, run the following;

    flatpak install --user --assumeyes flathub com.discordapp.Discord

You can go to https://flathub.org/ to see what programs are available.

9. Get a screen protector

LCD screens are prone to  getting scratched, so this is a necessary step to preserve you investment in this device. Fortunately the uConsole screen is pretty close to the Blackmagic Pocket Cinema 6K Camera in screen size, so almost any screen protector for it will work for a uConsole. These are not a perfect fit, but they are good enough.

https://www.amazon.com/dp/B07WCQD1NZ?ref=ppx_yo2ov_dt_b_product_details&th=1 

10. Get a carrying case

A nice hard shell is also a good idea. The one I am using is Hermitshell Hard Travel Case. It is designed for VR headsets, but works great for the uConsole and accessories.

https://www.amazon.com/gp/product/B01DVMTJQE/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1

Bonus. Build Emacs from source

This is not particularly necessary, you could just install it with "apt install emacs" or "flatpak install flathub org.gnu.emacs", but what fun is that. Besides showing your Hacker Street Cred, this is also a good way to stretch the legs of your new uConsole and make sure that the overclock settings are not causing any problems. For this exercise you will need to enable the source repo's in /etc/apt/sources.list and run "sudo apt update".

    sudo apt install build-essential libgtk-3-dev libwebkit2gtk-4.0-dev
    sudo apt build-dep emacs 

    git clone https://github.com/emacs-mirror/emacs.git
    cd emacs
    ./autogen.sh
    mkdir build
    cd build
    ../configure --with-cairo --with-xwidgets --with-x-toolkit=gtk3
    make -j4
    sudo make install

Alternatively, if you prefer Neovim, here is how to build it from source.

    sudo apt-get install ninja-build gettext libtool libtool-bin autoconf automake cmake g++ pkg-config unzip curl doxygen
    sudo apt build-dep neovim

    git clone https://github.com/neovim/neovim.git
    cd neovim
    make -j4 CMAKE_BUILD_TYPE=RelWithDebInfo
    sudo make install

