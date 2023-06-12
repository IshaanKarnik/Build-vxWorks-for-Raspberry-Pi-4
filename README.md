# Build vxWorks for Raspberry Pi 4

1. 	To create the SD card, download the firmware from: https://github.com/raspberrypi/firmware/archive/1.20200212.tar.gz
		 `wget https://github.com/raspberrypi/firmware/archive/1.20200212.tar.gz`
		
	  Unzip the file using command 
    `tar -xvzf 1.20200212.tar.gz`

	  Format an SD card as a FAT32 file system and copy the contents of the "boot" directory (copy entire folder) from the downloaded firmware to the SD card.

2. 	Compile a u-boot binary for Raspberry Pi 4 (Use January-2023 [v2023.01] u-boot. Latest version can cause the system not to boot) and copy it to the SD card

		E.g. on a Ubuntu/Debian host
		$ sudo apt install python-pip
		$ sudo pip install pyftpdlib
		$ sudo apt install build-essential
		$ sudo apt install gcc-aarch64-linux-gnu
		$ sudo apt install libc6-dev-i386 flex bison bc libssl-dev
		$ git clone https://gitlab.denx.de/u-boot/u-boot.git (Use January-2023 [v2023.01] u-boot. Latest version can cause the system not to boot)
		$ cd u-boot
		$ CROSS_COMPILE=aarch64-linux-gnu- make rpi_4_defconfig
		$ CROSS_COMPILE=aarch64-linux-gnu- make

3.    Copy u-boot.bin to the SD card as u-boot-64.bin

Download VxWorks Software Development Kit (SDK) from https://forums.windriver.com/t/vxworks-software-development-kit-sdk/43
  `wget https://d13321s3lxgewa.cloudfront.net/wrsdk-vxworks7-raspberrypi4b-1.4.tar.bz2`

Extract the downloaded file using command 
	`tar -xvf wrsdk-vxworks7-raspberrypi4b-1.4.tar.bz2`

4.    Copy the files from /vxsdk/sdcard/ to the SD card.

5.    Copy the VxWorks kernel image /vxsdk/bsps/rpi_4_0_1_3_0/uVxWorks to the SD card.  (use uVxWorks and not others)

6.    Connect a USB to TTL serial cable to the Raspberry Pi

On the Raspberry Pi 4 Model, GPIOs 14 and 15 are used as UART transmit and receive pins (Mini UART).

Bps/Par/Bits       : 115200 8N1

Hardware Flow Control : No

Software Flow Control : No
