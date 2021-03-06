# Thermal-Kotlin
Kotlin Driver for A2 Micro Panel Thermal Printer. Provides an easy to use API to print text and images to the 2.25" printer model. ([Get one here](https://www.adafruit.com/product/597))

![Adafruit Thermal Printer Example](https://i.imgur.com/wsbG4BV.gif)

### Features

- [x] Print text strings
- [x] Underline text
- [x] Bold Text
- [x] Inverse Text
- [x] Automatic Line Breaks for Text
- [x] Print 1-bit images
- [x] Resize and dither colored images (using [Floyd-Steinberg dithering](https://en.wikipedia.org/wiki/Floyd%E2%80%93Steinberg_dithering))
- [x] Throttled data transfer to allow for large images
- [ ] Rich text string DSL
- [ ] Print barcodes

### Usage with Gradle

Step 1: Add the JitPack repository to your build file:

```groovy
allprojects {
	repositories {
		//...
		maven { url 'https://jitpack.io' }
	}
}
```

Step 2: Add the dependency:

```groovy
dependencies {
	implementation 'com.github.SebastianAigner:Thermal-Kotlin:master-SNAPSHOT'
}
```

This library is still very new, and has not reached a stable state yet. Expect changes in the API from snapshot to snapshot. To bind yourself to a specific commit, check out the _Commits_ tab on [JitPack](https://jitpack.io/#SebastianAigner/Thermal-Kotlin/).

### Quick Start

1. **Set up** the printer using `val printer = ThermalPrinter("/dev/serial0", 19200)`, adjusting communication port and Baud rate if necessary.
2. **Connect** to the printer using `printer.connect()`.
3. **Write text** using `printer.writeLine()` for a _single line_ and `printer.writeText` if you need _automatic line-breaking_.
4. **Adjust text** by changing the `doubleWidth`, `justification`, `inverted`, `bold` properties. Don't forget to change them back when you're done!
5. **Print images** calling `writeImage()` with a `BufferedImage` of your choice. It is automatically scaled and dithered.
6. **Close the connection** using `printer.disconnect()`.

### How to determine Baud rate

Disconnect the Thermal Printer from the power supply. Press and hold the paper feed button, and plug in the power. The printer will output a Character Code Table as well as its Baudrate and other useful information that might be interesting for debugging.

### Further Reading

- Get a printer for yourself: https://www.adafruit.com/product/597
  - Soldering the printer: https://learn.adafruit.com/pi-thermal-printer/soldering-pre-2017
  - General information on pin setup: https://learn.adafruit.com/mini-thermal-receipt-printer/circuitpython - **Long story short: Ground goes to Ground pin on Raspberry Pi, Yellow goes to Pin 14**.
- Data sheet: https://cdn-shop.adafruit.com/datasheets/cashino+thermal+printer+a2.pdf
- In-depth manual (with control codes for serial access) https://cdn-shop.adafruit.com/datasheets/A2-user+manual.pdf