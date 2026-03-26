# BME280_RP2350B
BME280 temperature, pressure, and humidity driver for the Raspberry PI Pico written in C. 


[RP2350 DATA SHEET](https://pip-assets.raspberrypi.com/categories/1214-rp2350/documents/RP-008373-DS-2-rp2350-datasheet.pdf?disposition=inline)

[BME280 DATA SHEET](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf)


## WIRING
<img width="1225" height="957" alt="image" src="https://github.com/user-attachments/assets/bf9a3d95-eec9-4dab-a6aa-12648febc206" />

Note: In this image, I use an RP2350A and BME280, with I2C0 being used (pins 16/17). ANY i2C pins can be used and you are not limited to these

## How to use:
1. Make sure to edit the serialData, SerialClk, and I2C pins at the top of bme280.c to the pins that you are planning to use. You can find that on Page 18 of the RP2350 DATA Sheet
2. init_i2c() must be used to initialize the i2c peripheral on the RP2350 microcontroller. If this is not done before attempting to use then i2c will not function properly if at all.
3. bme_read_calibration(BME280_ADDRESS) also needs to be called. This will test whether or not the BME280 chip is connected to the microcontroller properly or not. The expected return addresses can be found in "bme280.h".
4. Call read_temp(), read_pressure(), and read_humidity() to obtain their respective raw data then use their respective calculate functions to obtain real data.


- calculate_temp() must be called before calculate_humidity() and calculate_pressure() because it calculates t_fine which is used to find the pressure and humidity (because temperature is needed for both).
- Design tested on the RP2350B Proton board with PlatformIO
