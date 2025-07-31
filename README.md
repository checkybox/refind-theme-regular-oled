# rEFInd theme Regular OLED
This is a fork of [bobafetthotmail's refind-theme-regular](https://github.com/bobafetthotmail/refind-theme-regular) (which is by itself a fork of [munlik's theme](https://github.com/munlik/refind-theme-regular)) which changes the ```bg_dark.png``` to a pitch black image, and also changes ```selection_dark-small.png``` and ```selection_dark-big.png``` accordingly.

This looks really good on OLED screens and I mostly made this for myself, but obviously everyone is free to install this theme too!

I also made some small changes to the ```install.sh``` file:
* ```/boot/EFI/refind``` is now used as the default installation directory
* Default font size changed from ```14``` to ```28```
* Theme's directory name changed to ```refind-theme-regular-oled```
#

A simplistic clean and minimal theme for [rEFInd](https://www.rodsbooks.com/refind/index.html)

NOTE: this is a fork of [munlik's theme](https://github.com/munlik/refind-theme-regular) since he seems to have abandoned his project, he didn't answer to (my) PRs on github for years.

 **Press F10 to take screenshot**
 
(default settings)
![Screenshot 01](https://raw.githubusercontent.com/checkybox/refind-theme-regular-oled/master/src/white_theme.png )

(oled dark theme selected)
![Screenshot 02](https://raw.githubusercontent.com/checkybox/refind-theme-regular-oled/master/src/oled_dark_theme.png)



### Installation [Quick]:

1. Just paste this command in your terminal and enter your choices.
   ```
   sudo bash -c "$(curl -fsSL https://raw.githubusercontent.com/checkybox/refind-theme-regular-oled/master/install.sh)"
   ```
2. To further adjust icon size, font size, background color and selector color edit `/boot/EFI/refind/themes/refind-theme-regular-oled/theme.conf` as root/SuperUser.

### Installation [Manual]:

1. Clone git repository to your `$HOME` directory.
   ```
   git clone https://github.com/checkybox/refind-theme-regular-oled.git
   ```

2. Remove unused directories and files.
   ```
   sudo rm -rf refind-theme-regular-oled/{src,.git}
   ```
   ```
   sudo rm refind-theme-regular-oled/install.sh
   ```

3. Locate refind directory under EFI partition. For most Linux based system is commonly `/boot/efi/EFI/refind/`. Copy theme directory to it. Here, we will copy it to `themes` subdirectory inside refind.

   **Important:** Delete older installed versions of this theme before you proceed any further.

   ```
   sudo rm -rf /boot/efi/EFI/refind/{regular-theme,refind-theme-regular,refind-theme-regular-oled}
   sudo rm -rf /boot/efi/EFI/refind/themes/{regular-theme,refind-theme-regular,refind-theme-regular-oled}
   ```
   ```
   sudo mkdir -p /boot/efi/EFI/refind/themes
   ```
   ```
   sudo cp -r refind-theme-regular-oled /boot/efi/EFI/refind/themes/
   ```

4. To adjust icon size, font size, background color and selector color edit `theme.conf`.
   ```
   sudo vi /boot/efi/EFI/refind/themes/refind-theme-regular-oled/theme.conf
   ```

5. To enable the theme add `include themes/refind-theme-regular-oled/theme.conf` at the end of `refind.conf`, and comment out or delete any other themes you might have installed.
   ```
   sudo vi /boot/efi/EFI/refind/refind.conf

   ```

**NOTE**: If you're not getting your full resolution or having color issues, then try disabling the CSM in your UEFI settings.

### Contribute new icons:

0. Fork this repository on github and then git clone your fork of this repository in your Linux system.

1. The icons must be in `svg` format to allow easy generation of icons at any scale. Canvas size must have width and height 128 px for OS icons, or 48 px for tool icons. The actual icon in the svg file should roughly fit in a square with a side of 96 px or 20 px (for OS and tool icons, respectively). Inkscape is a good program to create and work with svg files.

2. Refind uses the file name to select the right icon, so icons for Linux OS must have the correct OS name from that distro's /etc/os-release file "ID" or ID_LIKE" entries, for example if ID=cachyos the icon name becomes os_cachyos.svg

3. Copy the svg file in `/src/svg/big` or `/src/svg/small` (depending on what is more appropriate) and rename them to be consistent with others.

4. Install inkskape and optipng in your linux system as they will be needed to process the icons by the next step.

5. `cd` in the `./src` directory and run the script `./render_bitmap.sh`, which will process the svg files and generate the png files at various sizes.

6. Copy the `png` icons you generated from their `/src/bitmap` subfolder into the appropriate `/icons` subfolders for their size by running `./copy-bitmap.sh`.

7. Commit your changes, upload to your fork and then open a PR.

**More information**

[rEFInd](http://www.rodsbooks.com/refind/) The official rEFInd website
