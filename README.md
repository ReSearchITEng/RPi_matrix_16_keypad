# RPi_matrix_16_keypad
RPi3 with matrix membrane 16 keys Keypad using GPIO pinout

# Please improve this by sending a PR

# Installing prerequisite GPIO modules

## RPi.GPIO vs RPIO vs wiringpi2
Not sure which is better. RPIO claims to be an evolved version, but it seems to have older code than RPi.GPIO.
Just installed and tested both.
wiringpi2 seems to be for more advanced functionality. 
Not planning to use it for now.

## Common installation section:
```
sudo apt-get install build-essential  python3-setuptools python-setuptools #!!!
sudo apt-get install python-dev python3-dev
sudo apt-get install python-pip python3-pip python3-setuptools python-setuptools
sudo apt-get remove python-rpi.gpio python3-rpi.gpio
```

## RPi.GPIO
- Steps (after the above common section)
```
sudo apt-get install mercurial
sudo pip install hg+http://hg.code.sf.net/p/raspberry-gpio-python/code#egg=RPi.GPIO
sudo pip3 install hg+http://hg.code.sf.net/p/raspberry-gpio-python/code#egg=RPi.GPIO
```
- Links: https://sourceforge.net/p/raspberry-gpio-python/

## RPIO 
- Steps (after the above common section)
```
sudo easy_install -U RPIO
sudo easy_install3 -U RPIO
```
- Links: https://pythonhosted.org/RPIO/

## wiringpi2
- Steps (after the above common section)
```
sudo pip install wiringpi2
sudo pip3 install wiringpi2
```
- Links: https://pinout.xyz/pinout/wiringpi

# Troubleshooting:
2. If you get an error like:
"unable to execute 'arm-linux-gnueabihf-gcc': No such file or directory
error: Setup script exited with error: command 'arm-linux-gnueabihf-gcc' failed with exit status 1 "
**Solution** is: Check the above Common installation section: `apt-get install build-essential`

2. If you get an error like:
"The installation directory you specified (via --install-dir, --prefix, or
the distutils default setting) was:

    /usr/local/lib/python2.7/dist-packages/

This directory does not currently exist.  Please create it and try again, or
choose a different installation directory (using the -d or --install-dir
option).
"
**Solution** is: 
`ln -s /usr/lib/python2.7/dist-packages/ /usr/local/lib/python2.7/dist-packages`

Links I tried to follow:
- https://www.raspberrypi.org/forums/viewtopic.php?t=81675

For more advanced things try python module wiringpi2
- https://pinout.xyz/pinout/wiringpi

Pinout links:
- https://pinout.xyz/pinout/ 
- http://pi4j.com/pins/model-3b-rev1.html (just to confirm model3b has same pinout)
- https://sourceforge.net/p/raspberry-gpio-python/wiki/TechRef/  (Tech Refence - BCM2835_GPIOs description pdf)
