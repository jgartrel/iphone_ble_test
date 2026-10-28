# iPhone BLE connection test

The following test attempts to duplicate a reconnection issue with the iPhone 17e. It is designed to show the comparative reconnection deferences among the following models: iPhone 17e, iPhone 18 Pro Max, and an older model such as the iPhone 12 mini.  The test primarly focuses on connecting to an embedded device using BLE. Source code for the embedded device can be found here: https://github.com/jgartrel/iphone_ble_test


### Mac Setup Prerequisites

Mac setup is only necessary to rebuild the source code. Setup instructions can be found in [README.md](README.md).


### iPhone Setup
1.  Install the latest IOS version (27.0.1 as of this publication)
2.  Install the [BluefruitConnect](https://apps.apple.com/us/app/bluefruit-connect/id830125974) app from the Apple App Store
3.  Open the App and give it permission to use BLE


### Test Setup
1.  Purchase a [Seeed Studio XIAO nRF52840 Plus](https://www.seeedstudio.com/Seeed-Studio-XIAO-nRF52840-Plus-p-6359.html)
2.  Plug the nRF52840 Plus into your computer
3.  Double-click the reset button, a new USB Drive will appear
4.  Copy the `iphone_ble_test.ino.uf2` file to the newly mounted usb drive. Don't worry if you get a message that the device suprisingly disconnected.
5.  You should see a solid RED light on the  nRF52840 Plus for ten seconds, then the device should perpetually flash quckly every second.
6.  You should now see an "Embedded Test1" device appear in the list of BLE advertisements.


### Test Proceedure

You will need at least 2 iPhones for comparative analysis. As of this publication the following 3 phone models were used:
* iPhone 18 Pro Max
* iPhone 17e
* iPhone 12 mini

You will need to run the 'iPhone Setup' proceedure listed above for each iPhone used in the test. You will also need to run the 'Test Setup' proceedure on the nRF52840 Plus. This only needs to be done once.

Please Note: You may also need quite a bit of open space (50 feet) to run this test. The test can be run inside or outside, it does not matter. The iPhone can be held continuously or slid on the ground during the test proceedure. The latter provides more precise and consistent results.

Start the 'control' test, with the **iPhone 18 Pro Max**, using the following proceedure:
1.  Plug in the nRF52840 Plus a stable 5V USB-C power source.
2.  Confirm that after 10 seconds the red LED starts flashing once per second
3.  Using the iPhone 18 Pro Max, open the Bluefruit Connect App
4.  Connect to the "Embedded Test1" device and select 'UART'
5.  Confirm that you see a number each second that is roughly increasing by 1000
6.  Slowly back away from the device, stop when you notice that the 'Send' input box is greyed out and that the numbers have stopped. This signals that you have been disconnected.
7.  Take two large steps forward
8.  Observe the numbers start again and that the 'Send' input is no longer greyed out.
9.  Repeat steps 6-8 until you can consistently characterize how the iPhone is reconnecting
10. Disconnect from the device, close the BluefruitConnect app and turn off the iPhone.

Next, repeat the test with the **iPhone 17e**. Notice the difference in step 7:
*  Observe that you must take many large steps forward significantly closing the distance between you and the device before the iPhone 17e reconnects.

Finally, repeat the control proceedure with the **iPhone 12 mini**. Notice that the behavior is identical to that of the iPhone 18 Pro Max, requiring that the tester only take two steps forward to re-establish a connection.


### Conclusion

The expected behavior when losing connection to a BLE device is that the tester only needs to move slightly closer to be back in range and re-establish connection to the device. The iPhone 17e requires the user to bring the phone substantially closer to the device to regain a connection. This issue with the iPhone 17e is even more prevalent with embedded wearables where signal strength is limited. Our observations show that althogh the iPhone 17e is able to maintain a stable connection at 10 feet with a wearable, it must be brought within 2 feet of the device to reconnect. This creates an unexceptable experience for the end user.
