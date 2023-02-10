### Burning Twin Tiger Shark ROM

**Prerequisites**
* Raspberry Pi (2 model B tested)
* GPIO Connection wires

**Disclaimer** \
I will not be liable for any loss or damage made to anything related to this.
When everything works as expected, this is an easy thing to do. But things like this seldom work the way you expect them to.
If you're using another model of the Raspberry Pi, please make sure to double check the pin out for it, so the connections match their functions.
Raspberry Pi 2,3 and 4 should have the same pin outs.

**Upgrading ROM**
1. Remove the ROM board.

2. Attach wires between the ROM board and the Raspberry Pi as shown in the images at the bottom of this readme.

3. Start and login to your Raspberry Pi

4. Test if you have flashrom installed on your Pi by running: \
   `flashrom` \
   If not, it will need to be downloaded, compiled and installed. \
   Something like this, might depend on what RPI image you're running on: \
   `sudo apt-get install pciutils`\
   `sudo apt-get install libftdi-dev`\
   `sudo apt-get install libusb-dev`\
   `sudo apt-get install libpci-dev`\
   `sudo apt-get install libusb-1.0`\
   `sudo git clone https://github.com/stefanct/flashrom.git` \
   `cd flashrom`\
   `sudo make`\
   `sudo make install`

5. Copy and unpack the ZIP file with the ROMs somewhere to your Pi (found in the binary directory here).\
   `unzip ttsnts_2023-02-10_arcade_lovers.zip` \
   The sh files might need to be chmoded, by running something like:\
   `sudo chmod -R 777 .`\
   in the directory where you unpacked the ZIP.

6. Optional step to change the name at the boot screen.\
   Install JAVA, if it's not already installed, by running:\
   `sudo apt install default-jdk`  \
   Follow the instructions in case of some kind failure. \
   Then run: \
   `./changename name` \
   where `name` is the text you want at the boot screen. \
   Should all be lower case and not use any special characters, of any kind. \
   If you want to use a space in there, make sure to surround the whole text with citation marks. \
   Make sure it's short, otherwise you might make the ROM corrupt.
  
7. Now it's time to burn the ROMs.\
   Connect the wires for burning the CODE ROM. \
   Then run\
   `./write.sh ttsac_codegfx.rom` \
   After the prompt returns, you should see the text `Verifying flash... VERIFIED.` \
   Then you're ready to burn the AUDIO ROM. Connect the wires to go into the Audio connector on the ROM board, then run: \
   `./write.sh ttsac_audio.rom`
   
You're done!

**Connections**

Connection shown are to the Code/Gfx ROM. For the Audio ROM, just move the wires one by one to the corresponding pins on the other side of the ROM board:
![Alt text](pictures/home_burning_image_1.png?raw=true "Connections")

Blue goes to ground, green goes to MISO, red to 3.3v, brown to chip select, white to clock and yellow to MOSI: \
![Alt text](pictures/home_burning_image_2.png?raw=true "ROM Board Code connections")

The brown wire (chip select, pin 24) is somewhat hidden in this image: \
![Alt text](pictures/home_burning_image_3.png?raw=true "RPI connections")

Raspberry Pi pin outs: \
![Alt text](pictures/home_burning_image_4.png?raw=true "RPI pin outs")
