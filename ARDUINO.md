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
    







