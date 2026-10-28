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



# Day one

Day one I was brainstorming with my groupmates about some possible designs:

1. Using a button for playing the cards and joystick for moving the cursor.

2. Making the joystick the most important component, the pressing of it controls the card

3. LED that symbolizes the turn, a joystick that only controls the direction of movement and a button that plays the card and skips turns.


# Day two and three

Day two and three me and my groupmates start to lock-in and do the work. We completed the code and during the upload we encountered the issue of how the code doesn't really connect to the website game. 

Some things that we did to resolve:

Checking the Serial Baud Rate: Both the Arduino sketch (Serial.begin(9600)) and the browser-side script need to share the exact same baud rate, or the data gets scrambled into unreadable characters.

Closing Conflicting Ports: If the Arduino IDE's Serial Monitor window is left open, the browser's Web Serial API gets blocked from accessing the USB port because only one program can use it at a time.

Using a Compatible Browser: The Web Serial API requires a Chromium-based browser like Google Chrome or Microsoft Edge to prompt the user to select the device's COM port.

Formatting Data Correctly: Making sure the Arduino sends data ending with a newline (Serial.println()) helps the JavaScript side parse lines cleanly.



Then we uploaded the code and we were able to start playing and controlling the cards that we play. 
<img width="1320" height="990" alt="469e647437387340536845f555a83dee" src="https://github.com/user-attachments/assets/37e5fded-00a7-44af-8182-1f334e7e5ad2" />




We then proceeded to test the thumb joystick to make sure moving it left and right smoothly navigated through our hand of cards, pushing it up selected them, and pressing the pushbutton successfully submitted our plays. Then the LED and button. 



 ### Final Video

 


