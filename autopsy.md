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
