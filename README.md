# LIS2DU12

Arduino library to support the LIS2DU12 ultra-low-power 3D accelerometer

## API

This sensor uses I2C, I3C or SPI to communicate.
For I2C it is then required to create a TwoWire interface before accessing to the sensors:  

    TwoWire dev_i2cf(I2C_SDA, I2C_SCL);  
    dev_i2c.begin();

For SPI it is then required to create a SPI interface before accessing to the sensors:  

    SPIClass dev_spi(SPI_MOSI, SPI_MISO, SPI_SCK);  
    dev_spi.begin();

For I3C it is then required to create an I3C interface before accessing to the sensors:

    I3C.begin(I3C_SDA, I3C_SCL, 1000000U);

An instance can be created and enabled when the I2C bus is used following the procedure below:  

    LIS2DU12Sensor Accelero(&dev_i2c);
    Accelero.begin();
    Accelero.Enable_X();

An instance can be created and enabled when the SPI bus is used following the procedure below:  

    LIS2DU12Sensor Accelero(&dev_spi, CS_PIN);  
    Accelero.begin();
    Accelero.Enable_X();

An instance can be created and enabled when the I3C bus is used with SETDASA (static-to-dynamic address assignment):

    LIS2DU12Sensor Accelero(&I3C, LIS2DU12_I3C_ADD_H);
    I3C.resetDynamicAddresses();
    I3C.assignDynamicAddress(Accelero.getStaticAddress(), LIS2DU12_DYNAMIC_ADDRESS);
    Accelero.begin(LIS2DU12_DYNAMIC_ADDRESS);
    I3C.setClock(12500000);
    Accelero.Enable_X();

The access to the sensor values is done as explained below:  

  Read accelerometer.  

    int32_t accelerometer[3];
    Accelero.Get_X_Axes(accelerometer);  

# Examples

There are several examples with the LIS2DU12 library.
* LIS2DU12_DataLog_Terminal_I2C: This application shows how to get accelerometer data from the LIS2DU12 sensor over I2C and print them on terminal.
* LIS2DU12_Datalog_Terminal_I3C: This application shows how to use the LIS2DU12 sensor over I3C using SETDASA.

## Documentation

You can find the source files at  
https://github.com/stm32duino/LIS2DU12

The LIS2DU12 datasheet is available at  
https://www.st.com/content/st_com/en/products/mems-and-sensors/accelerometers/lis2du12.html
