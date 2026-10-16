# Tic Tac Toe

## Process

During class today, I used WebbGPT to create a functional, clean, interactive Tic Tac Toe game built with HTML and some JavaScript. Instead of using "canvas", WebbGPT used CSS grid layout with some button elements for a more interactive and responsive layout.

<img width="707" height="407" alt="image" src="https://github.com/user-attachments/assets/a0407bb1-9390-4b34-befc-44650462203c" />

## Code Explanation

**Where is it in the HTML?** Unlike physics-based arcade games that use an HTML / <canvas> element, my game renders the board inside a standard <div> container with the id #board.

<img width="237" height="61" alt="image" src="https://github.com/user-attachments/assets/53aa1408-ea37-4d69-84d3-45a5b3954aca" />


The layout is controlled via CSS Grid rather than fixed canvas pixel dimensions. The code that controls this is:

<img width="233" height="173" alt="image" src="https://github.com/user-attachments/assets/c82a4d1b-2bb0-45ac-aea8-5047c4be9d3f" />


If you modify grid-template-columns: **repeat(3, 100px)** or the **.cell width and height**, the grid cells will be larger or smaller while maintaining a  3 x 3 layout. Because it's DOM-based rather than canvas, text scaling (font-size: 3em) automatically scales the X and O markers to match the new box dimensions.



**State Variables:** The game tracks its data using four state variables that is at the start of the <script> block:

<img width="206" height="50" alt="image" src="https://github.com/user-attachments/assets/5517a015-28a3-4b62-86e6-cec130fcbf37" />

let board = Array(9).fill('');     // Tracks the state of each cell ('X', 'O', or empty '')
let currentPlayer = 'X';           // Tracks whose turn it is ('X' or 'O')
let gameOver = false;              // Boolean flag locking the board when a win or draw occurs
let scores = { X: 0, O: 0 };       // Keeps track of the cumulative session score



**The game loop:** Tic Tac Toe does not need a continuous loop unlike other games because it is a event based game meaning that the game responds by the click of a mouse. Thus there is no need for a continuous loop. 

Instead Tic Tac Toe runs on Javascript with clicks of the mouse. Specifically, **<makeMove(i)>**.

Each time a move is made, it performs two main jobs:

1. Updates the board array and writes the text/class attributes to the clicked cell.
2. Runs checkWin() and checks for a draw, updating the status message and score elements accordingly.


function makeMove(i) {
  if (gameOver || board[i] !== '') return;  // ignore invalid clicks

  // --- JOB 1: Mutate State & DOM ---
  board[i] = currentPlayer;                  // Updates the internal state array
  cells[i].textContent = currentPlayer;      // Writes the text ('X' or 'O') to the DOM
  cells[i].classList.add(currentPlayer.toLowerCase()); // Adds CSS styling class

  // --- JOB 2: Evaluate Conditions (Win, Draw, or Switch Turn) ---
  const winningLine = checkWin();
  if (winningLine) {
    winningLine.forEach(idx => cells[idx].classList.add('winner'));
    scores[currentPlayer]++;
    scoreEl.textContent = `X: ${scores.X} | O: ${scores.O}`;
    statusEl.textContent = `🎉 Player ${currentPlayer} wins!`;
    gameOver = true;
  } else if (!board.includes('')) {
    statusEl.textContent = "It's a draw!";
    gameOver = true;
  } else {
    currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
    statusEl.textContent = `Player ${currentPlayer}'s turn`;
  }
}




**Input Handling:** When the mouse click the 3x3 grid, the input is registered. The event listener is the attached to the 9 cell grid when generated. 

When a valid cell is clicked, makeMove(i) checks if **gameOver** is true or if the cell is already occupied. If true, the function <makeMove> assigns currentPlayer to board[i], updates the button's text content, and toggles CSS classes (x,o).

This is how the game register the inputs. 



**Collision / win-lose logic:** The checkWin() function compares the current board array values against the WIN_COMBOS index sets:

<img width="600" height="142" alt="Screenshot 2026-10-15 at 10 54 13 AM" src="https://github.com/user-attachments/assets/d9d1440a-a834-480a-b149-b8da87666486" />


Conditions:

1. uses checkWin() to check if you won. If a value is detected then you win.
2.  If !board.includes('') (when all cells are non-empty and no win was detected). meaning if there if all cells are non empty and no element(x,o) is filled 3 in a row it is a tie.


**scoring:** The code line that initialize the score is: let scores = { X: 0, O: 0 };


When a player wins, the score is incremented and written to the DOM:

<img width="508" height="67" alt="Screenshot 2026-10-15 at 4 57 58 PM" src="https://github.com/user-attachments/assets/a67c2f3d-99d7-4baf-9d37-ea4008d670a3" />

This is basically how it is calculated. 

### If still wondering how the points are tallied:

When a player makes a move, the function checkWin() immediately evaluates if that move completed any of the 8 winning combinations (rows, columns, or diagonals). If it finds a match, it returns that winning line, confirming the current player (currentPlayer) has won.



### Based on your process, what you noticed, and what you learned, set some meaningful goals for the week. Entries will be graded on the clarity of your goals, and how they relate to your documented, in-class process.


**Some cool innovations and ideas that I learned:**

Tic Tac Toe that WebbGPT coded for me uses an event-driven DOM model using standard HTML <button> elements inside a CSS Grid layout different from the traditional <canvas>.


Instead of running a continuous game loop (requestAnimationFrame), state updates and UI re-renders only occur when a user fires a click event.

Win detection relies on comparing array indices against predefined index patterns (WIN_COMBOS), triggering score increments on the scores object.


### Goals

To do a more advanced game and to educate others about it or helping others learn Chinese through my game. Therefore, I decide to do a game dealing with the traditional Chinese poker game, "斗地主“ where there are 3 players and the first one to play all their cards win. It has a complicated rule set that a hint button would explain in the beginning of the game. There would be pinyin on each input and hint for the game to actually educated the person.







# 斗地主


## Introduction
As I fully understand how to code the margin and syntax for HTML, I wanted some challenge, so I decided to create a game with AI about the traditional Chinese Poker game called, "斗地主“.

This game is a really complicated game involving 50+ rules and diverse ways to play the cards. I have attached the rule set to the game in the button where it says rules. I have also attached it to the original primary source. Just translate the rules to English in your own browser. 

[Rules](https://baike.baidu.com/item/欢乐斗地主/2754884)











# Sources
https://baike.baidu.com/item/欢乐斗地主/2754884








