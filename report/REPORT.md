# Chlorine Sampler
### Comp 4480 Directed Studies Final Report

**Student**: Chad Fawcett  
**Supervisors**: Kevin O'neil, Sharon Brewer  
Fall 2015

![Arduino and Colour Sensor](https://raw.githubusercontent.com/chadfawcett/chlorine-sampler/report/report/data/light_2013_05_18_IMG_1791-1024.jpg)  
Photo by [Adafruit](https://learn.adafruit.com/adafruit-color-sensors/assembly-and-wiring)

## Table of Contents
* [Summary](#summary)
* [Problem Statement](#problem-statement)
* [Existing Solutions](#existing-solutions)
  * [eXact iDip](#exact-idip)
  * [WaterLink Spin](#waterlink-spin)
* [Solution Overview](#solution-overview)
* [Hardware Technology](#hardware-technology)
  * [Colour Sensor](#colour-sensor)
    * [Adafruit RGB Color Sensor](#adafruit-rgb)
    * [SparkFun RGB Light Sensor](#sparkfun-rgb)
    * [COLSEN01 Colour Sensor Module](#colsen01)
  * [Micro-controller](#micro-controller)
    * [Arduino Uno](#arduino-uno)
* [Software Technology](#software-technology)
  * [Adafruit Colour Sensor Driver](#adafruit-driver)
* [Challenges Faced](#challenges-faced)
  * [Arduino](#arduino-problem)
* [Conclusion](#conclusion)

## <a name="summary"></a>Summary
Effectively testing drinking water for chlorine levels can be a tough task. Automated systems are often very expensive and most small treatment centres can’t afford the equipment. The cheaper alternative is to test manually, either using testing strips or a liquid reagent. Both of these less expensive methods rely on the operator to compare the colour of the sample to a chart of known values with is prone to error. Whether it be an expensive automated system, or manual tests, there appears to be lots of room for improvement.

## <a name="problem-statement"></a>Problem Statement
Testing water for chlorine levels is an essential part of ensuring safe, clean drinking water. If you live in a city, you most likely never even have to think about your water. A resident can simply turn on their tap and have safe drinking water instantly. Cities will have expensive automated systems constantly monitoring and treating the water. In the smaller surrounding communities, this is rarely the case. Water will be treated locally, often for just a handful of homes. These are the communities that can not afford costly automated system and resort to manual testing.

Manual testing can present lots of difficulties. From room lighting to partial colour blindness, there is a lot that can interfere with properly reading a sample.

Colour blindness happens to be a fairly common occurance among people. It's esitimated that approximately 8.0% of men and 0.4% of women are affected by some type of colour blindness. Nearly 95% of those affected have a common abnormal perception of red and green colours [(Color Blindness Prevelance)](http://www.news-medical.net/health/Color-Blindness-Prevalence.aspx). This is important to know as a lot of water testing mistures turn a red or green tint for the different amounts of chlorine/pH in the water.

Manual data entry also gives room for error. Having an operator manually record the reading means they need to double check that everything is entered correctly. Even with a causious data enterer, typos can still happen which could cause a lot of problem. Either a false positive, causing alert for people drinking the water. Or even worse, a false negative, which would mean the people drinking the water may never know that it's not clean.

## <a name="existing-solutions"></a>Existing Solutions
### <a name="exact-idip"></a>eXact iDip
![exact idip](https://raw.githubusercontent.com/chadfawcett/chlorine-sampler/report/report/data/eXactiDip393X400.jpg)  
Photo by [Sansafe](http://www.sensafe.com/idip/)

The [eXact iDip](http://www.sensafe.com/idip/) sensor, connected to phones wirelessly via bluetooth, but offers little features once the reading is on the phone. The app stores the reading locally with a geo-reference tagged to the sample test results. The only exporting of data is done through email. It appears that the main reason why the mobile phone connection was made was so that additional test functionality for the device could be sold after the fact as in-app purchases.

### <a name="waterlink-spin"></a>WaterLink Spin
![waterlink spin](https://raw.githubusercontent.com/chadfawcett/chlorine-sampler/report/report/data/wl_spin_mobile.jpg)  
Photo by [LaMotte](http://www.lamotte.com/en/pool-spa/digital-testing/3577.html)

The [WaterLink Spin](http://www.lamotte.com/en/pool-spa/digital-testing/3577.html) is a very interesting looking tester. It is targeted for the pool and spa industry but it does use the same photo sensing technique as the eXact iDip so it could be accurate enough for water system testing. The interesting thing about this tester is that it includes disks with several testing reagents in separate sections of the disk. The disk is then spun distributing the water sample into the separate section of the disk. Then the colour of each section is then read in order to determine the test results. The way this system was implemented removes a lot of room for error by not requiring the user to mix in the reagents.

## <a name="solution-overview"></a>Solution Overview
The solutions consists of both hardware and software. The hardware, consists of a micro-controller and a colour sensor. The software helps these devices communicate between each other as well as between the micro-controller and attached computer.

![Sampling](https://raw.githubusercontent.com/chadfawcett/chlorine-sampler/report/report/data/IMG_0182.JPG)

The hardware is capable of very accurately reading the colour of a chlorine sample. With this colour reading, the software can then compare the current sample to known values that correspond to chlorine levels. This allows for the operator to not have to make a manual comparison of the colour to known values reducing the risks of a false reading.

## <a name="hardware-technology"></a>Hardware Technology
### <a name="colour-sensor"></a>Colour Sensor
#### <a name="adafruit-rgb"></a>[Adafruit RGB Color Sensor with IR Filter and White Led](https://www.adafruit.com/products/1334)
![adafruit colour sensor](https://raw.githubusercontent.com/chadfawcett/chlorine-sampler/report/report/data/AdafruitColourSensor.jpeg)  
Photo by [Adafruit](https://www.adafruit.com/products/1334)

The Addafruit colour sensor is the one I decided to use for the project. The reason for this is simply because it is an all-in-one package. It includes a logic level shifting circuit so the module can be communicated with using either 3.3 volts or 5 volts. Having the logic level shifting built into the module simplifies the prototyping circuit as we don't have to implement it ourselves.

#### <a name="sparkfun-rgb"></a>[SparkFun RGB Light Sensor](https://www.sparkfun.com/products/12829)
![sparkfun RGB light sensor](https://raw.githubusercontent.com/chadfawcett/chlorine-sampler/report/report/data/12829-01.jpg)  
Photo by [SparkFun](https://www.sparkfun.com/products/12829)

The SparkFun RGB Light Sensor is another sensor that work for our needs, however it does not include the logic level shifting built in. For this reason, the Adafruit module was a better choice for what we needed. It also has an infrared filter over the colour sensor that improves accuracy.

#### <a name="colsen01"></a>[COLSEN01 Colour Sensor Module](http://www.elecfreaks.com/store/color-sensor-module-colsen01-p-285.html?zenid=8095153d156bd520dc8d83f4e4b3af49)
![colsen module](https://raw.githubusercontent.com/chadfawcett/chlorine-sampler/report/report/data/BK_COLSEN01_1.jpg)  
Photo by [elecfreaks](http://www.elecfreaks.com/store/color-sensor-module-colsen01-p-285.html?zenid=8095153d156bd520dc8d83f4e4b3af49)

The COLSEN01 Colour Sensor Module is similar to the Adafruit module but it lacks the infrared filter and has a higher price point. The infrared filter on the Adafruit module blocks out the infrared light coming into the sensor which helps produce a more accurate reading. The fact that this modules does not have the filter, made it clear that is was not the right module for the job.

### <a name="micro-controller"></a>Micro-controller
#### <a name="arduino-uno"></a>[Arduino Uno](https://www.arduino.cc/en/Main/ArduinoBoardUno)
![Arduino Uno](https://github.com/chadfawcett/chlorine-sampler/blob/report/report/data/36b21d3462e60577766300900621886a.image.538x354.jpg)  
Photo by [Arduino](https://store.arduino.cc/product/GBX00066)

Based on the colour sensor choice, the Arduino was the best choice for a Micro-controller. There are several choices that could have worked, but the Arduino is a very popular choice with lots of documentation and a large community behind them. In addition to the Adafruit colour sensor including an Arduino library for interfacing with it, I also personally have experience with the Arduino making it a lot more familiar and easier to understand and use new libraries.

## <a name="software-technology"></a>Software Technology
### <a name="adafruit-driver"></a>Adafruit Colour Sensor Driver
The [Adafruit TCS34725 Colour Sensor Driver](https://github.com/adafruit/Adafruit_TCS34725) is an Arduino libarary developed by Adafruit to easilly communicate with the colour sensor using an Arduino. The sensor communicates over the I2C protocol. This library makes the reading from the sensor much easier as the use does not have to worry about the complications of communicating with the sensor.

## <a name="challenges-faced"></a>Challenges Faced
### <a name="arduino-problem"></a>Arduino
Part of the scope of this project was to see if a smart phone could be used to communicate with the Arduino in order to get the colour reading. This would allow for operators in the field to be able to take readings on the fly. Using the Android USB On-the-Go (OTG) capabilities of some models, it would be possible to communicate with the Arduino.

The problem I faced was that the Arduino chosen for the project was a newer model than what my experience was based on. The newer model was using a different protocol than the older models for communicatin over USB. Since just the newest model of Arduino Uno used this protocol, all the information available online for communicating with Android was based on the older protocol. Knowing now that a different protocol is in place, with a little bit more time spent, the Android App component of the project could be implemented.

## <a name="conclusion"></a>Conclusion
With the time spent researching these details, we can see that it is in fact possible to make a cost effective automatic chlorine sampler. Reducing the amount of steps an operator takes can help prevent mistakes and false readings. By having the reading in an electronic format right from the source, it also prevents false reporting and delayed reporting.
