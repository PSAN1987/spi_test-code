# spi_test-code
- This code can be reference to send data and receive data by SPI of Raspberry Pi4 using C-language
- It is just loop back to check if SPI TX to SPI RX is correct or not
- Original code and trouble shooting are referenced with links beloew
https://tomosoft.jp/design/?p=5428
https://github.com/nRF24/RF24/issues/517

# Build code
- Enable SPI pin using < Preference < Raspberry Pi configuration < Interface < SPI < Enable
- check SPI dev using command below
$ ls /dev/spi*
/dev/spidev0.0 /dev/spidev0.1
- check SPI module (spidev、spi_bcm2708) using command below
$ lsmod
- bcm2835 libray install
$ sudo wget http://www.airspayce.com/mikem/bcm2835/bcm2835-1.59.tar.gz
$ tar zxvf bcm2835-1.59.tar.gz
$ cd bcm2835-1.59/
$ sudo ./configure
$ sudo make
$ sudo make install
- Build code
$ gcc -o spi spi.c -l bcm2835
$ sudo ./spi

#  "bcm2835_init: gpio mmap failed: Cannot allocate memory" 
If you face this issue, you need a updated SPI library, so please follow followings instructions
- download patch file: https://github.com/nRF24/RF24/commit/e221acdc4315a39016b31c28143639b27421d75a
$ cd bcm2835-1.59/
$ patch -lNp1 --input=/path/to/patch/bcm2835_rpi4.patch " You need to change path to patch to yours
$ sudo ./configure
$ sudo make
$ sudo make install
This can resolve gpio mmap failed issue 
