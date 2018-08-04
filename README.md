[ ![Download](https://api.bintray.com/packages/knobtviker/maven/fram/images/download.svg) ](https://bintray.com/knobtviker/maven/fram/_latestVersion)

Fujitsu MB85RC256V driver for Android Things
======================================

This driver supports [Fujitsu MB85RC256V](http://www.fujitsu.com/uk/Images/MB85RC256V-20171207.pdf) I2C FRAM.

It's based on [Arduino library for I2C FRAM](https://github.com/sosandroid/FRAM_MB85RC_I2C) and will eventually support all devices listed there.
  
Ferroelectric RAM (FeRAM, F-RAM or FRAM) is a random-access memory similar in construction to DRAM but using a ferroelectric layer instead of a dielectric layer to achieve non-volatility.

How to use the driver
---------------------

### Gradle dependency

To use the `fram` driver, simply add the line below to your project's `build.gradle`,
where `<version>` matches the last version of the driver available on [jcenter](https://bintray.com/knobtviker/maven/fram) .

```
dependencies {
    implementation 'com.knobtviker.android.things.contrib.community.driver:fram:<version>'
}
```

### Sample usage

```java
import com.knobtviker.android.things.contrib.community.driver.fram.Mb85rc256v;

// Access the FRAM device:

Mb85rc256v fram;

try {
    //default constructor with default write protection pin and status
    fram = new Mb85rc256v(i2cBusName);
} catch (IOException e) {
    // couldn't configure the device...
}

// Reads one byte from the specified FRAM address
try {
    final byte valueToRead = fram.readByte(0);
} catch (IOException e) {
    // error reading value from address
}

// Write one byte from the specified FRAM address
try {
    final byte valueToWrite = 111;
    fram.writeByte(0, valueToWrite);
} catch (IOException e) {
    // error writing value to address
}

// Close the FRAM device when finished:

try {
    fram.close();
} catch (IOException e) {
    // error closing device
}
```