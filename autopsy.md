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
  


