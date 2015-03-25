# Introduction #

PureData is a free open source cross platform (Mac, Windows & Linux) application similar to Max/MSP.  PureData (aka Pd) is a very open ended visual programming environment.  You can use it to create synthesized music, visualizations, do audio processing or pretty much anything else.  You can download it for free here: http://puredata.info/downloads

# Details #

Below is an example of using PureData to convert OSCemote messages into a MIDI messages for use in any MIDI compatible software.

# Simple PureData Example #

![http://oscemote.googlecode.com/files/OSCemote-Simple.png](http://oscemote.googlecode.com/files/OSCemote-Simple.png)

  * First download and open [this simple PureData file](http://oscemote.googlecode.com/files/OSCemote-Simple.pd)
  * Now launch OSCemote on your iPhone or iPod Touch.
  * Open your computer's network settings control panel to find your WiFi IP address (usually something like 10.0.1.2 or 192.168.0.2)
  * Go to the Settings tab in OSCemote and enter the IP address of your computer.
  * Make sure the port number in OSCemote and PureData's "dumpOSC" object match (usually 3333).
  * Also make sure your computer's firewall will allow UDP traffic on the port you are using.
  * Now switch to the buttons, sliders or multi-touch view in OSCemote and press something.
  * You should see the values from the button, slider or touch appear in the PureData window.

# OSC to MIDI Bridge #

![http://oscemote.googlecode.com/files/OSCemoteToMIDI-Fancy.png](http://oscemote.googlecode.com/files/OSCemoteToMIDI-Fancy.png)

  * First download and open [this fancy PureData file](http://oscemote.googlecode.com/files/OSCemoteToMIDI-Fancy.pd)
  * Now follow the same steps as the simple example above.
  * You should now see PureData responding to OSCemote.
  * If you have an external MIDI device plugged in to your machine it will now receive MIDI notes.