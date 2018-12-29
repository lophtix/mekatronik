Update:  
```sudo apt-get update && sudo apt-get upgrade```
  
Setup with raspi-config:  
```sudo raspi-config```  
  
**Network Options:**
* Hostname > set hostname to rosberrypi2.X  
* Wi-Fi > connect to wi-fi  

**Boot Options:**  
* Desktop / CLI > select *Console Autologin*  
* Splash Screen > turn off splash screen  

**Localisation Options:**  
* Change Keyboard Layout > set keyboard layout to Swedish  

**Interfacing Options:**  
* Camera > enable camera  
* SSH > enable SSH  

**Advanced Options:**  
* *Expand Filesystem*  
  
Install pijuice software and remove lock file:
```
sudo apt-get pijuice-base
sudo rm /tmp/pijuice_gui.lock
```  

