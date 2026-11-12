# 3-D scanner with John Deng and Wachi 


## Materials

**Stepper Motor** StepperOnline | 1 | Provides precise angular rotation for the scanning platform. |

**Stepper Motor Driver**: HW134A Driver Board | 1 | Amplifies signals from Arduino pins to drive the high-current stepper coils. |

**Breadboard**: Normal | 1 | Allows rapid, non-permanent circuit wiring and power rail distribution. |

**External Battery / Power Supply**: DC12V 5A 60W | 1 | Dedicated power to the stepper motor to prevent microcontroller brownouts. |

**Jumper Wires**: Male-to-Male & Male-to-Female | Assorted | Connects microcontroller digital pins, driver board, and power rails. |

**3D printed parts** PLA | 3 | The parts for the platform, some of the lifting for the design and the adapter for the Stepper motor. |


## AI usage

AI again helped us immensely, we used AI to help us review what the stepper motor was again. We also asked it for some design strategies and what to prevent. The code that AI provided us was also really helpful. If we had things that we did not know how to do, such as wiring, we would ask AI to generate a wire diagram. I would ask AI what a certain code meant, and it would give me a thorough explanation which was extremely useful. Google also helped us understand how to build the circuit. For example, if we did not understand how the driver motor worked, we would search on google the circuit diagram.

Youtube was one of the most important element for us to finish this assignment. There was this one 30 minute video that went through how to use the stepper motor and driver, how to wire it correctly, and how to use the Multimeter. It took a long time for us to understand 
how to measure the AMP in the motor driver. Then after watching the Youtube video, we understood it and it was a huge milestone for us.


[View the video](https://www.youtube.com/watch?v=wcLeXXATCR4&t=687s)


[View the video](https://www.youtube.com/watch?v=7spK_BkMJys&t=136s)

These two videos both helped us setup the stepper motor and allowed us to further enhance our knowledge on the Arduino piece that was unfamiliar to us. 




## Process

### First days

The first days were just remembering what stepper motor were. We would look at our past documentaries on GitHub and review the basic fundamentals of how to wire the stepper motor and the driver. 




## Trouble Shoot

1. The first problem that we encountered was that there were no accurately sized parts that allows us to put the 3-D scanned object on, so me and John CADDED a circular object with an adapter that allowed the stepper motor to hold an object that is 3-D scannable.


<img width="960" height="1280" alt="f3f7a5b9600f923d25476748e596963a" src="https://github.com/user-attachments/assets/4e2f8dfe-f486-42d7-b2ec-78b4de94f77f" />


But then quickly we realized that the apadter is still too weak to carry the weight of the object above it, so me and John increased the dimensions of it. We added 0.5 mm to the CAD and then it worked flawlessly. 

2. Another problem that we encountered was how the machine that was connected to the belt that lifted the sensor was really unstable. But then I realized that John screwed in a M3 instead of M4 screw, so I fixed it and it became much more stable.

<img width="810" height="1440" alt="bee2789ee28071ecdf1bb0cc534dbef8" src="https://github.com/user-attachments/assets/baf7503f-4885-461e-aa1f-11559cb50ed3" />

3. Another problem was how we needed a flat surface to make the 3-D scanner flat so it could stand up. John Cadded 4 corner piece that made the surface flat.

<img width="810" height="1440" alt="a1e762bb8b7f64162f2bbee8043d27bc" src="https://github.com/user-attachments/assets/d6ebe244-3444-459f-bff2-a801b9c8734d" />











