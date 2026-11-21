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

We visualized a build that we would later based our project on. 

<img width="1166" height="1243" alt="image" src="https://github.com/user-attachments/assets/02745412-a3bd-47e1-b677-ef94eacf1234" />

The first days were just remembering what stepper motor were. We would look at our past documentaries on GitHub and review the basic fundamentals of how to wire the stepper motor and the driver. 


### The first week

The first week went by slow, we started our build but never actually did major innovations on. We were stuck on the multimeter for a long time and wasn't able to get it to work. Wachi also took a long time to figure out the code for the spinning of the stepper motor. 


### Second week

During the second week, we really started to progress. We had a concrete blueprint to base our design on. Moreover, thanks to Dr. Dzula we were able to use the robotics lab and the tools in there. It was really helpful and it allowed us to add the layering design for the 3-d scanner.

<video src="stepM.mp4" type="video/mp4" controls width="600">
  Your browser does not support the video tag.
</video>
/*

## Trouble Shoot

1. The first problem that we encountered was that there were no accurately sized parts that allows us to put the 3-D scanned object on, so me and John CADDED a circular object with an adapter that allowed the stepper motor to hold an object that is 3-D scannable.


<img width="960" height="1280" alt="f3f7a5b9600f923d25476748e596963a" src="https://github.com/user-attachments/assets/4e2f8dfe-f486-42d7-b2ec-78b4de94f77f" />


But then quickly we realized that the apadter is still too weak to carry the weight of the object above it, so me and John increased the dimensions of it. We added 0.5 mm to the CAD and then it worked flawlessly. 

2. Another problem that we encountered was how the machine that was connected to the belt that lifted the sensor was really unstable. But then I realized that John screwed in a M3 instead of M4 screw, so I fixed it and it became much more stable.

<img width="810" height="1440" alt="bee2789ee28071ecdf1bb0cc534dbef8" src="https://github.com/user-attachments/assets/baf7503f-4885-461e-aa1f-11559cb50ed3" />

3. Another problem was how we needed a flat surface to make the 3-D scanner flat so it could stand up. John Cadded 4 corner piece that made the surface flat.

<img width="810" height="1440" alt="a1e762bb8b7f64162f2bbee8043d27bc" src="https://github.com/user-attachments/assets/d6ebe244-3444-459f-bff2-a801b9c8734d" />



### Arduino Programming and Motor Testing

Another major part of our project involved connecting the stepper motors to the Arduino and writing code to control them. We used an Arduino Uno R3 and experimented with different motor setups. Our goal was to independently control the motor responsible for the rotating platform and the motor responsible for the vertical movement mechanism. However, at this stage, our Arduino program is still a very early prototype.

### Code
const int stepX = 2;
const int dirX = 5;

const int stepY = 3;
const int dirY = 6;

const int enablePin = 8;

// Smaller interval = faster rotation
const unsigned long fastSpeed = 5000;
const unsigned long slowSpeed = 20000;

unsigned long lastStepX = 0;
unsigned long lastStepY = 0;

void setup() {
  pinMode(stepX, OUTPUT);
  pinMode(dirX, OUTPUT);

  pinMode(stepY, OUTPUT);
  pinMode(dirY, OUTPUT);

  pinMode(enablePin, OUTPUT);

  digitalWrite(dirX, HIGH);
  digitalWrite(dirY, HIGH);

  digitalWrite(enablePin, LOW);
}

void loop() {
  unsigned long currentTime = micros();

  // Motor 1: Fast rotation
  if (currentTime - lastStepX >= fastSpeed) {
    lastStepX = currentTime;

    digitalWrite(stepX, HIGH);
    delayMicroseconds(5);
    digitalWrite(stepX, LOW);
  }

  // Motor 2: Slow rotation
  if (currentTime - lastStepY >= slowSpeed) {
    lastStepY = currentTime;

    digitalWrite(stepY, HIGH);
    delayMicroseconds(5);
    digitalWrite(stepY, LOW);
  }
}


Our current program is designed mainly to test whether the motors can rotate continuously. We have experimented with running two stepper motors at different speeds. One motor is intended for the rotating object platform, while the other is intended for the vertical belt mechanism. At the moment, our code simply keeps the motors spinning - one slow, the other fast. It does not yet perform an automated 3D scanning sequence.



### Physical Design

<img width="1702" height="1276" alt="18849c3f712d696c26f47cd1121db29f" src="https://github.com/user-attachments/assets/6ca6ce01-8d4d-4c94-a1d7-8bf4373ddf0b" />




### Future of the project

We still had not finished the project yet, lacking the ability to actually scan the object and export it onto a website or program. However, we are really close to that as we have a functioning pulley system that allows the sharp sensor to scan the object at anywhere and having no major scanning flaws. 

To improve, we have to either borrow Kaiden's scanning program or develop one ourselves and export the 3-D scan.










