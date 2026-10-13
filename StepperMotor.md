# Stepper Motor With Sean Wei and Wachi Manwichachai

## Materials
**Arduino Uno**: ATmega328P Microcontroller Board | 1 | Executes stepper control code and sends positioning signals. |

**Stepper Motor**: StepperOnline RoHS (17HE15-1504S) | 1 | Provides precise angular rotation for the scanning platform. |

**Stepper Motor Driver**: HW134A Driver Board | 1 | Amplifies signals from Arduino pins to drive the high-current stepper coils. |

**Breadboard**: Normal | 1 | Allows rapid, non-permanent circuit wiring and power rail distribution. |

**External Battery / Power Supply**: DC12V 5A 60W | 1 | Dedicated power to the stepper motor to prevent microcontroller brownouts. |

**Jumper Wires**: Male-to-Male & Male-to-Female | Assorted | Connects microcontroller digital pins, driver board, and power rails. |


## AI usage 

AI was critical in this project. It helped us code, understand the code that it gave us and help us solve problems regarding the code. Some prompts that we would give AI is, "Help us program the stepper motor so it could sync like a 3D scanner. Although it was easy to copy the code, AI helped us understand it even more. I would ask AI what a certain code meant, and it would give me a thorough explanation which was extremely useful. Google also helped us understand how to build the circuit. For example, if we did not understand how the driver motor worked, we would search on google the circuit diagram. 

Youtube was one of the most important element for us to finish this assignment. There was this one 30 minute video that went through how to use the stepper motor and driver, how to wire it correctly, and how to use the Multimeter. It took a long time for us to understand how to measure the AMP in the motor driver. Then after watching the Youtube video, we understood it and it was a huge milestone for us. 

[View the video](https://www.youtube.com/watch?v=wcLeXXATCR4&t=687s)


## First few days

We examined the youtube video attached above during the first few days. It was a great introduction for using the motor driver. The driver was also very fragile and therefore the video helped prevent the motor coils from overheating and burning. However, the motor driver is not automatic to the power that we wanted, so we limit the output by adjusting the potentiometer and measuring the Direct Current Voltage with a multimeter. AI also contributed to the wiring of the first prototype. It would show us the wiring diagram and respond by saying the VSS pin goes to ground. 

<video src="step1.mp4" type="video/mp4" controls width="600">
  Your browser does not support the video tag.
</video>
/*


## Final Project

<img width="1280" height="1707" alt="ef2a0b88fc9f6e7adeaeffe2be524b09" src="https://github.com/user-attachments/assets/a2c0d7d1-40f8-4c1a-87de-bdae9a0cffd1" />

After we are done with measuring the AMP for the motor driver, we proceeded with the wiring of it and then we start coding for the driver motor. The prompt that we put in for AI was, "Could you help me code the spinning of the stepper motor using a driver motor?" and AI would just give me the code for it. I would then ask it to explain it to me and it would with immense detail. 

### Final Project

<video src="step2.mp4" type="video/mp4" controls width="600">
  Your browser does not support the video tag.
</video>
/*'

In this video the stepper motor was turning with the command of the code with a periodic turn of 90 degrees to make the object appear more visual on the 3D scanning site. I also used some AI to help me explain how to turn the motor and I added the code myself with Wachi into the actual arduino code.
