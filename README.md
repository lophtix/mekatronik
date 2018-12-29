# mekatronik
Lophtix notes about robotics and mechatronics 

## Links
* [Programmera LEGO Mindstorms EV3 med Python via webbläsare](Lego-EV3dev.md) (written in Swedish)

-----------------------------------

## Notes to be structured later...

Set up via `sudo raspi-config`
 * Keyboard layout to match your physical keyboard
 * enable ssh
 * enable camera
 * setup wifi
 * extend filesystem (requires reboot after)
 
Check that camera works by running `raspistill -o image.jpg` if HDMI-display is connected it should show a 5 sec preview before taking and storing image. 

```bash
$ sudo apt-get update
$ sudo apt-get upgrade
```


After checking python works 

```bash
$ sudo apt-get install python-opencv
$ sudo apt-get install python-picamera python3-picamera
```

These command line calls should now pass without errors  
```bash
$ python -c "import picamera"
$ python3 -c "import picamera"
```

Now time to combine with openCV:
https://picamera.readthedocs.io/en/release-1.13/recipes2.html#capturing-to-an-opencv-object

Install PyTesseract (not finished) https://pypi.org/project/pytesseract/  
```bash
pip install pillow
(pip install pytesseract)
(pip install opencv-python)
```

Install Tesseract
``` bash
$ sudo apt install tesseract-ocr
(sudo apt-get install tesseract-ocr libtesseract-dev libleptonica-dev)
```
Version 4 of tesseract seems to require compilation for rasperry pi: https://raspberrypi.stackexchange.com/questions/89231/tesseract-ocr-4-x-beta-for-raspberry-pi

For python íntegration there is tesserocr https://github.com/sirfz/tesserocr but we did not get that to work now.




How you can get started with Tesseract  
https://medium.freecodecamp.org/getting-started-with-tesseract-part-i-2a6a6b1cf75e  
  
How to use image preprocessing to improve the accuracy of Tesseract  
https://medium.freecodecamp.org/getting-started-with-tesseract-part-ii-f7f9a0899b3f
  
Detect whitlisted single character:  
```tesseract stdin stdout -c tessedit_char_whitelist=HSU -psm 10```
