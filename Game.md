# Game with Joystick

# Materials
Arduino Uno Microcontroller Board: This is the main brain of the hardware setup that processes inputs from your physical controls and manages communication with your computer via USB.   

Breadboard: A solderless platform used to securely connect and wire the electronic components together without needing permanent solder.   

Thumb Joystick Module: Located at the bottom of the breadboard, it allows you to move left or right to navigate through your hand of cards and push up to select or deselect cards.   

Pushbutton Switch: Located on the left side of the breadboard, it acts as the primary action button to play selected cards, pass your turn, or confirm bids.   LEDs (Light Emitting Diodes): Positioned on the breadboard to visually indicate whose turn it is (such as your turn versus the AI opponents' turns).   

Resistors: Small components used on the breadboard to limit electrical current to the LEDs and stabilize button input signals.   

Jumper Wires: The colored wires routing power (5V), ground (GND), analog signals (to pins A0 and A1), and digital signals (to digital pins) between the Arduino board and the breadboard components.+



# AI usage 


Normally, connecting a physical microcontroller like an Arduino to a web browser requires complicated background servers or bridge software. AI help me design solutions using modern browser capabilities like the Web Serial API, writing both ends of the system:

1. The C++ Arduino Code: Configures analog pins for the joystick, digital pins for the button and LEDs, and handles serial communication (Serial.begin(9600)).

2. The JavaScript Frontend: Listens to incoming serial ports right inside the browser tab, translating hardware signals into game actions instantly without extra downloads.



Wiring up new components for me can be intimidating when dealing with power, ground, and digital/analog inputs. AI helped me by mapping out clear pinout guides (such as assigning X to A0, Y to A1, the button to pin 2, and turn LEDs to pins 8, 9, and 10). Explaining why a pin is used—like utilizing internal pull-up resistors (INPUT_PULLUP) so a button doesn't need external hardware—turns abstract wiring into a clear logic lesson.



AI also help me write the codes and truely understand them. 

1. State Management: Keeping track of game phases (BIDDING, PLAYING, GAME_OVER) in a central structure.

2. Algorithmic Logic: Implementing proper shuffling routines like the Fisher-Yates algorithm to ensure fair card distribution.

3. UI Feedback Loops: Managing timing delays (setTimeout) so AI opponents mimic a human "thinking" pace while updating physical LED indicators on your board.



