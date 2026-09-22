<style>
header {
  display: none;
}

footer {
  display: none;
}

.wrapper {
  width: 95%;
  max-width: none;
  margin: 0 auto;
}

section {
  width: 100%;
  float: none;
}

body {
  padding: 20px;
}
</style>

# Timer LCD Alarm

## Project Overview 
For this project, I used an 16x2 parallel LCD screen, a piezo buzzer, a "fan" motor, and two pushbuttons to build an interactive, countdown timer powered by an Arduino Uno.

The LCD screen is connected to analog {13, 4, 5, 8, 9, 7, 12, 10, 6, 11}. 

The Piezo Buzzer is connected to analog {A0}.

The Potentiometer connected to analog {V0 of LCD, and (+) (-)}.

The two Button connected to analog {2, 3}.

The motor connected to {A5}

## Skill that I am building on

Through this project, the skill that I am building on is the constant trouble shooting and wire management. Since, there are so much pins involved with the LCD screen, I really have to keep track of which analog pin goes to which pin of the LCD screen. I also have gone through a lot of issues with my breadboard and LCD screen which I will explain later. 

## The LCD Screen

<img width="970" height="728" alt="image" src="https://github.com/user-attachments/assets/b065893b-34cb-4748-91c8-6f7db75fd55f" />

I chose to use a LCD display screen for this project as a new component. I found its information on [Link](https://docs.arduino.cc/learn/electronics/lcd-displays/). I used the LCD because it is versatile, and it could display a lot of things on it. Moreover, the LCD screen is interconnectable to other pieces of components such as the buzzer and the potentiometer. 

## Wiring the Analogs 

<img width="778" height="566" alt="Screenshot 2026-09-21 at 9 52 53 PM" src="https://github.com/user-attachments/assets/0a5ad6d9-b9f5-42f8-a514-76124a6eb703" />


# Explaining the code

## Analogs and Pin readings

<img width="719" height="278" alt="Screenshot 2026-09-21 at 10 08 35 PM" src="https://github.com/user-attachments/assets/6f4308aa-1524-494a-a988-4fdc5b417725" />

This part of my code assigns the physical analog pins on the Arduino board to represent the X (horizontal) and Y (vertical) signal pins.

<img width="383" height="198" alt="Screenshot 2026-09-22 at 9 11 57 AM" src="https://github.com/user-attachments/assets/495816c7-4d6a-461c-8613-4786e674a963" />

The first line creates a variable to hold how many seconds are left on the clock. It starts off set to whatever starting time you defined (like 5 seconds).

Then the (boolean) acts like the on/off switch for the timer displayed on the LCD screen. False is paused and True is counting down. 

The third line means that I could store whatever timestamp(in ms) when the timer last subtracted 1 second. 

The second part first line keeps track of the previous reading for each button as High is the default. For example, high is not pressed and low is pressed.

Then it is for calculating how long the time passed since I last pressed the button.

Lastly, there is a 50 milli-second wait. The code ignores the fast bounce or flickers to minimize bugs. 

<img width="352" height="266" alt="Screenshot 2026-09-22 at 9 18 18 AM" src="https://github.com/user-attachments/assets/1f3c9d8f-345a-4846-a831-28d865e43e52" />

The setup() allows this code to run as soon as the Arduino powers up or resets. 

The code inside the setup configures the hardware pins for the button, motor, and buzzer. It also sets up the buttons using the (INPUT_PULLUP) which is an internal pull-up resistor. The button also sets the motor and buzzer pin as output, and displayed the default starting screen on the LCD screen. 
  
**  showTime();
  lcd.setCursor(0, 1);
  lcd.print("Press to start");**

<img width="474" height="283" alt="Screenshot 2026-09-22 at 9 30 50 AM" src="https://github.com/user-attachments/assets/c97b5eb3-d8a6-4d66-94e7-60b11de4368e" />

In loop() the code makes it so it could continuously check for button inputs while tracking time using millis(). 

Every 1000 milliseconds(1 sec) that the timer is active (running == true), it decreases the remaining time by 1.

Then it would refresh the screen and trigger timeUp() alarm when the timer reaches zero. 


<img width="574" height="257" alt="Screenshot 2026-09-22 at 9 34 17 AM" src="https://github.com/user-attachments/assets/49a13b24-fa7e-4de0-baad-a266c9050174" />

handleButtons() acts as a function that reads the state of both of the buttons(reset, and pause/start). 

the digitalRead() checks the Voltage status on START_PAUSE_PIN and RESET_PIN. It returns to HIGH when released and LOW when pressed.

Then there is a if ...

The first if is for comparing the current time against the last time a button is pressed. If at least 50 millisecond (debounceDalay) have passed, it would allow the button to be processed. This hinders the rapid contact present in the button. 

<img width="552" height="161" alt="Screenshot 2026-09-22 at 9 38 56 AM" src="https://github.com/user-attachments/assets/cee87c79-f685-4c7b-b339-963988af1bb0" />

Then there is two {if}.

The first one: **if (startPauseReading == LOW && lastStartPauseState == HIGH) {**
checks if the button is pressed in this exact instant --> (from HIGH to LOW). 

**lastDebounceTime = millis();** means that it resets the debounce timestamp to start the 50ms timer over again

**if (remainingSeconds > 0) {
        running = !running;
        lastTickMillis = millis();
        updateStatusLine();
      }
    }**
This **if** means that if there is time left on the clock, flip the timer between running and paused, reset the 1-second interval timer, and update the display status.

<img width="470" height="189" alt="Screenshot 2026-09-22 at 10 00 46 AM" src="https://github.com/user-attachments/assets/a1f36f24-0d9b-4022-af68-304800f5ba62" />

Detects when the Reset button goes from HIGH to LOW.

**running = false;** Stops the countdown.

**remainingSeconds = countdownStartSeconds;** Resets the clock variable back to its initial value.

**showTime() & updateStatusLine()** Updates the LCD display to show the starting time and "Paused".

**noTone(BUZZER_PIN);** means turns off the buzzer output in case the alarm is currently ringing.


**lastStartPauseState = startPauseReading; lastResetState = resetReading;**

This updates the time as well as the "state of the button" allowing the cycle to repeat smoothly without missing a single button press.

<img width="357" height="77" alt="Screenshot 2026-09-22 at 10 05 27 AM" src="https://github.com/user-attachments/assets/bda5ccac-007e-477c-b509-56469a7d6f16" />

This code converts the total (remainingSeconds) into minutes and seconds using integer math:

Division (/ 60): Calculates total full minutes.

Modulo (% 60): Calculates the leftover seconds.


<img width="410" height="178" alt="Screenshot 2026-09-22 at 10 06 30 AM" src="https://github.com/user-attachments/assets/97a4cc67-296a-405a-8bc0-8a9e3109e3e1" />

In LCD display the initial position must be (0,0) to display. And the first line moves the LCD cursor to row 0, column 0.

Leading Zeros: if (minutes < 10) and if (seconds < 10) add a "0" prefix before single-digit numbers so the screen displays 05:09 instead of 5:9."Basically, it fixes the format and adds a "0" before every single digit number."

Trailing Spaces ("   "): Overwrites remaining characters on the line to prevent old digits from staying visible when the number of digits decreases.

<img width="443" height="165" alt="Screenshot 2026-09-22 at 10 18 07 AM" src="https://github.com/user-attachments/assets/66054e53-820b-49c8-929d-79e87ec09c44" />

Sets the LCD cursor to the beginning of the second row (row 1). (0,1)

Prints "Running..." if running is true, or "Paused" if running is false.

**void timeUp() { lcd.setCursor(0, 1); lcd.print("TIME'S UP!!!    ");**

This code displays the "time up" output on LCD screen.

<img width="666" height="242" alt="Screenshot 2026-09-22 at 10 30 40 AM" src="https://github.com/user-attachments/assets/99935e5b-021b-4516-9def-204e57761ddf" />


Then there is a while loop, where it would run the code continuously for up to 10 seconds of the beeping sound for the buzzer. 

The if checks inside the while loop if the reset button is pressed hence the **(digitalWrite(MOTOR_PIN, LOW);**) 

**noTone(BUZZER_PIN);** means that if the button is pressed it turns off the sound and motor. 

<img width="672" height="230" alt="Screenshot 2026-09-22 at 12 22 51 PM" src="https://github.com/user-attachments/assets/d8dcccec-91e7-40cf-93c3-adc95e56c5b2" />

The first line means that it takes a snapshot of the current time so the code can measure how much time has passed since the last sound toggle.

The if means that if the Alarm is producing noise (toneOn = true) and it has been sounding for at least 300 milliseconds. It turns the sound off.

The else if conveys that is the Alarm is silent (toneOn = true) and it has been silent for 200 millisecond, it turns the sound on.

In summary the if shuts the sound off after 300ms and the else if turns the sound back on after 200ms pause. 


## Things that did not work out for me

### The first is the the lack of Analog pins

My first design was to create a LCD display that has a buzzer and the LCD would display the lyrics of a song. But that did not work out for me as I needed more analog pins than what the Arduino supplied. So instead of it displaying lyrics, I would use the LCD to do a countdown alarm requiring way less analog pins than my original design. 

Then it was with the fan. I had to 3-D print something that contains the fan, but since the fan did not fit in the disign and the library was closed, I had no way to fit the fan in. So I made the fan a "motor" for my Arduino. 

<img width="1280" height="1707" alt="dbc7097e7983182a59a28edbcce8748f" src="https://github.com/user-attachments/assets/9fc49afb-a9a8-4589-81ec-afb8de3d6ef6" />


## My final product and code

<video width="700" controls>
  <source src="videos/videolast.mp4" type="video/mp4">
</video>

/*
  LCD Countdown Timer (8-bit parallel LCD, no I2C backpack)
  -----------------------------------------------------------
  Wiring:
    LCD RS -> Arduino 13
    LCD RW -> GND (tied directly, not to an Arduino pin)
    LCD E  -> Arduino 4
    LCD D0 -> Arduino 5
    LCD D1 -> Arduino 8
    LCD D2 -> Arduino 9
    LCD D3 -> Arduino 7
    LCD D4 -> Arduino 12
    LCD D5 -> Arduino 10
    LCD D6 -> Arduino 6
    LCD D7 -> Arduino 11

    LCD VSS -> GND
    LCD VDD -> 5V
    LCD V0  -> center pin of a contrast potentiometer (other two legs to 5V and GND)
    LCD A (backlight +) -> 5V (through a resistor if your board doesn't have one built in)
    LCD K (backlight -) -> GND

    Start/Pause button: one leg -> Pin 2, other leg -> GND
    Reset button:       one leg -> Pin 3, other leg -> GND
      (both use internal pull-ups, no external resistors needed)

    Motor  -> Pin A5
    Buzzer -> Pin A0 (positive leg), other leg -> GND

  Library required: built-in "LiquidCrystal" (comes with Arduino IDE, no install needed)
*/

#include <LiquidCrystal.h>

// ---- Configuration ----
const int LCD_COLUMNS = 16;
const int LCD_ROWS = 2;

const int START_PAUSE_PIN = 2;
const int RESET_PIN = 3;
const int MOTOR_PIN = A5;
const int BUZZER_PIN = A0;

long countdownStartSeconds = 5;  // <-- change starting time here (in seconds)

// ---- LCD pin setup: RS, E, D0, D1, D2, D3, D4, D5, D6, D7 ----
LiquidCrystal lcd(13, 4, 5, 8, 9, 7, 12, 10, 6, 11);

// ---- Globals ----
long remainingSeconds = countdownStartSeconds;
bool running = false;
unsigned long lastTickMillis = 0;

// simple debounce tracking
bool lastStartPauseState = HIGH;
bool lastResetState = HIGH;
unsigned long lastDebounceTime = 0;
const unsigned long debounceDelay = 50;

void setup() {
  pinMode(START_PAUSE_PIN, INPUT_PULLUP);
  pinMode(RESET_PIN, INPUT_PULLUP);
  pinMode(MOTOR_PIN, OUTPUT);
  digitalWrite(MOTOR_PIN, LOW);
  pinMode(BUZZER_PIN, OUTPUT);
  digitalWrite(BUZZER_PIN, LOW);

  lcd.begin(LCD_COLUMNS, LCD_ROWS);

  showTime();
  lcd.setCursor(0, 1);
  lcd.print("Press to start");
}

void loop() {
  handleButtons();

  if (running && millis() - lastTickMillis >= 1000) {
    lastTickMillis = millis();
    if (remainingSeconds > 0) {
      remainingSeconds--;
      showTime();
    }
    if (remainingSeconds == 0) {
      running = false;
      timeUp();
    }
  }
}

void handleButtons() {
  bool startPauseReading = digitalRead(START_PAUSE_PIN);
  bool resetReading = digitalRead(RESET_PIN);

  if (millis() - lastDebounceTime > debounceDelay) {
    // Start/Pause button pressed (goes LOW when pressed)
    if (startPauseReading == LOW && lastStartPauseState == HIGH) {
      lastDebounceTime = millis();
      if (remainingSeconds > 0) {
        running = !running;
        lastTickMillis = millis();
        updateStatusLine();
      }
    }

    // Reset button pressed
    if (resetReading == LOW && lastResetState == HIGH) {
      lastDebounceTime = millis();
      running = false;
      remainingSeconds = countdownStartSeconds;
      showTime();
      updateStatusLine();
      noTone(BUZZER_PIN); // stop alarm if it was buzzing
    }
  }

  lastStartPauseState = startPauseReading;
  lastResetState = resetReading;
}

void showTime() {
  int minutes = remainingSeconds / 60;
  int seconds = remainingSeconds % 60;

  lcd.setCursor(0, 0);
  lcd.print("Time: ");
  if (minutes < 10) lcd.print("0");
  lcd.print(minutes);
  lcd.print(":");
  if (seconds < 10) lcd.print("0");
  lcd.print(seconds);
  lcd.print("   "); // clear leftover chars
}

void updateStatusLine() {
  lcd.setCursor(0, 1);
  if (running) {
    lcd.print("Running...      ");
  } else {
    lcd.print("Paused          ");
  }
}

void timeUp() {
  lcd.setCursor(0, 1);
  lcd.print("TIME'S UP!!!    ");

  digitalWrite(MOTOR_PIN, HIGH);

  // Alarm: beep on/off for up to 10 seconds, but stop immediately if Reset is pressed
  unsigned long alarmStart = millis();
  bool toneOn = false;
  unsigned long lastToggle = millis();

  while (millis() - alarmStart < 10000) {
    // Check for Reset button press (LOW = pressed, using internal pull-up)
    if (digitalRead(RESET_PIN) == LOW) {
      noTone(BUZZER_PIN);
      digitalWrite(MOTOR_PIN, LOW);
      running = false;
      remainingSeconds = countdownStartSeconds;
      showTime();
      lcd.setCursor(0, 1);
      lcd.print("Paused          ");
      delay(200); // brief debounce so the same press isn't re-read in loop()
      return;     // exit timeUp() immediately
    }

    // Toggle tone on/off roughly every 300ms/200ms without blocking on Reset checks
    unsigned long now = millis();
    if (toneOn && now - lastToggle >= 300) {
      noTone(BUZZER_PIN);
      toneOn = false;
      lastToggle = now;
    } else if (!toneOn && now - lastToggle >= 200) {
      tone(BUZZER_PIN, 2500);
      toneOn = true;
      lastToggle = now;
    }
  }

  noTone(BUZZER_PIN);
  digitalWrite(MOTOR_PIN, LOW);
}

## Peer Support

Watchi really helped me with teaching me how to wire the LCD display. He gave me tips on how to wire correctly, and how to manage wires. He also provided me with pictures of his design so I could learn from him. He inspired me to change my design from a lyric producer to an alarm clock, and gave me ideas about how I should use the analog pins. 

## Reflection
My timer system would be useful for people who are taking a break from electronics, for example. They could set the alarm for 5 minutes and then chill until the buzzer starts to beep signaling that their break is over. I could also use this as an interval for waking me up. 

I could set a 30-minute timer and take a nice nap before going to afternoon activities.  
Some modifications could be I change my code so that so users can change the duration on the fly without reprogramming the board. To do this, I could add a keypad to input the time without changing the code.  


I would use the non-blocking code as without them, adding features like dynamic button menu navigation or multi-pattern alarms would cause the system to freeze or become unresponsive to user input. These include, delay(). 


## Chapters while designing 

<img width="1280" height="1707" alt="d66f8055d974f9afe4f5febc46c28516" src="https://github.com/user-attachments/assets/71098f76-48ac-4ee3-99c6-2fe0c684a285" />

In this image, I plugged in all the LCD wires but it didn't turn on. I later found that my code didn't correspond with my analog pin and I changed it later. 

<img width="1280" height="1707" alt="5732ef0678e345cf412e3656c8c81e93" src="https://github.com/user-attachments/assets/662f7814-d6ed-42a9-9309-142d15649eaf" />

In this image, I added a Potentiometer which would help me change the brightness for my LCD. It is a must-have piece for my Arduino project as it controls the current flowing. 

<img width="1280" height="1707" alt="e495806d93968741f2f12c0f6c2dbf23" src="https://github.com/user-attachments/assets/dad7a4b5-7793-49ae-abb0-08924b9936e1" />

I then added buttons to this project so the time could be controlled. 


video/06add66bcab2f785d333c3f21075d628.mp4

This video showcases my LCD design with the button functioning before I added the buzzer. 
 










