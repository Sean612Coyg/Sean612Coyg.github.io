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




# Things I learned

1. Hardware-Driven Cursor Navigation: Maps physical joystick inputs directly to a dynamic UI cursor index (focusedCardIndex) to highlight cards visually on screen before committing a play.
  
2. Non-Blocking AI Delays: Uses asynchronous timer functions (setTimeout) to simulate 3–5 second human-like AI thinking periods without locking the browser UI thread.
 
3. Real-Time LED Indicators: Triggers physical breadboard LEDs (digitalWrite()) in response to browser turn changes, offering visual feedback outside the digital screen.   

4. Algorithmic Mechanics: Features the Fisher-Yates Shuffle Algorithm to achieve an unbiased $O(n)$ randomized card deck shuffle each round.

5. Web Serial API Integration: Establishes direct browser-to-hardware communication over USB, bypassing the need for secondary local servers (e.g., Node.js or WebSocket bridges).

6. Analog Signal Processing & Thresholding: Reads continuous voltage signals from the joystick's X/Y potentiometers (analogRead()) and applies deadzones and movement locks to prevent input jitter or unintended double-scrolling.   

 ### Final Video


[View my Video Project](video.mp4)




 # Final Code
/*
  Fight the Landlord controller (Arduino Uno)
  VRx -> A4; VRy -> A5 (unused); joystick SW -> D2
  Separate mini button -> D3 and GND
  LEDs: You D4, Bot 1 D5, Bot 2 D6 (each through a 220-330 ohm resistor)
  Joystick VCC -> 5V; all GND connections -> Arduino GND.

  Tilt left/right: move the highlighted card (return to center each time).
  Click joystick straight down: select/deselect highlighted card.
  Press mini button: play selected cards, or pass if none are selected.
  During bidding: mini button bids the next available value.
  Other bidding choices use the on-screen buttons.
*/
#include <Arduino.h>
#include <string.h>

const byte PIN_JOY_X = A4;
const byte PIN_JOY_SW = 2;
const byte PIN_PLAY_BTN = 3;
const byte LED_P0 = 4;
const byte LED_P1 = 5;
const byte LED_P2 = 6;

// Reversed to match the orientation of your joystick.
// Set false if you later rotate or replace the joystick.
const bool REVERSE_X = true;
const int CENTER_MIN = 400;
const int CENTER_MAX = 620;
const int THRESHOLD_LOW = 250;
const int THRESHOLD_HIGH = 770;
const unsigned long DEBOUNCE_DELAY = 50;
bool movedX = false;

struct ButtonState {
  byte pin;
  bool lastReading;
  bool stableState;
  unsigned long changedAt;
};
ButtonState selectButton = {PIN_JOY_SW, HIGH, HIGH, 0};
ButtonState playButton = {PIN_PLAY_BTN, HIGH, HIGH, 0};

char incoming[24];
byte incomingLength = 0;
bool discardLine = false;
unsigned long lastTurnUpdate = 0;

void setTurnLEDs(int player) {
  digitalWrite(LED_P0, player == 0 ? HIGH : LOW);
  digitalWrite(LED_P1, player == 1 ? HIGH : LOW);
  digitalWrite(LED_P2, player == 2 ? HIGH : LOW);
}

void readButton(ButtonState &button, const char *command) {
  bool reading = digitalRead(button.pin);
  if (reading != button.lastReading) {
    button.changedAt = millis();
    button.lastReading = reading;
  }
  if (millis() - button.changedAt >= DEBOUNCE_DELAY &&
      reading != button.stableState) {
    button.stableState = reading;
    if (reading == LOW) Serial.println(command);
  }
}

void readJoystickInputs() {
  int x = analogRead(PIN_JOY_X);
  if (x >= CENTER_MIN && x <= CENTER_MAX) movedX = false;
  if (!movedX && (x < THRESHOLD_LOW || x > THRESHOLD_HIGH)) {
    bool left = (x < THRESHOLD_LOW);
    if (REVERSE_X) left = !left;
    Serial.println(left ? "NAV_LEFT" : "NAV_RIGHT");
    movedX = true;
  }
  // VRy is intentionally unused. Selection comes ONLY from the SW click.
}

void handleIncomingLine() {
  int player;
  if (strcmp(incoming, "TURN:0") == 0) player = 0;
  else if (strcmp(incoming, "TURN:1") == 0) player = 1;
  else if (strcmp(incoming, "TURN:2") == 0) player = 2;
  else if (strcmp(incoming, "TURN:OFF") == 0) player = -1;
  else return;
  setTurnLEDs(player);
  lastTurnUpdate = millis();
}

void readIncomingSerial() {
  // Consume complete lines without blocking joystick/button polling.
  while (Serial.available() > 0) {
    char c = Serial.read();
    if (c == '\r') continue;
    if (c == '\n') {
      if (!discardLine) {
        incoming[incomingLength] = '\0';
        handleIncomingLine();
      }
      incomingLength = 0;
      discardLine = false;
    } else if (!discardLine) {
      if (incomingLength < sizeof(incoming) - 1) incoming[incomingLength++] = c;
      else discardLine = true;
    }
  }
}

void setup() {
  Serial.begin(9600);
  pinMode(PIN_JOY_SW, INPUT_PULLUP);
  pinMode(PIN_PLAY_BTN, INPUT_PULLUP);
  pinMode(LED_P0, OUTPUT);
  pinMode(LED_P1, OUTPUT);
  pinMode(LED_P2, OUTPUT);
  digitalWrite(LED_P0, HIGH);
  digitalWrite(LED_P1, HIGH);
  digitalWrite(LED_P2, HIGH);
  delay(500);
  setTurnLEDs(-1);
  Serial.println("READY");
}

void loop() {
  readJoystickInputs();
  readButton(selectButton, "TOGGLE_SELECT");
  readButton(playButton, "BTN_PLAY");
  readIncomingSerial();
  // Turn lights off if the game stops sending its one-second heartbeat.
  if (millis() - lastTurnUpdate > 3500) setTurnLEDs(-1);
}



**file:///C:/Users/Sean/AppData/Local/Temp/8ed85bbd-747a-40f8-82a8-b501ee5d6450_landlord_joystick_update%20(2)(1).zip.450/gemini-code-1793038528517.html**






 


