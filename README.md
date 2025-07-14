# SHT4x-python
SHT4x.py is a Python class for interfacing with the Sensirion SHT4x temperature and humidity sensor family via the I²C bus using the [i2cpy](https://github.com/iynehz/i2cpy) library (currently supports CH341 and CH347). This library provides methods to control the sensor, retrieve temperature and humidity readings, reset the sensor, and obtain the serial number.

## Installation

Make sure you have Python 3.x installed. You can install the required i2cpy library using pip:

```console
foo@bar:~$pip install i2cpy
```

## Usage

### Import the `SHT4x` class from the library:

```python
from SHT4x import SHT4x
```
### Create an instance of the SHT4x class:

```python
sensor = SHT4x()
```
### You can optionally customize all the parameters:

```python
from i2cpy import I2C
sensor = SHT4x(i2c=I2C(id="/dev/ch34x_pis0", driver="ch347", freq=100000, auto_init=False), address=0x14, mode="low")
```
### Reading Temperature and Humidity

To retrieve temperature and humidity readings from the sensor, call the update() method:

```python
if sensor.update():
    temperature = sensor.temperature
    humidity = sensor.humidity
    print(f"Temperature: {temperature}°C")
    print(f"Humidity: {humidity}% RH")
else:
    print("Failed to read data from the sensor.")
```
### Setting the Measurement Mode

You can set the measurement mode using the mode property. Valid modes are e.g. "high", "medium", and "low". For example:

```python
sensor.mode = "high"
```
### Resetting the Sensor

To reset the sensor to its default state, use the reset() method:

```python
if sensor.reset():
    print("Sensor reset successful.")
else:
    print("Failed to reset the sensor.")
```
### Retrieving the Serial Number

You can obtain the serial number of the sensor using the serial_number property:

```python
serial_number = sensor.serial_number
print(f"Serial Number: {serial_number}")
```

### Printing a class instance

When printing a class instance you get a summarized output of the serial number the current temperature and the current humididy:

```python
sensor = SHT4x()
sensor.update()
print(sensor)
```

```output
serial number: beefbeef | temperature: 20.0°C | humidity: 45.0% RH
```
Please refer to the inline code comments and the class definition for detailed information about each method and property.

## License

This library is released under the MIT License. See the LICENSE file for more details.

## Contributing

Contributions to the SHT4x class are welcome! If you find any issues or have suggestions for improvements, please feel free to open an issue or submit a pull request.

## Author
Original code by Thorsten Schnebeck, ported by Jan Równicki
