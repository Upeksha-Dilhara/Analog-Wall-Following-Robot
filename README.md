# Analog-Wall-Following-Robot
Creating a wall-following robot is a popular project among robotics enthusiasts worldwide. Nowadays, it's quite common for robots to have this capability due to the availability of microcontrollers like the ATMega328P and open-source hardware and software platforms such as Arduino. These tools have made it easier to implement and troubleshoot such projects.

However, our team, consisting of Mr. Shanaka Liyanarachchi, Mr. Ishara Dilshan, Mr. Upeksha Dilhara, and Mr. Namina Wijethunga, decided to take on a unique challenge for our analog electronics project in Semester 3 of the EN2091 module at the Department of Electronic and Telecommunication Engineering, University of Moratuwa. Our goal was to design the main circuitry of the robot using only analog electronic components like resistors, capacitors, and ICs, without relying on any microcontrollers.Our project was supervised by Mr. Pahan Mendis, Mr. Hiruna Vidumina, and Mr. Hasantha Nadeeshan.

## Project Description
_**Build a simple wall following robot with a PID controller which keeps the robot at the center as it travels. Use of analog distance measurement sensors. Use analog electronics for the implementation (transistors, operational amplifiers).Robot should be able to track the center-line between walls with minimum latency. Evaluated based on design, speed and performance of the robot. A design with 2 motors will be sufficient. You can use a robot kit with chassis (but you are encouraged to come up with a custom design).Wall height is 7 cm. The width between walls is 30 cm. Maximum robot size is 15 cm x 15 cm.**_

## Functinality Description
The robot should maintain a constant distance between the two walls when the robot moves forward. If the robot moves toward one wall, it should have the ability to bring back the middle of two walls. The robot should always measure the distance between two walls. For measuring we thought of two types of sensors to use. Those are:
- Ultrasonic sensors
- Sharp IR sensors

Finally we decided to use sharp ir sensors because everything we have to do in the analog domain. 

### Reasons why not to use ultrasonic sensors 
- To enable the ultrasonic sensor to emit ultrasound waves, a PWM signal is used, but as other circuits work with analog voltages, a PWM signal generator is needed to trigger the sensor.

- The ultrasonic sensor produces a PWM signal as output, which needs to be converted into a voltage for analysis by other circuits. This requires an additional circuit.

- Due to these conversions, there may be some loss of accuracy in the generated voltage, potentially affecting the robot's functionality.

### Reasons why use sharp ir sensors
- The Sharp IR sensor operates without needing triggering; it starts with a 5V voltage source.

- Its output is already in analog voltage, eliminating the need for additional PWM-to-analog conversion circuits, saving costs.

- Despite the sensor's distance-dependent behavior (proportional below 15cm, inverse proportional above 15cm), this can be managed by careful placement on the robot chassis.
![sharp ir](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/de36962b-a052-47be-8cc7-04dfe336c348)

## Block Diagram 
![block diagram](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/6c0335a3-481f-4b4c-b89d-44b74b07b03c)

## Main circuits used in the wall following robot are as follows:
- Instrumentation amplifier circuit
- PID controller circuit
- Triangular waveform generator circuit
- PWM signal generator circuit and turn adjustment circuit
- Motor driver circuit

### Instrumentation amplifier circuit
2 sharp IR sensors are used to measure the distance from both sides of the robot to the walls and the difference between the 2 output voltages are taken. Since the difference of the output of the sharp IR sensors is a small mV value, to reduce any interference caused by the power line and to compensate with a common mode rejection input, an instrumentation amplifier is used to get the difference between the inputs of the sharp IR sensors. The output of the instrumentation amplifier is the error signal which should be adjusted.

### PID controller circuit
The second yet the main thing the robot should do is if there is an error is present (Drifted away from the wall),that signal should be corrected and then should be given to the system to adjust the error. Therefore, a PID controller is used to correct any error signal. The output of the instrumentation amplifier is fed into the PID controller. PID controller is the main circuit present in the analog wall following robot where the error signal is adjusted and given to the system to reduce the error.

### Triangular waveform generator circuit
The triangle signal generator provides the frequency required for the basic PWM signal and the necessary ramp voltage (rise and down) to produce the PWM signal. By comparing the ramp voltage with the voltage output of the turn controller using a comparator, the required PWM signal can be generated. After generating the required separate PWM signals for the motors, the output should be given to the motor driver module. It will then drive the 2 motors moving the robot forward while keeping its middle path.

### PWM signal generator circuit and turn adjustment circuit
It should be considered that always a signal should be given to the motors to go forward and the adjusted signal from the PID controller should be given to that signal. 2 motors will be used for the robot. Therefore for the signal of one motor, that error should be added and should be subtracted from the signal of the other motor. Yet another important circuit comes into play, the turn adjustment control circuit which does the above task. Along with the turn adjustment, the forward speed of the motors is also regulated from this part of the circuit. The speed of rotation of motors is very important because it should match with the response time of the sharp IR sensors. Reducing the speed of the motors so the IR sensors can detect any change in the distance to the wall is recommended.

## Components Used
- Operational amplifier- **LM324N**
![LM324N](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/07ca3efd-51bc-4f96-9d37-af2bf8445edd)

- Motor driver - **L298N**
![morot drive](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/0f39e35b-1ecb-43f6-b45a-9b0675a8b46d)

- Resistors - **1k, 10k, 12k 470k**
- Capacitors - **0.01uF, 2.2uF, 27pF, 4.7pF**
- Batteries - **DE 18650 Li-ion**

## Simulation Results
Before the breadboard implementation, all the circuits and the total circuitry was simulated using LTSpice.
![LT spice](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/570d8e95-f13b-4276-8283-3f15f179fc09)

## Circuits being implemented in breadboards
![breaboard1](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/25ee8456-e44a-4ca3-a973-1d010a389516)

**Output PWM signals through the oscilloscope**
![breaboard2](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/1b288e24-bd9f-423a-a892-cd7bc6061c18)

## Enclosure of robot
The chassis was designed using Solidworks and then got laser cutting of the model.

![en1](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/b54bd8b5-ca35-40f9-98fc-5bc445b02d47)
![en2](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/9b6ed13d-0185-413f-af86-1b436e866484)
![en3](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/22f91810-24aa-488e-be5e-7ce77a5e8a70)
![en4](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/5bc80a45-d523-4e8f-883c-d5444c3006cf)

## PCBs 
All the four pcbs was designrf using Altium Designer. With the time constraints we had to print all the pcbs locally. 

## Final Outcome
After designing the schematics and the PCBs for the above mentioned circuits, the prototype of the analog wall following robot looked like as follows.

![final1](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/9a7696f6-8f4b-40db-a601-6487769568e2)
![final2](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/859669ab-4b9d-4358-b100-0263e2bd0fc7)
![final3](https://github.com/Upeksha-Dilhara/Analog-Wall-Following-Robot/assets/128304167/50a890e6-00eb-4667-872a-adc60870d875)

## Conclusion
In conclusion, creating an analog wall-following robot is both intriguing and demanding, even for dedicated robotics enthusiasts. However, the project offers valuable learning experiences by applying analog electronic principles to real-world applications.

We extend our heartfelt gratitude to Mr. Pahan Mendis, Mr. Hiruna Vidumina, and Mr. Hasantha Nadeeshan for their exceptional supervision and guidance, which played a pivotal role in making this project a resounding success.




