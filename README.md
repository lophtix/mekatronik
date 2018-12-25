# mekatronik
Lophtix notes about robotics and mechatronics


Set up via `sudo raspi-config`
 * Keyboard layout to match your physical keyboard
 * enable ssh
 * enable camera
 * setup wifi
 * extend filesystem (requires reboot after)
 
Check that camera works by running `raspistill -o image.jpg` if HDMI-display is connected it should show a 5 sec preview before taking and storing image. 

``` bash
$ sudo apt-get update
$ sudo apt-get upgrade
```

Install Tesseract
``` bash
$ sudo apt install tesseract-ocr
```


After checking python works 

``` bash
$ sudo apt-get install python-opencv
$ sudo apt-get install python-picamera python3-picamera
```

These command line calls should now pass without errors  
``` bash
$ python -c "import picamera"
$ python3 -c "import picamera"
```

Now time to combine with openCV:
https://picamera.readthedocs.io/en/release-1.13/recipes2.html#capturing-to-an-opencv-object

Install PyTesseract (not finished) https://pypi.org/project/pytesseract/  
```pip install pytesseract```



How you can get started with Tesseract  
https://medium.freecodecamp.org/getting-started-with-tesseract-part-i-2a6a6b1cf75e  
  
How to use image preprocessing to improve the accuracy of Tesseract  
https://medium.freecodecamp.org/getting-started-with-tesseract-part-ii-f7f9a0899b3f

