# BAE-305-Lab-6
# Lab 6: Sensing and Mobility

Group Members: Heath Shewmaker and Terence Redford

Submitted: 3/12/25

# Introduction: 
The purpose of this lab was to get acquainted with the ultrasonic sensor through more hands-on experience with coding. This sensor uses sound waves to sense its distance away from objects. It can be used for a variety of reasons but was used as a cautionary measure in this instance. We used this sensor to cut the power to a pair of electric motors once they reached a certain distance from our boundary. We also measured the accuracy and resolution of this sensor to get a feel for its capabilities.
# Methods:
Step 1: We first created the circuit shown below in figure 1, utilizing the HC-SR04 ultrasonic sensor. 
 
 ![image](https://github.com/user-attachments/assets/9adae911-dbac-4990-8b28-233540abdf0e)

Figure 1: Connection of the ultrasonic sensor to the Redboard

Step 2: Using the link found in the lab manual, we coded a program to continually output the distance being read by the sensor. You can copy and paste the given code, seen below in figure 2.
 
 ![image](https://github.com/user-attachments/assets/5153dd79-124a-447c-9a9d-579946e7fedd)

Figure 2: Given code for ultrasonic sensor distance display

Code Explanation: The above code initializes the two pins , “trigPin” and “echo pin” to digital pins 9 and 10 on the arduino respectively, in the setup function. Then in the loop function which runs constantly, the following flow of events is set to occur in sequence; the trigPin (which controls the ultrasonic emitter) is set to low, in case it is not already off. It then delays 2 microseconds, after which it is supplied with the “High” voltage of the arduino, which causes it to begin emitting an ultrasonic signal. After 10 microseconds the pin is then set to the “Low” value again to cease the emission of ultrasonic sound. This set of actions results in a distinctive ultrasonic signal that can be detected by the other side of the sensor when it returns. To detect this signal the “pulseIn()” function is programmed to wait for either a high or low signal on a certain pin. In this case it was set to wait for a “High” reading on the echoPin. This would mean that when the receiver on the ultrasonic sensor detects the distinctive signal we sent, it will return a high voltage, and the pluseIn() function will tell us how long this took. Then the total distance travelled can be calculated using a constant multiplier (which has been mathematically derived by the original programmers) and then divided by two to get the distance to the object that the signal encountered. This was set to repeat on a delayed interval using the “delay()” at the end of the loop, which prevented interference from occurring.

Step 3: After uploading our code to the Redboard, we were able to see the distance outputs being displayed in the serial monitor on Arduino IDE. We used the provided ruler to confirm our sensor was displaying accurate readings. 

*** Make sure to take measurements from the tips of the sensor, rather than the backboard***

Step 4: Next, we determined the resolution of our sensor by testing for the smallest increment of change in distance that it could detect. We moved the sensor approximately one millimeter for three separate trials and documented the differences in the readings displayed. This data is displayed in the results section.

*** For this next step, do not completely dismantle your previous circuit, as you will need it for the last step***

Step 5: We then created a second circuit to utilize a motor driver and 2 electric motors. Through reading and listening to Dr. Jarro carefully, we observed that the sliding switch in the diagram below was not needed and would instead be replaced by our ultrasonic detector setup later. 
 
 ![image](https://github.com/user-attachments/assets/d639268f-091e-42c0-be47-0f517ac5b583)

Figure 3: Connection to motor controller and electric motors (https://learn.sparkfun.com/tutorials/sparkfun-inventors-kit-experiment-guide---v40/circuit-5b-remote-controlled-robot)  

Step 6: We then wrote a code to control the movement of both motors at 3 different speeds in 4 directions: forward, backward, left, and right. We used the code given in the provided link to get started but made modifications to tune it to our liking. The given code can be found in the ‘Open the Sketch’ section of the SparkFun write up linked under figure 3. 

*** Save your code from step 6, as you will need it for your report***

Step 7: We tested our program to make sure the motors would go in each direction at each different speed, as we needed to demonstrate this for the lab instructor in order to leave. We also tested, as requested by the discussion question, for minimum input speed for forward motion at this point.  

Step 8: Add your code from the ultrasonic sensor (step 2) in such a way that the motors will stop moving when the distance reads less than 10 centimeters. Simple copy and paste will not suffice, you will need to make some adjustments. These changes can be seen in the results section. 
# Results:
For the first circuit with the ultrasonic sensor we found that it was more accurate than we had initially expected. From a small sample of measurements we estimated that changing the distance to the obstacle by 1mm made the reading change by about 4mm. However, we observed that the fluctuations in the measurement were large compared to the precision of the reading, indicating to us that there was a large influence of error on these estimates. We believe that slight angle variations of how the ultrasonic waves made incident with the obstacle, random electromagnetic interference (potentially from the many other ultrasonic sensors in the same room) and human error in the precision of our distance adjustments could all have been significant factors in why the device appeared less precise. Despite this, when tested at various distances, the distances detected by the sensor were accurate within a range of +-3 mm. This leads us to believe that this ultrasonic sensor is quite accurate, but not completely precise. The data for these estimates is shown below:
 
 ![image](https://github.com/user-attachments/assets/9868eb01-cf56-4cbe-9e81-a1fc40769b2e)

Table 1: Actual distance vs. sensor reading

![image](https://github.com/user-attachments/assets/22addec5-f6b5-4500-9a16-4504dc981845)
 
Table 2: Difference in sensor readings for 1mm of movement

For the second circuit, we changed a considerable amount of the given code. The majority of the setup section, where locations and components are called out, was the same; the changes can be seen in figure 4. 
 
 ![image](https://github.com/user-attachments/assets/7eab25a9-6264-4679-bacf-d33ce4451ca6)

Figure 4: Setup for the code

The loop section, on the other hand, was heavily modified from the given code. The program written to run the left motor can be seen in Figure 5. This is similar to the codes controlling the right motor and both motors concurrently. We initially separated control of the motors by using two nested if statements to distinguish right and left motors by inputting ‘R’ or ‘L’ respectively, but  when this proved to be unnecessary we modified the code to rather take inputs of ‘L’, ‘R’, ’B’, ’F’ to represent left, right, back and forward respectively. 

 ![image](https://github.com/user-attachments/assets/ada9cf67-1cfc-4c0c-a13f-80a28796c78e)

Figure 5: Code for running left motor (similar for right)

For the last rendition of the second circuit, we added the ultrasonic sensor and used it as a “safeguard” for our machine. Because we already had the code to read the sensor, we just had to add a limit switch in the code to stop the motor when the reading was less than a certain distance. This can be seen below in Figure 6.
 
 ![image](https://github.com/user-attachments/assets/e751f1e8-7a7d-4efd-9df0-c8c7ca4cf8e9)

Figure 6: Code for limit switch using ultrasonic sensor

# Discussion: 
What was the minimum “speed” number in the code to make the motor move?

We determined that we could get the motor to spin very slowly when we used 35 as the motorSpeed() input. We occasionally had to start it by pushing it, although it could usually start on its own. This indicated to us that this was the minimum current the motor needed before the inertial weight of the motor armature was too great for the magnetic forces to overcome.
# Conclusion: 
The aim of this lab was to get practical experience using the arduino as an interface with other components. We also learned how to manipulate the code in Arduino IDE to allow us to use sensors, such as the ultrasonic distance sensor, to receive information and react to it using our other output devices. We felt there were 3 key takeaways from this lab.

For the first of these, we found that the table explaining each of the pins on the motor driver was not only very useful, but also that we were able to recognize patterns in the labeling of the pins. We noticed that these components are all specifically designed to be modular, so a quick glance at a table of pin explanations or even reading the printed labels on the components can give you a sufficient understanding of what the component needs and provides. 

We were also familiarized with what each of the pins on the arduino are designed for. From PWM enabled digital pins, to the analog input pins, and the various power pins for ground and supply voltage, this lab provided us with a strong understanding of what each of the pins is for. This was also enhanced by tinkering with the code, which taught us that the pins have input and output modes, which we directly controlled in Arduino IDE when combining the motors and the ultrasonic sensor.

Finally, we learned how testing for edge cases and limiting scenarios is important for ensuring that components function as expected. By testing the minimum speed for the motor to move and testing the precision and accuracy of the ultrasonic sensor, we realized that it is important to test your electrical components, since the theoretical functions are not always reflected in reality. By using these components, we were also able to see how they can be used in various applications and combinations to perform different tasks. 
