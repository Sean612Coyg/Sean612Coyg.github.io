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



Component	Arduino Pin	Purpose
LCD RS	Pin 13	Register Select control line
LCD RW	GND	Hardwired to Ground for Write mode
LCD Enable (E)	Pin 4	Execution enable signal
LCD Data (D0–D7)	Pins 5, 8, 9, 7, 12, 10, 6, 11	8-bit parallel data bus
Start / Pause Button	Pin 2 (INPUT_PULLUP)	Toggles timer between active and paused
Reset Button	Pin 3 (INPUT_PULLUP)	Resets countdown and silences active alarm
Piezo Buzzer	Pin A0	Emits pulsing audio alarm on completion
DC Motor	Pin A5	Physical motion indicator output

