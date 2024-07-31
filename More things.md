# More things to do after you get your ClockworkPi uConsole

1. Fix WiFi reception

One well known issue with the uConsole is the weak Wifi reception.

The first thing to do is check to make sure you connected the antenna to the CM4 and not the converter board, that is there for the 4G module to use.

The second thing to do is open config.txt and check to make sure you have the correct settings.

    sudo nano /boot/firmware/config.txt

Look for this line, if it is not there, add it to the end of the file.

    dtparam=ant2

Oddlly enough, if youo find this setting is already there, try removing it. Some folks have reported that they get better reception withought this settings, me included. I personally found my recption improved by about 15% without the setting. 

If you have done this or it was already done with no improvement, the next step is to add a strip of thick double sided tape between the antenna and the chasis. This lifts it up a bit and gets it off the metal, for me this increased the signal from about 45% to 65%.

If the tape does not work for you, then you will probably need to get an external antenna. There are several ways to mount it. All of these methods are fiddly and most depend  on you having access to a 3D printer. 

 I have uploaded the stl files various mounting methods, I did not create any of these stl's, I found all of them on Printable and Thingaverse. You can find more by searching uConsole on either site.

2. 3D print a front cover

For a little extra protection when carrying your uConsole around 3D print a cover for it. The stl is in the stl folder.

3. Make the terminal more readable

The small screen can be hard to read, especially for older people. In the GUI this is pretty easily fixed by choosing larger fonts. Here is how to get a larger font in the terminal.

    sudo dpkg-reconfigure console-setup

Select your preferred encoding and character set, selecting Terminus as the font, then picking 16x32(the largest size). Of course if you are comfortable with a smaller font you can pick something else, but I find 16x32 is easier to read.
