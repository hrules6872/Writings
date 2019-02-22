# Internet of Things — from zero to DIY Bitcoin Ticker
## tl;dr [source code](https://github.com/hrules6872/DIY-Bitcoin-Ticker) & [gallery](https://imgur.com/gallery/Yuvjj67)

I’m sure almost everyone has heard at least once about **[Arduino](https://www.arduino.cc/)** and/or **[Raspberry Pi](https://www.raspberrypi.org/)** *low cost computers*. Both are used in countless ingenious **DIY** [electronic](https://create.arduino.cc/projecthub) [projects](https://www.raspberrypi.org/forums/viewforum.php?f=15&sid=95585e4b93a16bf8879382a5025493a4), on their own or by using one of the many expansion modules available, due to their low price and small credit-card size form factor (even smaller if we refer to [Raspberry Pi Zero](https://www.arrow.com/en/research-and-events/articles/raspberry-pi-3-vs-raspberry-pi-zero-w) model).

But they aren’t the only ones (in fact there are many): among the most popular is **[NodeMCU](http://www.nodemcu.com/index_en.html)** *aka The Arduino Killer*🏆 (based on **[ESP8266](https://www.espressif.com/en/products/hardware/esp8266ex/overview)** wifi-[soc](https://en.wikipedia.org/wiki/System_on_a_chip))

### What are their differences?

They are [totally different concepts](https://cybergibbons.com/uncategorized/arduino-misconceptions-4-the-arduino-is-obsolete-now-the-raspberry-pi-exists/) because they were conceived to perform different tasks: while **Arduino** is actually an [almost indestructible](https://www.rugged-circuits.com/10-ways-to-destroy-an-arduino/) open source¹ **microcontroller** which we can start playing with using a simple script (in C/C++; one application at a time) from the minute one, **Raspberry Pi** is a *full* **minicomputer**² on one small board ([SBC](https://en.wikipedia.org/wiki/Single-board_computer)) that runs a dedicated [Linux OS distribution](https://www.raspberrypi.org/downloads/) (so it can be programmed using a wide variety of languages) which allows us to run different programs very much like we do on our desktop computers.
>  “If your application is more about controlling things, the Arduino is probably a better choice. While if you need to process lots of data the PI is your best bet”
>  — [Arduino vs Raspberry Pi — Which is best?](https://www.youtube.com/watch?v=7vhvnaWUZjE)

That said, more like a microcontroller than a minicomputer, we have our hero **[NodeMCU](https://github.com/nodemcu/nodemcu-devkit): an Arduino-compatible [dev](https://github.com/esp8266/Arduino) board with built-in WIFI for [less than $5](https://www.aliexpress.com/item/ESP8266-CH340G-NodeMcu-Lua-V3-ESP8266-CP2102-NodeMcu-Lua-V2-Wireless-Module-ESP8266-ESP-12E-Micro/32909262615.html)** that also supports [Lua](https://www.lua.org/) scripting language (there are several variants of **ESP8266** chipset out there but it’s highly recommended to buy from the [second-generation](https://frightanic.com/iot/comparison-of-esp8266-nodemcu-development-boards/) **ESP-12E** variant because it has a [built-in power regulator](https://tttapa.github.io/ESP8266/Chap02%20-%20Hardware.html)).

## NodeMCU on Arduino IDE

The **Arduino platform** has its own **[IDE](https://www.arduino.cc/en/Main/Software)** (more of an editor than an [IDE](https://imgflip.com/i/2nzd3m) actually) available for free and it is quite easy to make it compatible with NodeMCU:

 1. Install standalone Arduino IDE following [these instructions](https://www.arduino.cc/en/Guide/HomePage) depending on your machine’s OS

 2. Launch Arduino IDE

* Open *Preferences*

* Add the link [http://arduino.esp8266.com/stable/package_esp8266com_index.json](http://arduino.esp8266.com/stable/package_esp8266com_index.json) to *Additional Boards Manager URLs*

* Open *Boards Manager…* (menu *Tools* > *Board…*)

* Search for *ESP8266* and install it

* Open menu *Tools* > *Board*… and select *NodeMCU [x.x…](https://frightanic.com/iot/comparison-of-esp8266-nodemcu-development-boards/)*

Done!

### Hello world!

Now that our development environment is ready, let’s verify that everything works well using one of the most easiest [examples included](https://www.arduino.cc/en/Tutorial/BuiltInExamples): **[LED Blinking](https://www.arduino.cc/en/Tutorial/BlinkWithoutDelay)**.
>  We will use stock “[Arduino language](https://www.arduino.cc/en/Main/FAQ#toc13)” (limiting the project to a single file with .ino extension known as “sketch”) along this journey which is basically [a set of C/C++ functions](https://www.arduino.cc/reference/en/) (IMO they have done an excellent job in general abstracting the different interfaces because even a beginner would able to read and understand easily almost all the code). Advanced use cases perhaps will need a *real* IDE³ plus the use of plain C/C++ language.

 1. Launch Arduino IDE

 2. Connect the board to the computer (it’s quite common to tape the back to ensure that no metal scrap can short-circuit the board)

 3. Select the correct `COM` port for your serial adapter (*Tools* > *Port…*)⁴

 4. Load *Blink* sketch (*File* > *Examples* > *ESP8266* > *Blink*). Nothing to explain here as we can see the code is very easy to understand⁵.

 5. Add the following line to the very beginning of the example (because the example is written for an older module version and not for ESP-12): `#define LED_BUILTIN 2`

 6. Upload it and wait a few seconds (the led should blink quickly during the uploading)

Welcome to life!

### Serial monitor

In order to make a real “Hello, World!” example we will modify the previous Blink example to print that well-known message.

 1. Add `Serial.begin(9600); Serial.print(“Hello, World”);` lines within `setup()` method

 2. Upload it

 3. Open *Serial Monitor* (*Tools* > *Serial Monitor*)

 4. Select *9600 baud* option in the drop-down list

 5. Push the *reset* button on the board

[Logging](https://www.youtube.com/watch?v=iNkrF43SZEU)!

## Who is out there?

As we have seen before, our tiny and dirt cheap **NodeMCU has a built-in WIFI chipset**. Therefore, the second thing we will do is display in the *Serial Monitor* all the wireless networks available around us using again one of the included examples: *WifiScan* (*Files* > *Examples* > *ESP8266WiFi* > *WiFiScan*).
>  Be sure to set the same baud rate in the code (`Serial.begin(xxx);`) as in the Serial Monitor drop-down list.

### Home is where the WIFI connects

This time there is no example included showing us how to make the connection to our lovely Internet, so we will create a new script (*File* > *New*) containing the code below (as we can see the code is almost self-explanatory and doesn’t need any additional comment 🤞):

{% gist https://gist.github.com/hrules6872/1aef38f33b416e7692a2fc3c58009aec#file-arduino-wifi-connect-ino %}
>  Check twice the ssid and/or password values before start to think the board is broken 😉

### Do you even fetch, bro?

Now, it is time to start coding our project 👏, a **Physical [Bitcoin](https://bitcoin.org/en/) Ticker**, fetching some data from a well-known [free API](https://pro.coinmarketcap.com/)⁶ (**[CoinMarketCap](https://coinmarketcap.com/)**).

 1. Go to *Tools* > *Manage Libraries*, and search for **[ArduinoJson](https://arduinojson.org/)** ([6 or above](https://arduinojson.org/v6/doc/upgrade/) version)

 2. Create a new *sketch* and paste the code below

 3. Fill in `ssid`, `password` and `api_key` variables ([get your API key here](https://pro.coinmarketcap.com/)⁶)

 4. Upload!
>  There is a [wrapper around CoinMarketCap API](https://github.com/witnessmenow/arduino-coinmarketcap-api) available for NodeMCU but it seems pretty abandoned and old so we will use our own implementation.

 {% gist https://gist.github.com/hrules6872/b06097fe38e7d1e0ef1af3d3bdc37a38#file-arduino-api-request-ino %}

## Rise & shine

At this point we all agree on this: it makes no sense to use an **[IoT](https://en.wikipedia.org/wiki/Internet_of_things)** device of any kind to dump the information to the *Serial Monitor*. So, **we should use a display to make our BitCoin Ticker really useful**.

Although there are a vast offer of [I2C](https://en.wikipedia.org/wiki/I%C2%B2C)/[SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface) displays models (ie SSD1306 or SH1106 models) to buy (these kind of add-on boards are also known as “*shields*”) we don’t want to mess around with cables, [GPIOs](https://en.wikipedia.org/wiki/General-purpose_input/output), [breadboards](https://en.wikipedia.org/wiki/Breadboard), voltages and [that sort of thing](https://www.arduino.cc/glossary/en/) by the moment so, **for just less than $7,** we can buy an [ESP8266+OLED](https://www.aliexpress.com/item/NODEMCU-Wifi-ESP8266-ESP-12F-For-Wemos-For-Arduino-ESP12F-0-96-0-96-Inch-OLED/32890892129.html) built-in on [PCB](https://en.wikipedia.org/wiki/Printed_circuit_board).

Using the easiest (also the cheapest) option described above we must install the [U8g2lib](https://github.com/olikraus/u8g2) library (even if we follow another path that library support [almost all types of displays](https://github.com/olikraus/u8g2/wiki/u8g2setupc#setup-function-reference) so I can stop recommending it), paste the code below and upload it.
>  We have to setup the display driver at the beginning using one of the default constructors the library give us. Printed on its back side we can find where SDA and SCL are [connect to](https://raw.githubusercontent.com/nodemcu/nodemcu-devkit/master/Documents/NODEMCU-DEVKIT-INSTRUCTION-EN.png). For example SDA-D1 and SCL-D2 means that the first one is connected to GPIO5 (D1) and the second to GPIO04 (D2). So later we use these values as data (5 in this case) and clock (4).<br>
>  Example working for the ESP8266+OLED said above: `U8G2_SSD1306_128X64_NONAME_1_HW_I2C u8g2(*/* rotation=*/ *U8G2_R0, /* reset=*/ U8X8_PIN_NONE, /* clock=*/ 4, /* data=*/ 5);`<br>
>  For more details on those parameters refer to [this](https://github.com/olikraus/u8g2/wiki/u8g2reference#carduino-example) example.

 {% gist https://gist.github.com/hrules6872/dc58455164266730bded9bf30614b315#file-arduino-display-ino %}

## Where do we go from here?
>  “To infinity and beyond!” — [Buzz Lightyear](https://en.wikipedia.org/wiki/Buzz_Lightyear)

As we have already seen in a couple of hours and a few lines of code we can have our own **[Bitcoin Ticker](https://github.com/hrules6872/DIY-Bitcoin-Ticker)** running. So based on this and reading in depth all the shared links we will able [to improve it](https://imgur.com/gallery/Yuvjj67) or [start a new project](https://www.esp8266.com/viewforum.php?f=11) totally different. **No limits! 🚀**

### Thanks for reading. If you enjoyed this article, feel free to hit that clap button 👏 as much as you can to help others find it.

*****

[1] We can buy an official **Arduino** in [their online store](https://store.arduino.cc/) [for about $25](https://store.arduino.cc/arduino-uno-rev3) **without WIFI module** (supporting the company to continue researching and improving their products) but as it is an open source product there are some manufacturers who have created perfect clones that we can buy for [less than $3](https://www.aliexpress.com/item/One-set-high-quality-WEIYU-UNO-R3-CH340G-MEGA328P-Chip-16Mhz-UNO-R3/32865259855.html) ([Ebay](https://www.ebay.com/sch/i.html?_nkw=arduino) is also a great place to buy them). <br>
[2] One of the “biggest cons” of **Raspberry Pi** is that its hardware is not open source (Broadcom has an agreement with the Foundation to sell its chipset on exclusivity) so we cannot buy any cheaper Chinese clone anywhere.<br>
[3] There are more powerful [alternatives](https://www.survivingwithandroid.com/2018/08/10-arduino-ide-alternative-to-start-programming.html) (personally I always stay as far as I can from that [Eclipse](https://giphy.com/gifs/vh1-AENSKmYsLY5S2F4QQK) thing) to the official “IDE” such as **[PlatformIO](https://platformio.org/)** (which looks promising but perhaps quite complicated IMO) or this other **[Visual Studio Code extension for Arduino](https://github.com/Microsoft/vscode-arduino)** (which is backed by Microsoft)<br>
[4] On **macOS** you will probably have to install [one](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers) of these [drivers](https://github.com/nodemcu/nodemcu-devkit/wiki/Getting-Started-on-OSX) (Bluetooth is not a valid port to uploading our sketches 😆) <br>
[5] Anyway [here](https://arduino-esp8266.readthedocs.io/en/2.4.2/) is your new Bible.<br>
[6] They will be migrating their [Public API](https://coinmarketcap.com/api/) to a “**[Professional API](https://pro.coinmarketcap.com/)**” on Dec 4th, 2018. For our intentions their **[FREE](https://pro.coinmarketcap.com/pricing)** [tier](https://pro.coinmarketcap.com/signup?plan=0) meets our needs 😉

*****

[External links 👀](https://gist.github.com/hrules6872/e659c389bafcf8663e5c084d67b3cfeb)