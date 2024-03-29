# Zombie Mirror

| <img src="readmeImages/mirror0.jpg"> | <img src="readmeImages/mirror1.jpg"> | <img src="readmeImages/mirror2.jpg"> | <img src="readmeImages/mirror3.jpg"> |
|---|---|---|---|

Zombie Mirror is a project created by [Ben Rush](https://github.com/kwende/) and [Josh Brown Kramer](https://github.com/jbrownkramer/) for Halloween 2019.  Look into the Zombie Mirror, wait for it to find your face, and ... POOF! ... you're a Zombie.  It's a lot of fun at parties.

Behind the scenes, Zombie Mirror consists of a monitor or TV connected to a Raspberry Pi running a program that finds faces.  If it finds one, it sends it up to DeepGrave.me (also created by Josh and Ben) which uses a type of deep neural network called a CycleGAN to zombify the face.

This is the repo for the Raspberry Pi side of the Zombie Mirror project.  If you would like to create your own, follow the instructions below to set up the Raspberry Pi, and see the Instructables page for the rest.

## Required Materials

The following will be part of the final build.
- [Raspberry Pi](https://www.raspberrypi.org/products/).  Note, this build has been tested on a Rasberry Pi 3 Model B+, but it will likely work with other configurations.
- [Raspberry Pi Camera Module](https://www.raspberrypi.org/products/camera-module-v2/) or a web cam.  We've tested with the Camera Module V2.
- [Power supply](https://www.raspberrypi.org/products/raspberry-pi-universal-power-supply/).  Must be 5V, at least 2.5Amps, and end in Micro USB.
- MicroSD Card.
- HDMI Cable
- A monitor or TV that supports HDMI

While setting up, you'll also want 
- A USB Keyboard
- A USB Mouse.
- An SD Card Reader

## Steps

### Put the Zombie Mirror software on the Raspberry Pi
1. Follow [the instructions from raspberrypi.org to get your Pi up and running](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/).
2. Follow [the instructions from raspberrypi.org to set up the Raspberry Pi Camera Module](https://www.raspberrypi.org/documentation/configuration/camera.md).  Or plug in your USB web cam.
4. Open a terminal.
3. Clone this repo.
```
git clone https://github.com/jbrownkramer/zombiemirror/
```
4. Navigate to the repo.
```
cd zombiemirror
```
5. Follow [these instructions](https://www.pyimagesearch.com/2018/09/26/install-opencv-4-on-your-raspberry-pi/) to install opencv.
6. Install required pacakages.
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install libjpeg-dev
pip3 install -r requirements.txt
```
7. Test.
```
python3 ui.py
```
8. Press q to exit.

### Configure Raspberry Pi To Not Sleep
1. Open a root terminal in raspberry Pi.

2. Open "lightdm.conf" file located in, 

     /etc/lightdm/lightdm.conf

3. Add the following line to the `Seat:*` section.

     [Seat:*]
     
     xserver-command=X -s 0 -dpms

Source: https://raspberrypi.stackexchange.com/questions/4773/raspberry-pi-sleep-mode-how-to-avoid

### Optional Configuration

You may need to change some things if your setup isn't exactly like the one described in the Instructables.  Here is an example of all the optional configs.  Details of each configuration appear below.

```
python3 ui.py --cameraorientation 180 --displayorientation 270 --mirrored False --minfacesize 128 --zombietime 5 --fontsize 128 --cameraresolution 1280x720 --webtimeout 6
```

- `--cameraorientation`.  Use this argument to indicate how the camera is oriented.  Default is 180.
     
| <img src="readmeImages/0.png"> | <img src="readmeImages/90.png"> | <img src="readmeImages/180.png"> | <img src="readmeImages/270.png"> |
|---|---|---|---|
| `--cameraorientation 0` | `--cameraorientation 90`  | `--cameraorientation 180`  | `--cameraorientation 270` |

- `--displayorientation`.  Use this argument to indicate how the monitor/TV is oriented.  Default is 270.
     
| <img src="readmeImages/monitor0.png"> | <img src="readmeImages/monitor90.png"> | <img src="readmeImages/monitor180.png"> | <img src="readmeImages/monitor270.png"> |
|---|---|---|---|
| `--displayorientation 0` | `--displayorientation 90`  | `--displayorientation 180`  | `--displayorientation 270` |

- `--mirrored`. Configure True if unaltered image from the camera is mirrored.  Default is False.
- `--minfacesize`. Set this smaller if the mirror tells you to move closer but you're already close.  Default is 128.
- `--zombietime`. Amount of time, in seconds, to display the zombie image.  Default is 5.
- `--fontsize`.  How large the font is.  Default is 128.
- `--cameraresolution`.  Desired camera resolution.  Set it smaller if you want the framerate to be higher.  Default is "1280x720".  
- `--webtimeout`.  Time in seconds to wait for zombie image before timing out.  Default is 6.
