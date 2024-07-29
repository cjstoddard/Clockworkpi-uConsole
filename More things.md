# More things to do after you get your ClockworkPi uConsole

1. Fix WiFi reception

One well known issue with the uConsole is the weak Wifi reception.

The first thing to do is check to make sure you connected the antenna to the CM4 and not the converter board, that is there for the 4G module to use.

The second thing to do is open config.txt and check to make sure you have the correct settings.

    sudo nano /boot/firmware/config.txt

Look for this line, if it is not there, add it to the end of the file.

    dtparam=ant2

If you have done this or it was already done with no improvement, the next step is to add a strip of thick double sided tape between the antenna and the chasis. This lifts it up a bit and gets it off the metal, for me this increased the signal from about 30% to 50%.

If the tape does not work for you, then you will probably need to get an external antenna. There are several ways to mount it. The least destructive is to 3D print a replacement for the left side plate with a hole for the antenna. Below is the antenna I purchased, I have uploaded the stl file for the left side plate so you can print it yourself. The stl actually prints two, it never hurts to have a spare or you can send it to a friend who does not have a 3D printer. I have also uploaded stl files of other non destructive antenna mounts, one of them uses the stock antenna so you do not have to buy an external. I did not create any of these stl's, I found all of them on Printable and Thingaverse. You can find more by searching uConsole on either site.

https://www.amazon.com/gp/product/B08T63H83S/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1

2. Make the terminal more readable

The small screen can be hard to read, especially for older people. In the GUI this is pretty easily fixed by choosing larger fonts. Here is how to get a larger font in the terminal.

    sudo dpkg-reconfigure console-setup

Select your preferred encoding and character set, selecting Terminus as the font, then picking 16x32(the largest size). Of course if you are comfortable with a smaller font you can pick something else, but I find 16x32 is easier to read.

3. 3D print a front cover

For a little extra protection when carrying your uConsole around 3D print a cover for it. The stl is in the stl folder.
