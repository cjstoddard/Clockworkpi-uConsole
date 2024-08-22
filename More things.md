# More things to do after you get your ClockworkPi uConsole

1. Fix WiFi reception

One well known issue with the uConsole is the weak Wifi reception.

The first thing to do is check to make sure you connected the antenna to the CM4 and not the converter board, that is there for the 4G module to use.

The second thing to do is open config.txt and check to make sure you have the correct settings.

    sudo nano /boot/firmware/config.txt

Look for this line, if it is not there, add it to the end of the file.

    dtparam=ant2

Oddlly enough, if you find this setting is already there, try removing it. Some folks have reported that they get better reception without this settings, me included. I personally found my recption improved by about 15% without the setting. 

If you have done this or it was already done with no improvement, the next step is to add a strip of thick double sided tape between the antenna and the chasis. This lifts it up a bit and gets it off the metal, for me this increased the signal from about 45% to 65%.

If the tape does not work for you, then you will probably need to get an external antenna. There are several ways to mount it. All of these methods are fiddly and most depend on you having access to a 3D printer. 

I have uploaded the stl files various mounting methods, I did not create any of these stl's, I found all of them on Printable and Thingaverse. You can find more by searching uConsole on either site.

2. 3D print a front cover

For a little extra protection when carrying your uConsole around 3D print a cover for it. The stl is in the stl folder.

3. Make the terminal more readable

The small screen can be hard to read, especially for older people. In the GUI this is pretty easily fixed by choosing larger fonts. Here is how to get a larger font in the terminal.

    sudo dpkg-reconfigure console-setup

Select your preferred encoding and character set, selecting Terminus as the font, then picking 16x32(the largest size). Of course if you are comfortable with a smaller font you can pick something else, but I find 16x32 is easier to read.

4. Hitchhikers Guide to the Galaxy

Kiwix is on offline browser that lets you store and access all sorts of information locally so you can still access it if you do not have a working internet connection.

    sudo apt install kiwix wget

Start up kiwix, it will be empty, we are just getting the config files in place, go a head and close the program. The next thing we want to do is download some useful zim files. First however, we want to make it easier to download them by making a link in your home directory pointing to the kiwix data directory.

    ln -s .local/share/kiwix kiwix
    cd kiwix

Now we can populate kiwix, you can go check out what they have availble at https://library.kiwix.org/#lang=eng and the direct download site is https://download.kiwix.org/zim. Here are the zim files I downloaded. Please be mindful of the space you have availble on your SD card, many of these files are multi GB in size. The Project Gutenberg zim is 72 GB, which is double all the others combined and will take a good long time to download. If you only have a 32GB SD card, you are not going to be able to download all of them, and even a 128 GB SD card will seem cramped.

    wget https://download.kiwix.org/zim/zimit/based.cooking_en_all_2024-07.zim
    wget https://download.kiwix.org/zim/zimit/fas-military-medicine_en_2024-06.zim
    wget https://download.kiwix.org/zim/other/openstreetmap-wiki_en_all_maxi_2023-05.zim
    wget https://download.kiwix.org/zim/wikibooks/wikibooks_en_all_maxi_2021-02.zim
    wget https://download.kiwix.org/zim/wikipedia/wikipedia_en_simple_all_maxi_2024-06.zim
    wget https://download.kiwix.org/zim/wikisource/wikisource_en_all_maxi_2022-09.zim
    wget https://download.kiwix.org/zim/wikivoyage/wikivoyage_en_all_maxi_2024-06.zim
    wget https://download.kiwix.org/zim/wiktionary/wiktionary_en_all_maxi_2024-05.zim

    wget https://download.kiwix.org/zim/gutenberg/gutenberg_en_all_2023-08.zim

This is not a super well curated collection of zim files, there is no over arcing princple involved beyond useful reference material. If SD card space is not a concern, the first change I would make is replace Simple English Wikipedia with the complete Wikipedia. Be warned though, the compllete Wikipedia is over 100 GB.

5. Reduce wear and tear on your SD Card

Along with being a lot slower, SD cards are not as resiliant hard drives, the number of writes you get on them is limited compared to even low cost SSD drives. One way to help reduce the number of writes to your SD cards is to write log files to a RAM drive. Below is a link to log2ram, which does exactly this. The downsides to this method is first it reduces the amount of RAM available to programs by 128 MB and if for some reason the uConsole looses power or crashes, log files may not be written to the SD card and finding out the problem will be more difficult without proper logs.

https://github.com/azlux/log2ram

6. Checkout other uConsole advise articles

https://gist.github.com/selfawaresoup/b296f3b82167484a96e4502e74ed3602

