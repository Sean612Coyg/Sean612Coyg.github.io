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







