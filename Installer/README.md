# **CM6206 Enabler 2.1**

by Alexander Thomas (aka Dr. Lex)

<http://www.dr-lex.be/>

*doctor.lex at gmail.com*



This is a small program that activates the analog and S/PDIF outputs on
USB devices that are based on the C-Media CM6206 surround sound chip
(sometimes also referred to as CMI6206). This IC supports up to 7.1
audio, although many devices only have six channels. Some major brands
also use this chip, for instance Zalman uses it in their ZM-RS6F USB
headphones and the Sweex SC016 is also based on the CM6206.

You can see if you have a CM6206-based device by opening System
Profiler. The device should show up as "USB Sound Device" and have a
Product ID of 0x0102 and Vendor ID of 0x0d8c.



The CM6206 is a fully compliant USB sound card and therefore should
theoretically work out-of-the-box with any operating system that has
support for USB audio built-in, like OS X. In fact, it does work but for
some reason the device powers up with all its outputs disabled, and some
USB commands are required to activate those outputs. That is where this
program comes in. It is not really a driver, it is just an 'activator'.



## **Installing**

Unlike the old version, the program now comes in an installer package
and works transparently in the background. You will need to reboot after
installation.

The program runs as a daemon and will activate every CM6206 device that
is plugged in. It will also reactivate any devices when it detects a
wake-from-sleep.



You can verify whether the daemon works by opening Console.app and
seeing if the line "CM6206 device added"[ 
]{.Apple-converted-space}appears in system.log whenever you plug in the
sound card. If your sound card has an S/PDIF output, it should light up.



If for some reason you still want to run the program manually, I suppose
you\'re tech savvy enough to find the 'cm6206init' binary in the
installer package. Run it with "-h" to see options.



## **Uninstalling**

The installer only installs two files. To uninstall, delete the folder
and file:

[ ]{.Apple-converted-space}*/Library/Application Support/CM6206*

[ ]{.Apple-converted-space}*/Library/LaunchDaemons/be.dr-lex.cm6206init.plist*

Reboot to complete uninstallation.



## **Requirements**

The program should run from OS X 10.4 on, but the last time I tested it,
it failed to activate the CM6206 on anything less than OS X 10.5. For
some reason unknown, all interfaces on the device are "in use" (error
e00002c5) no matter what I try in 10.4.x. I\'m also unsure whether the
launchd plist is compatible with 10.4. In other words, you need at least
10.5.



## **Caveats**

While testing the program, I had several kernel panics when repeatedly
plugging and unplugging the sound card while iTunes was playing and the
JoeSoft "Hear" sound enhancer was active. I avoided this by
incorporating some extra delays in the program, but I cannot guarantee
that the program will not crash in combination with any third-party
tools that have anything to do with audio or USB. I recommend to stop
audio output in all programs whenever you plug in a CM6206 sound card.



The program is written such that it should be able to handle any number
of sound cards, so if you feel like getting 60 output channels by
hooking up as many sound cards as your USB hubs can handle, knock
yourself out. This is not tested however, so I don\'t guarantee that it
will work.



Here are some common *corrections of misconceptions* about CM6206-based
USB sound cards:

1\. The CM6206 is *not able to decode or encode AC3 or DTS streams*. It
is a simple sound card with 6 or 8 discrete output channels. This means
your playback software *must* support built-in 5.1 decoding to get
multi-channel output. For instance VLC is able to do this, but at the
time of this writing, Plex is not.

2\. Most likely, the optical S/PDIF connectors, if your card has any,
are completely *useless* to you except as an 'activity light'. Do not
connect anything to them unless you know what you\'re doing. Most Macs
already have S/PDIF built into their 3.5mm jacks. A 3.5mm optical
adaptor is much cheaper and works without software.

3\. The output S/PDIF on the sound card is nothing but a hardwired copy
of the 'front' channel output. It can theoretically be toggled, but you
cannot route a different signal to the front channel and the S/PDIF: *it
is the same channel*. This is why it doesn\'t show up in system
preferences.



## **Setting up surround sound**

Unfortunately, at the time of this writing it\'s still quite a hassle to
get surround sound properly set up on OS X. Here\'s a checklist of what
you should do to get 5.1 sound out of any multi-channel USB sound card.


1.  Log in using an *administrator account*. Otherwise OS X will
    silently ignore any changes you make to the multichannel setup.
2.  In the Sound control panel, select the USB audio output device.
3.  Open the *'Audio Midi Setup'* program in your Applications/Utilities
    folder.
4.  Select the USB card as output device and set the sampling rate to
    44100 or 48000 depending on the rate of the audio you want to play
    (for a movie it\'s most likely 48k).
5.  Set the number of channels to 6 (6ch-16bit) or 8, depending on your
    device.
6.  Click 'Configure speakers' and choose "5.1 surround". You can click
    the buttons to test each speaker, but mind that the default test
    sound is an *awfully* loud noise (you should drag the 'Audio' slider
    in AMS\' preferences almost fully to the left to fix this).
7.  In your media player (e.g. VLC), you may also need to select the USB
    audio device as output device. Do not enable 'passthrough' or
    'optical out' anywhere.



To test if all channels work in your media player and to calibrate the
volumes, there are many 5.1 test sound files available on the web. Keep
in mind that for movie soundtracks, the LFE channel needs to be
amplified by 10dB to be at the correct level. You should not just hook
up the LFE to your subwoofer and the other channels to the satellites,
but I won\'t go into the details of *bass management* here.

Mind that during the time when I used this sound card with VLC, I
noticed that despite careful calibration, the volume of the surround
channels needed considerable readjustment with pretty much every film I
played. Sometimes the volume of the center channel was wrong as well. My
guess is that the decoder in VLC is missing a part that sets correct
relative channel gains. This, as well as lack of multichannel output in
many other players like Plex, annoyed me to such a degree that I
eventually bought a standalone 5.1 decoder.



## **Version History**

*2009/06: 1.0:*[  ]{.Apple-converted-space}Initial release.

*2011/01: 2.0:*[  ]{.Apple-converted-space}Implemented 'daemon mode' and
provided an installer.

*2011/02: 2.1:*[  ]{.Apple-converted-space}Prevented the program from
delaying the computer while going to sleep.

*2011/04: 2.1:*[  ]{.Apple-converted-space}Fixed permissions problem in
the installer.



## **Legalese**

This program is released under the GNU General Public License. See the
files main.cpp and COPYING for more details.



This program is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.



This is just a hobby project and I am in no way affiliated with C-Media
or the manufacturer of your particular sound card. I cannot be held
responsible for any damage caused by your sound card or the combination
of your sound card and this program.
