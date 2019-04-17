#### Enabling Background in LightDM GTK Greeter

Using the background config entry in /etc/lightdm/lightdm-gtk-greeter.conf in Arch Linux has no effect
if the specified path is something different than /usr/share/background/FILENAME

So the fix is to create the path and to move your wallpaper there.

```
sudo mkdir -p /usr/share/backgrounds
sudo cp /home/USERNAME/Downloads/wallpaper.png /usr/share/backgrounds
```

Now edit your greeter.conf to the new path - theme-name, icon-theme-name and font-name are optional
```
[greeter]
background=/usr/share/backgrounds/wallpaper.png
theme-name=Arc-Dark
icon-theme-name=Numix Circle
font-name=Noto Sans
```
