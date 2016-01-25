# Chlorine Sampler
### Comp 4480 Directed Studies Final Report

**Student**: Chad Fawcett  
**Supervisors**: Kevin O'neil, Sharon Brewer  
Fall 2015

## Table of Contents

* [Summary](#summary)
* [Problem Statement](#problem-statement)
* [Existing Solutions](#existing-solutions)
  * [eXact iDip](#exact-idip)
  * [WaterLink Spin](#waterlink-spin)
* [Solution Overview](#solution-overview)
* [Hardware Technology](#hardware-technology)
* [Software Technology](#software-technology)
* [Challenges Faced](#challenges-faced)
* [Further Research](#further-research)
* [Conclusion](#conclusion)

## <a name="summary"></a>Summary
Effectively testing drinking water for chlorine levels can be a tough task. Automated systems are often very expensive and most small treatment centres can’t afford the equipment. The cheaper alternative is to test manually, either using testing strips or a liquid reagent. Both of these less expensive methods rely on the operator to compare the colour of the sample to a chart of known values with is prone to error. Whether it be an expensive automated system, or manual tests, there appears to be lots of room for improvement.

## <a name="problem-statement"></a>Problem Statement
Testing water for chlorine levels is an essential part of ensuring safe, clean drinking water. If you live in a city, you most likely never even have to think about your water. A resident can simply turn on their tap and have safe drinking water instantly. Cities will have expensive automated systems constantly monitoring and treating the water. In the smaller surrounding communities, this is rarely the case. Water will be treated locally, often for just a handful of homes. These are the communities that can not afford costly automated system and resort to manual testing.

Manual testing can present lots of difficulties. From room lighting to partial colour blindness, there is a lot that can interfere with properly reading a sample.

Colour blindness happens to be a fairly common occurance among people. It's esitimated that approximately 8.0% of men and 0.4% of women are affected by some type of colour blindness. Nearly 95% of those affected have a common abnormal perception of red and green colours. [Color Blindness Prevelance](http://www.news-medical.net/health/Color-Blindness-Prevalence.aspx) This is important to know as a lot of water testing mistures turn a red or green tint for the different amounts of chlorine/pH in the water.

## <a name="existing-solutions"></a>Existing Solutions
### <a name="exact-idip"></a>eXact iDip
The [eXact iDip](http://www.sensafe.com/idip/) sensor, connected to phones wirelessly via bluetooth, but offers little features once the reading is on the phone. The app stores the reading locally with a geo-reference tagged to the sample test results. The only exporting of data is done through email. It appears that the main reason why the mobile phone connection was made was so that additional test functionality for the device could be sold after the fact as in-app purchases.

### <a name="waterlink-spin"></a>WaterLink Spin
The [WaterLink Spin](http://www.lamotte.com/en/pool-spa/digital-testing/3577.html) is a very interesting looking tester. It is targeted for the pool and spa industry but it does use the same photo sensing technique as the eXact iDip so it could be accurate enough for water system testing. The interesting thing about this tester is that it includes disks with several testing reagents in separate sections of the disk. The disk is then spun distributing the water sample into the separate section of the disk. Then the colour of each section is then read in order to determine the test results. The way this system was implemented removes a lot of room for error by not requiring the user to mix in the reagents.

## <a name="hardware-technology"></a>Hardware Technology
### Colour Sensor
#### [Adafruit RGB Color Sensor with IR Filter and White Led](https://www.adafruit.com/products/1334)
The Addafruit colour sensor is the one I decided to use for the project. The reason for this is simply because it is an all-in-one package. It includes a logic level shifting circuit so the module can be communicated with using either 3.3 volts or 5 volts. Having the logic level shifting built into the module simplifies the prototyping circuit as we don't have to implement it ourselves.

#### 

## <a name="software-technology"></a>Software Technology

## <a name="challenges-faced"></a>Challenges Faced

## <a name="further-research"></a>Further Research

## <a name="conclusion"></a>Conclusion
