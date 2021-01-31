# Parallels Desktop Fixer

Fix Parallels Desktop network and USB loading issues on macOS Big Sur. 

```
#!/usr/bin/env zsh

set -e

color_red="\\033[31m"
color_end="\\033[0m"

dispatcher_desktop_xml="/Library/Preferences/Parallels/dispatcher.desktop.xml"
network_desktop_xml="/Library/Preferences/Parallels/network.desktop.xml"

if [ -f ${dispatcher_desktop_xml} ]; then
    echo "Patching ${color_red}${dispatcher_desktop_xml}${color_end}"
    sudo sed -i '' "s/\(<Usb>\)[^<]*\(<\/Usb>\)/\11\2/" ${dispatcher_desktop_xml}
fi

if [ -f ${network_desktop_xml} ]; then
    echo "Patching ${color_red}${network_desktop_xml}${color_end}"
    sudo sed -i '' "s/\(<UseKextless>\)[^<]*\(<\/UseKextless>\)/\10\2/" ${network_desktop_xml}
fi

echo "Done."
```

Save as `ParallelsDesktopFixer.sh` and `chmod +x ParallelsDesktopFixer.sh`.

```
./ParallelsDesktopFixer.sh
Patching /Library/Preferences/Parallels/dispatcher.desktop.xml
Password:
Patching /Library/Preferences/Parallels/network.desktop.xml
Done.
```
