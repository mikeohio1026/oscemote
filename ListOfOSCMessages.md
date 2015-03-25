# Introduction #

Here is a list of all the OSC messages that OSCemote's built-in panels can send.

# Start Up #

When OSCemote first connects it sends a greeting that uniquely identifies the device that OSCemote is running on.  You can use this to allow for more than one OSCemote device to control different things on the same OSC host without worrying about what ip address the WiFi network has assigned to each of them.

```
/hello OSCemote@{deviceID}
```

For example:

```
/hello OSCemote@0a80e9315c31e13c17cf48339fc933a327cb6138
```

# Buttons #

Buttons are labeled by row A-E and column 1-3.  They send on/off events as int values 0 and 1.

```
/button/{row}{col} {value}
```

For example, pressing three buttons in the top row one at a time would send:

```
/button/A1 1
/button/A1 0
/button/A2 1
/button/A2 0
/button/A3 1
/button/A3 0
```

# Sliders #

Sliders are numbered 1-6.  They send float values between 0 and 1.

```
/slider/{number} {value}
```

For example, slider number 1 might send:

```
/slider/1 0.0
/slider/1 0.1
/slider/1 0.2
/slider/1 0.3
```

# Segmented Control #

The segmented control at the bottom of the sliders panel sends the label of the selected segment.  The segment has an id number 0 to allow for more in the future.

```
/segmented/{id} {value}
```

For example, pressing A, then B, then C sends:

```
/segmented/0 A
/segmented/0 B
/segmented/0 C
```

# Switches #

The switches at the bottom of the sliders panel send on/off events as int values 0 or 1.

```
/switch/{id} {value}
```

For example, turning the first switch on, then off sends:

```
/switch/1 1
/switch/1 0
```

# Accelerometer #

When you turn the accelerometer on or off, it sends an event with an int value 1 or 0 indicating on or off.  When turned on, it sends a stream of 3-axis acceleration events with float values measured roughly in Gs (1.0 g = 9.81 meters per second per second = Earth's gravity).

```
/accelerometer {enabled}
/acceleration/xyz {x} {y} {z}
```

For example, turning it on, shaking the phone and then turning it off again sends:

```
/accelerometer 1
/acceleration/xyz 0.109012 -0.763081 -0.635901
/acceleration/xyz 0.199855 -0.763081 -0.763081
/acceleration/xyz 0.436047 -0.872093 -0.872093
/acceleration/xyz 0.181686 -0.890262 -0.363372
/acceleration/xyz -0.508721 -0.65407 0.490552
/acceleration/xyz -0.454215 -0.52689 1.01744
/acceleration/xyz -0.0363372 -0.327035 0.25436
/acceleration/xyz 0.890262 -0.327035 -2.16206
/acceleration/xyz 0.890262 -0.981105 -2.32558
/acceleration/xyz 0.0363372 -1.28997 -1.14462
/accelerometer 0
```

# Multi-Touch #

OSCemote's multi-touch panel uses the TUIO protocol to send events over OSC.  This is not just a simple XY-pad.  The iPhone supports up to 5 simultaneous touches.  You can read all about the TUIO protocol here: http://reactable.iua.upf.edu/?tuio  There are a variety of pre-made components for interpreting TUIO available for PureData, Max, ActionScript, C/C++, python, Quartz Composer and many others.

OSCemote sends each TUIO frame in a single OSC bundle to prevent partial updates.

Note that the touch id numbers are usually small (1-5) but can get larger when you hold one finger and tap others.  This avoids any ambiguity caused by lifting one finger and touching another one in the span of a single TUIO frame.

The basic 2D cursor positions are specified as:
```
/tuio/2Dcur set {touch_id} {x} {y} {velocity_x} {velocity_y} {acceleration}
```

Here is an example of what the messages look like:

```
/tuio/2Dcur source OSCemote@0a839fc215c31e13c14cf48933a327cb60e93138
/tuio/2Dcur set 1 0.41875 0.6691 0 0 0
/tuio/2Dcur alive 1
/tuio/2Dcur fseq 0
/tuio/2Dcur source OSCemote@0a839fc215c31e13c14cf48933a327cb60e93138
/tuio/2Dcur set 1 0.390625 0.63747 -0.439142 -0.493872 10.3189
/tuio/2Dcur alive 1
/tuio/2Dcur fseq 1
/tuio/2Dcur source OSCemote@0a839fc215c31e13c14cf48933a327cb60e93138
/tuio/2Dcur set 1 0.396875 0.610706 0.409134 -1.75201 99.3308
/tuio/2Dcur alive 1
/tuio/2Dcur fseq 2
/tuio/2Dcur source OSCemote@0a839fc215c31e13c14cf48933a327cb60e93138
/tuio/2Dcur set 1 0.415625 0.579075 1.18527 -1.99948 51.4968
/tuio/2Dcur alive 1
/tuio/2Dcur fseq 3
/tuio/2Dcur source OSCemote@0a839fc215c31e13c14cf48933a327cb60e93138
/tuio/2Dcur set 1 0.471875 0.506083 1.75083 -2.27196 19.5399
/tuio/2Dcur alive 1
/tuio/2Dcur fseq 4
/tuio/2Dcur source OSCemote@0a839fc215c31e13c14cf48933a327cb60e93138
/tuio/2Dcur set 1 0.496875 0.476886 1.4853 -1.73465 35.6077
/tuio/2Dcur alive 1
/tuio/2Dcur fseq 5
...
/tuio/2Dcur fseq 70
/tuio/2Dcur source OSCemote@0a839fc215c31e13c14cf48933a327cb60e93138
/tuio/2Dcur set 1 0.525 0.216545 0 0 0
/tuio/2Dcur set 2 0.34375 0.596107 0 -0.0168743 0.117028
/tuio/2Dcur set 3 0.865625 0.525547 0 0 0
/tuio/2Dcur alive 1 2 3
/tuio/2Dcur fseq 71
/tuio/2Dcur source OSCemote@0a839fc215c31e13c14cf48933a327cb60e93138
/tuio/2Dcur set 1 0.53125 0.214112 0.0105537 -0.00410848 0.0191235
/tuio/2Dcur set 2 0.34375 0.593674 0 -0.076675 1.88453
/tuio/2Dcur set 3 0.865625 0.525547 0 0 0
/tuio/2Dcur alive 1 2 3
/tuio/2Dcur fseq 72
/tuio/2Dcur source OSCemote@0a839fc215c31e13c14cf48933a327cb60e93138
/tuio/2Dcur set 2 0.34375 0.593674 0 0 0
/tuio/2Dcur alive 2
/tuio/2Dcur fseq 73
/tuio/2Dcur source OSCemote@0a839fc215c31e13c14cf48933a327cb60e93138
/tuio/2Dcur alive
/tuio/2Dcur fseq 74
```