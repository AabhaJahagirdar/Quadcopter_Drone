
Content:
YMFC-AL_setup.ino
YMFC-AL_esc_calibrate.ino
YMFC-AL_Flight_controller.ino
YMFC_scematic.pdf

Revision update:
=====================================================================================================================================================

The calibration sketch stops working when a character or number is send. When sending a character via the serial monitor of some Arduino IDE’s 
a line feed is also send. Because the ESC calibration program only expects one character the program stops working.

In the code the line:
data = Serial.read();                                                               //Read the incomming byte.

Is changed into:
data = Serial.read();                                                               //Read the incomming byte.
delay(100);                                                                         //Wait for any other bytes to come in
while(Serial.available() > 0)loop_counter = Serial.read();                          //Empty the Serial buffer.
=====================================================================================================================================================

Steps to uplode the code into your Arduino Board :

1. The very first step is to clear the EEPROM of the Arduino board.
2. Uplode this code into arduino for clearing the EEPROM :
   #include <EEPROM.h>
   void setup() {
     // Optional: Initialize the LED pin as an output for visual feedback
     // pinMode(13, OUTPUT); 
     // Iterate through each byte of the EEPROM storage
     // EEPROM.length() returns the size of the EEPROM for the specific board
     for (int i = 0 ; i < EEPROM.length() ; i++) {
       EEPROM.write(i, 0); // Write 0 to each address
     }
     // Optional: Turn the LED on to indicate completion
     // digitalWrite(13, HIGH); 
   }
   void loop() {
     // Empty loop as no continuous operation is needed after clearing EEPROM
   }
3. Goto the esc_calibrate folder and uplode the arduino code.
4. Download the required libraries.
5. Compile the code and uplode it.
6. Make sure you keep your drone on a flat surface before the process starts.
7. Open the monitor screen and let it pair with your remote control. In my case I have used the FS-i6.
8. Follow the instrctions by moving the throttle as per the instructions on the screen.
9. Once its done it's time for the MPU 6050 calibration.
10. Again read the instructons on the monitor and title the drone accordingly.
11. Open the setup folder and compile the code.
12. Uplode the code and meanwhile open the monitor screen and type r and a and observe the output and if the coordinates on the monitor chnage your MPU is calibrated successfully.
13. Now remove the arduino uplode cable and try pairing it with your fs-i6. Confirming it by 3 beeps from each motor.
14. After these steps again plug in the arduino cable and uplode the code from the flight controller folder.
15. Run your drone after completion.