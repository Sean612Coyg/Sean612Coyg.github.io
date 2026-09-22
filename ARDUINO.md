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

## Wiring the Analogs 

<img width="778" height="566" alt="Screenshot 2026-09-21 at 9 52 53 PM" src="https://github.com/user-attachments/assets/0a5ad6d9-b9f5-42f8-a514-76124a6eb703" />


# Explaining the code

## Analogs and Pin readings

<img width="719" height="278" alt="Screenshot 2026-09-21 at 10 08 35 PM" src="https://github.com/user-attachments/assets/6f4308aa-1524-494a-a988-4fdc5b417725" />








