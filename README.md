# RPi_matrix_16_keypad
RPi3 with matrix membrane 4x4 16 keys Keypad

#### Please improve this project by sending a PR

# Installing prerequisite GPIO modules

## pad4pi vs RPi.GPIO vs RPIO vs wiringpi
Not sure which is better. RPIO claims to be an evolved version, but it seems to have older code than RPi.GPIO.
wiringpi seems to be for more advanced functionality - but not planning to use it for now.
pad4pi seems to have exactly what we need.

## Common installation section:
```
sudo apt-get install build-essential  python3-setuptools python-setuptools #!!!
sudo apt-get install python-dev python3-dev
sudo apt-get install python-pip python3-pip python3-setuptools python-setuptools
sudo apt-get remove python-rpi.gpio python3-rpi.gpio
```

## pad4pi (the one I used in below example)
- Steps (after the above common section):
```
sudo pip install wheel
sudo pip3 install wheel
sudo pip install pad4pi
sudo pip3 install pad4pi
```
- Links: https://pypi.org/project/pad4pi/
The code below uses this pad4pi

## RPi.GPIO
- Steps (after the above common section)
```
sudo apt-get install mercurial
sudo pip install hg+http://hg.code.sf.net/p/raspberry-gpio-python/code#egg=RPi.GPIO
sudo pip3 install hg+http://hg.code.sf.net/p/raspberry-gpio-python/code#egg=RPi.GPIO
```
- Links: https://sourceforge.net/p/raspberry-gpio-python/; for code examples check here: https://github.com/srih4ri/RpiMatrixKeyboard/blob/master/1.py

## RPIO 
- Steps (after the above common section)
```
sudo easy_install -U RPIO
sudo easy_install3 -U RPIO
```
- Links: https://pythonhosted.org/RPIO/

## wiringpi
- Steps (after the above common section)
```
sudo pip install wiringpi
sudo pip3 install wiringpi
```
- Links: https://pinout.xyz/pinout/wiringpi

# Troubleshooting:
1. Note the Pinout. There are multiple numbering schemes: BCM(Broadcom), Board(physical pin numbers), wiringpi, etc.
   **Solution** is: in your library you have a function to choose the numbering scheme. In my example below is BCM.
   
2. If you get an error like:
"unable to execute 'arm-linux-gnueabihf-gcc': No such file or directory
error: Setup script exited with error: command 'arm-linux-gnueabihf-gcc' failed with exit status 1 "
**Solution** is: Check the above Common installation section: `apt-get install build-essential`

3. If you get an error like:
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

For more advanced things try python module wiringpi
- https://pinout.xyz/pinout/wiringpi

Pinout links:
- https://pinout.xyz/pinout/ 
- http://pi4j.com/pins/model-3b-rev1.html (just to confirm model3b has same pinout)
- https://sourceforge.net/p/raspberry-gpio-python/wiki/TechRef/  (Tech Refence - BCM2835_GPIOs description pdf)


# Code options:
- cpp (instead of python): https://github.com/ilhamadun/WiringPiKeypad

# Finally the 4x4 keypad app is:
```python
from pad4pi import rpi_gpio
import time

# Setup Keypad
KEYPAD = [
        ["1","2","3","A"],
        ["4","5","6","B"],
        ["7","8","9","C"],
        ["*","0","#","D"]
]

# same as calling: factory.create_4_by_4_keypad, still we put here fyi:
ROW_PINS = [4, 14, 15, 17] # BCM numbering
COL_PINS = [18, 27, 22, 23] # BCM numbering

factory = rpi_gpio.KeypadFactory()

# Try factory.create_4_by_3_keypad
# and factory.create_4_by_4_keypad for reasonable defaults
keypad = factory.create_keypad(keypad=KEYPAD, row_pins=ROW_PINS, col_pins=COL_PINS)

#keypad.cleanup()

def printKey(key):
  print(key)
  if (key=="1"):
    print("number")
  elif (key=="A"):
    print("letter")

# printKey will be called each time a keypad button is pressed
keypad.registerKeyPressHandler(printKey)

try:
  while(True):
    time.sleep(0.2)
except:
 keypad.cleanup()

#keypad.cleanup()
```

