[gemini-code-1792434266941.js](https://github.com/user-attachments/files/33679292/gemini-code-1792434266941.js)[gemini-code-1792434243177.js](https://github.com/user-attachments/files/33679279/gemini-code-1792434243177.js)[gemini-code-1792434088650.html](https://github.com/user-attachments/files/33679205/gemini-code-1792434088650.html)# Tic Tac Toe

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
[Game](https://share.gemini.google/F01ssh6HYkqe)

## Introduction

As I fully understand how to code the margin and syntax for HTML, I wanted some challenge, so I decided to create a game with AI about the traditional Chinese Poker game called, "斗地主“.

This game is a really complicated game involving 50+ rules and diverse ways to play the cards. I have attached the rule set to the game in the button where it says rules. I have also attached it to the original primary source. Just translate the rules to English in your own browser. 

[Rules](https://baike.baidu.com/item/欢乐斗地主/2754884)



## AI usage
AI helped me code everything for my project. I was able to do a few tweaks with AI, adding a bit of delay time for each person to play their cards. This makes the game more realistic and gives time for the player to realize what is happening. Additionally, I also edited the AI's background color for my game. Initially it was just blue and had no background. I changed the RGB color of the blue to green so the cards stand out a little bit more. 


Some prompts that I gave AI was, "Could you help me code a game with the ruleset attached in the hyperlink". And Gemini would help me code and display the game into HTML. 

## Motivations

1. I created this game partly because during the Tic Tac Toe game, the AI really helped me understand the CSS and Javascript embedded in the code, so I wanted to use those again for my new game.

2. Neither game uses a Canvas element (<canvas>) or continuous game loop (requestAnimationFrame). Instead, both rely entirely on event listeners (mouse clicks/taps) to trigger game state updates and re-renders.

3. Both games keep track of their game state in JavaScript memory using standard arrays and variables (e.g., array tracking positions vs. array tracking card hands). This makes the game flow smoother and allow the code to be simpler with more variations such as adding more elements and ways to play the cards.

### Differences and Innovations

<img width="554" height="575" alt="image" src="https://github.com/user-attachments/assets/4c60bf8b-e3dd-4766-8f1e-3bbec4f3785f" />



## Documentation


### Day one and two

Day one was simple, I created the code using AI and was playing around with the game. First, AI gave me a boring game just with cards and no background color nor designs. 

<img width="525" height="366" alt="image" src="https://github.com/user-attachments/assets/5ba0be6a-c7bb-4e64-a42c-c62998c22ce5" />

I figured that this was really boring and I could add a background color to mimic the real life experience of playing those cards. Furthermore, there was only simplified Chinese, since I wanted to make this game educations, I asked AI if it could help me add some colors and also include Pinyin for everything. 


Then, I changed the color of the background HUD from Blue to green using the RGB color and also asking AI to help me locate the code where I could do it. What I learned from AI was that there are specific places in HTML to help me change the margin and format of the website. 






Day Two was different, I found some bugs inside my "how to play" page had nothing inside of it. Thus I went on the actual website of the game and copied and user manual into AI to help me add the HOW TO PLAY instructions. 

<img width="701" height="521" alt="image" src="https://github.com/user-attachments/assets/5973f00f-c6fc-4d9e-b0cc-6484bda2a168" />




I also felt that in order for beginners to quickly understand the game, I had to make the instructions more clearer and add a hint section so whenever the player is lost, it could rely on the hint. 

<img width="1171" height="548" alt="image" src="https://github.com/user-attachments/assets/cdeaa535-933b-4f01-ab87-5c5b0804f5f9" />


The hint would first highlight the cards that it thinks that we should play and explain the reasoning. This was extremely helpful for the people I found that had basically no experience such as Dr. Dzula. Sometimes, he would allow hint to help him learn this game. 


In the meantime, AI also has helped me add the how to play section on the right top of the game and included the full depth description of it.
<img width="482" height="374" alt="image" src="https://github.com/user-attachments/assets/19108f42-6e45-4132-811c-fc98ca0b4d73" />


Day three was working on this documentation and adding all the Pinyins onto the game's GUI. I asked AI to help me add them before making it list out everything and me checking for it. Although, it made like 1-2 translation errors, it was overall amazing and really good. I would then correct it's mistakes and tell it to add it to the code. During day 3, I also asked for feedback from the people who played this game. I have listed out the feedbacks they gave below this section. 


## Different experiences while playing the game

### Beginners

I found 1-2 beginners playing my game and one being Dr. Dzula. Although I gave some tips to Dr. Dzula, he won a game without me explaining. I found out the the hint was really helpful for new players and it was a great implementation.


### Advanced

I also found some players whose been playing this game for a long time such as Matthew Ma and John Deng. They both really liked the game and gave me some tips such as "Add a 1 second delay so the player can tell who is playing next" or "Make the cards pop out when selected so I know what cards I selected". These were all amazing feedbacks for me and I changed my game accordingly. 




## Things I learned

1. **State Management:** How a turn-based game tracks phases (BIDDING, PLAYING, GAME_OVER), player hands, and table trick history.
    
2. **Turn Logic & Delays:** How using timer functions (setTimeout) creates human-like thinking delays for AI opponents so the game flow is easy to follow.

3. **Card Counting (记牌器)**: Tracking key remaining high cards ($2$, $A$, and Jokers) to calculate tactical risks during play.
   

4.**JavaScript Game Logic & Engine Design** Array Shuffling (Fisher-Yates Algorithm): A standard method for shuffling array elements to ensure fair, randomized card distribution each round.

function shuffleDeck(deck) {
  let shuffled = [...deck];
  for (let i = shuffled.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]]; // Swap elements
  }
  return shuffled;
}


5. **State Management (gameState)**: A centralized object tracking player hands, whose turn it is (currentTurn), active multipliers, and current table state.

gameState = {
  phase: 'BIDDING', // Tracks state: 'BIDDING', 'PLAYING', 'GAME_OVER'
  deck: [],
  holeCards: [],
  players: [
    { id: 0, name: 'You (South)', cards: [], role: 'PEASANT', bid: 0, playsCount: 0 },
    { id: 1, name: 'AI West', cards: [], role: 'PEASANT', bid: 0, playsCount: 0 },
    { id: 2, name: 'AI East', cards: [], role: 'PEASANT', bid: 0, playsCount: 0 }
  ],
  landlordId: -1,
  currentTurn: 0,
  highestBid: 0,
  highestBidder: -1,
  lastTrick: null,
  passCount: 0,
  baseScore: 15,
  multiplier: 1,
  selectedCards: new Set(),
  aiThinkingTimeout: null
};ading gemini-code-1792434243177.js…]()

  
7. Turn Phase Machine: Dividing the game into distinct sequential phases: BIDDING PLAYING GAME_OVER.

function processTurn() {
  updateUI();

  if (gameState.phase === 'BIDDING') {
    processBiddingStep();
  } else if (gameState.phase === 'DOUBLING') {
    processDoublingStep();
  } else if (gameState.phase === 'PLAYING') {
    processPlayStep();
  } else if (gameState.phase === 'GAME_OVER') {
    // End game resolution
  }
}


9. AI Thinking Delay (setTimeout): Using timer delays to pause AI actions for 3–5 seconds, giving you time to read the board.

function triggerAIThinking(aiId, thoughtMsg, callback) {
  const thoughtElem = document.getElementById(`thought-${aiId}`);
  const reasoningElem = document.getElementById(`reasoning-${aiId}`);
  
  if (thoughtElem && reasoningElem) {
    reasoningElem.innerText = thoughtMsg;
    thoughtElem.classList.remove('hidden'); // Show thinking bubble
  }

  // Generate a randomized delay between 3000ms (3s) and 5000ms (5s)
  const delayMs = Math.floor(Math.random() * 2000) + 3000;

  gameState.aiThinkingTimeout = setTimeout(() => {
    if (thoughtElem) thoughtElem.classList.add('hidden'); // Hide bubble
    playSound('turn');
    callback(); // Execute the AI decision after delay
  }, delayMs);
}



## Final Code
[U<!DOCTYPE html>
<html lang="zh-CN" class="h-full">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>斗地主 Fight the Landlord (Dòu Dìzhǔ)</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap');
    body { font-family: 'Inter', system-ui, -apple-system, sans-serif; user-select: none; }
    .card-item { transition: transform 0.18s cubic-bezier(0.34, 1.56, 0.64, 1), box-shadow 0.18s ease; }
    .card-item.selected { transform: translateY(-26px) scale(1.03); box-shadow: 0 14px 22px -4px rgba(0, 0, 0, 0.6), 0 0 0 2px #f59e0b; }
    @keyframes avatarGlow {
      0%, 100% { box-shadow: 0 0 18px rgba(245, 158, 11, 0.85), 0 0 0 3px #f59e0b; }
      50% { box-shadow: 0 0 28px rgba(245, 158, 11, 1), 0 0 0 4px #fbbf24; }
    }
    .active-turn-avatar { animation: avatarGlow 1.5s infinite ease-in-out; }
    .dot-flashing {
      display: inline-block; width: 6px; height: 6px; border-radius: 5px;
      background-color: #f59e0b; color: #f59e0b; animation: dot-flashing 1s infinite alternate; animation-delay: 0.5s;
    }
    @keyframes dot-flashing { 0% { background-color: #f59e0b; } 50%, 100% { background-color: rgba(245, 158, 11, 0.2); } }
  </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen flex flex-col justify-between overflow-x-hidden">

  <!-- TOP BAR & CARD TRACKER -->
  <header class="bg-slate-900 border-b border-slate-800 px-4 py-2 flex flex-wrap items-center justify-between gap-2 shadow-lg">
    <div class="flex items-center space-x-3">
      <div class="bg-amber-500 text-slate-950 font-black text-lg px-2.5 py-1 rounded shadow">🃏 斗地主</div>
      <span class="text-xs sm:text-sm text-slate-400 font-medium">Fight the Landlord (Dòu Dìzhǔ)</span>
    </div>

    <!-- Live Card Tracker -->
    <div class="flex items-center bg-slate-950 px-3 py-1.5 rounded-lg border border-slate-800 text-xs gap-3 font-mono">
      <span class="text-slate-400 font-sans hidden sm:inline">📊 记牌器 Card Tracker:</span>
      <div><span class="text-red-500 font-bold">大王 Red Joker:</span> <span id="track-bj" class="text-amber-400 font-bold">1</span></div>
      <div><span class="text-slate-300 font-bold">小王 Blk Joker:</span> <span id="track-sj" class="text-amber-400 font-bold">1</span></div>
      <div><span class="text-amber-400 font-bold">2s:</span> <span id="track-2" class="text-amber-400 font-bold">4</span></div>
      <div><span class="text-slate-200 font-bold">As:</span> <span id="track-a" class="text-amber-400 font-bold">4</span></div>
    </div>

    <div class="flex items-center space-x-2">
      <button onclick="restartGame()" class="px-3 py-1.5 rounded bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold text-xs shadow transition">
        🔄 新游戏 New Game
      </button>
    </div>
  </header>

  <!-- MAIN PLAY AREA -->
  <main class="flex-1 max-w-7xl w-full mx-auto p-3 flex flex-col justify-between gap-2">
    
    <!-- HOLE CARDS & SCORES -->
    <section class="flex items-center justify-between bg-slate-900/60 p-2.5 rounded-xl border border-slate-800/80">
      <div class="flex items-center gap-2">
        <span class="text-xs font-bold text-amber-400">底牌 Dǐpái (Hole Cards):</span>
        <div id="hole-cards-container" class="flex gap-1.5"></div>
      </div>
      <div class="flex items-center gap-4 bg-slate-950 px-4 py-1.5 rounded-lg border border-slate-800 text-xs font-mono">
        <div><span class="text-slate-400">底分 Base:</span> <span class="text-amber-400 font-bold ml-1" id="base-score-val">15</span></div>
        <div><span class="text-slate-400">倍数 Multipliers:</span> <span class="text-emerald-400 font-bold ml-1" id="multiplier-val">x1</span></div>
        <div><span class="text-slate-400">阶段 Phase:</span> <span class="text-sky-400 font-bold ml-1" id="game-phase-label">叫牌 Bidding</span></div>
      </div>
    </section>

    <!-- THREE PLAYERS LAYOUT -->
    <section class="grid grid-cols-12 gap-2 my-auto items-stretch min-h-[360px]">
      
      <!-- LEFT AI WEST -->
      <div id="player-container-1" class="col-span-3 bg-slate-900/50 rounded-2xl border border-slate-800 p-3 flex flex-col justify-between relative">
        <div class="flex flex-col items-center text-center gap-1">
          <div id="avatar-1" class="w-14 h-14 rounded-full bg-slate-800 border-2 border-slate-700 flex items-center justify-center text-2xl relative shadow">🤖</div>
          <div class="font-bold text-xs text-slate-200">AI 玩家 1 (West)</div>
          <div id="card-count-1" class="text-xs text-amber-400 font-mono font-semibold">17 Cards</div>
        </div>

        <div id="thought-1" class="my-2 bg-slate-950 border border-amber-500/30 rounded-xl p-2 text-center hidden shadow-lg">
          <div class="text-[11px] text-amber-400 font-medium">🤔 思考中 Thinking... (3-5s)</div>
          <div class="text-[10px] text-slate-400 mt-0.5 font-mono"><span class="dot-flashing"></span> <span id="reasoning-1">Evaluating deck...</span></div>
        </div>

        <div class="min-h-[80px] flex items-center justify-center flex-wrap gap-1" id="played-1"></div>
      </div>

      <!-- CENTER TABLE -->
      <div class="col-span-6 bg-slate-900/30 rounded-2xl border border-slate-800/50 p-4 flex flex-col items-center justify-between">
        <div id="table-status-banner" class="w-full text-center py-1.5 px-3 rounded-lg bg-amber-500/10 border border-amber-500/20 text-amber-300 text-xs font-semibold">
          🎯 <span id="table-status-text">请出牌或叫分 Please bid or play cards</span>
        </div>

        <div class="my-auto w-full flex flex-col items-center justify-center py-2">
          <div class="text-[11px] text-slate-400 mb-1 font-medium" id="current-trick-owner">当前牌面 Current Trick</div>
          <div id="center-trick-cards" class="flex flex-wrap items-center justify-center gap-2 min-h-[90px]">
            <span class="text-xs text-slate-500 italic">等待出牌 Waiting for plays...</span>
          </div>
        </div>

        <div class="w-full bg-slate-950/70 border border-slate-800 rounded-lg p-2 text-center text-xs">
          <div class="text-amber-400 font-bold mb-0.5">💡 战术提示 Strategy Hint:</div>
          <div id="live-hint-text" class="text-slate-300 font-mono text-[11px]">叫牌阶段：手牌有大王、2或炸弹时建议叫3分地主。</div>
        </div>
      </div>

      <!-- RIGHT AI EAST -->
      <div id="player-container-2" class="col-span-3 bg-slate-900/50 rounded-2xl border border-slate-800 p-3 flex flex-col justify-between relative">
        <div class="flex flex-col items-center text-center gap-1">
          <div id="avatar-2" class="w-14 h-14 rounded-full bg-slate-800 border-2 border-slate-700 flex items-center justify-center text-2xl relative shadow">🤖</div>
          <div class="font-bold text-xs text-slate-200">AI 玩家 2 (East)</div>
          <div id="card-count-2" class="text-xs text-amber-400 font-mono font-semibold">17 Cards</div>
        </div>

        <div id="thought-2" class="my-2 bg-slate-950 border border-amber-500/30 rounded-xl p-2 text-center hidden shadow-lg">
          <div class="text-[11px] text-amber-400 font-medium">🤔 思考中 Thinking... (3-5s)</div>
          <div class="text-[10px] text-slate-400 mt-0.5 font-mono"><span class="dot-flashing"></span> <span id="reasoning-2">Calculating...</span></div>
        </div>

        <div class="min-h-[80px] flex items-center justify-center flex-wrap gap-1" id="played-2"></div>
      </div>

    </section>

    <!-- HUMAN PLAYER BOTTOM AREA -->
    <section id="player-container-0" class="bg-slate-900/80 border border-slate-800 rounded-2xl p-3 flex flex-col items-center gap-3">
      <div id="action-controls-bar" class="flex flex-wrap items-center justify-center gap-2 min-h-[44px]"></div>

      <div class="w-full flex flex-col items-center">
        <div class="flex items-center gap-3 mb-2">
          <div id="avatar-0" class="w-8 h-8 rounded-full bg-amber-500 text-slate-950 font-bold flex items-center justify-center text-sm">👤</div>
          <span class="font-bold text-sm text-slate-100">你 You (South)</span>
          <span id="role-badge-0" class="text-xs px-2 py-0.5 rounded-full bg-slate-800 border border-slate-700 font-semibold text-amber-400">农民 Peasant</span>
        </div>

        <div id="human-hand-container" class="flex justify-center items-end py-2 px-4 overflow-x-auto max-w-full min-h-[140px] select-none"></div>
      </div>
    </section>

  </main>

  <!-- JAVASCRIPT GAME ENGINE -->
  <script>
    const SUITS = [
      { symbol: '♠', color: 'text-slate-200' },
      { symbol: '♥', color: 'text-red-500' },
      { symbol: '♣', color: 'text-slate-200' },
      { symbol: '♦', color: 'text-red-500' }
    ];

    const RANKS = [
      { value: 3, label: '3' }, { value: 4, label: '4' }, { value: 5, label: '5' },
      { value: 6, label: '6' }, { value: 7, label: '7' }, { value: 8, label: '8' },
      { value: 9, label: '9' }, { value: 10, label: '10' }, { value: 11, label: 'J' },
      { value: 12, label: 'Q' }, { value: 13, label: 'K' }, { value: 14, label: 'A' }, { value: 15, label: '2' }
    ];

    let gameState = {
      phase: 'BIDDING', deck: [], holeCards: [],
      players: [
        { id: 0, name: 'You (South)', cards: [], role: 'PEASANT', bid: 0, playsCount: 0 },
        { id: 1, name: 'AI West', cards: [], role: 'PEASANT', bid: 0, playsCount: 0 },
        { id: 2, name: 'AI East', cards: [], role: 'PEASANT', bid: 0, playsCount: 0 }
      ],
      landlordId: -1, currentTurn: 0, highestBid: 0, highestBidder: -1,
      lastTrick: null, passCount: 0, baseScore: 15, multiplier: 1,
      selectedCards: new Set(), aiThinkingTimeout: null
    };

    function create54Deck() {
      let deck = [], cardId = 0;
      for (const rank of RANKS) {
        for (const suit of SUITS) {
          deck.push({ id: cardId++, value: rank.value, label: rank.label, suit: suit.symbol, color: suit.color });
        }
      }
      deck.push({ id: cardId++, value: 16, label: '小王', suit: '🃏', color: 'text-slate-300' });
      deck.push({ id: cardId++, value: 17, label: '大王', suit: '🃏', color: 'text-red-500' });
      return deck;
    }

    function shuffleDeck(deck) {
      let shuffled = [...deck];
      for (let i = shuffled.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
      }
      return shuffled;
    }

    function sortHand(cards) {
      return cards.sort((a, b) => (b.value !== a.value ? b.value - a.value : a.id - b.id));
    }

    function restartGame() {
      if (gameState.aiThinkingTimeout) clearTimeout(gameState.aiThinkingTimeout);
      const deck = shuffleDeck(create54Deck());
      
      gameState.players[0].cards = sortHand(deck.slice(0, 17));
      gameState.players[1].cards = sortHand(deck.slice(17, 34));
      gameState.players[2].cards = sortHand(deck.slice(34, 51));
      gameState.holeCards = deck.slice(51, 54);

      gameState.players.forEach(p => { p.role = 'PEASANT'; p.bid = 0; p.playsCount = 0; });
      gameState.phase = 'BIDDING'; gameState.landlordId = -1; gameState.currentTurn = Math.floor(Math.random() * 3);
      gameState.highestBid = 0; gameState.highestBidder = -1; gameState.lastTrick = null; gameState.passCount = 0;
      gameState.baseScore = 15; gameState.multiplier = 1; gameState.selectedCards.clear();

      document.getElementById('played-1').innerHTML = '';
      document.getElementById('played-2').innerHTML = '';
      document.getElementById('thought-1').classList.add('hidden');
      document.getElementById('thought-2').classList.add('hidden');

      updateUI();
      processTurn();
    }

    function processTurn() {
      updateUI();
      if (gameState.phase === 'BIDDING') {
        const bidsCount = gameState.players.filter(p => p.bid > 0 || p.bid === -1).length;
        if (gameState.highestBid === 3 || bidsCount === 3) {
          if (gameState.highestBidder !== -1) finalizeLandlord(gameState.highestBidder);
          else restartGame();
          return;
        }

        const activeP = gameState.players[gameState.currentTurn];
        if (activeP.id === 0) updateHint('你的叫牌回合！选择 1分、2分、3分 或 不叫。');
        else triggerAIThinking(activeP.id, '评估叫牌中...', () => makeBid(activeP.id, Math.floor(Math.random() * 2)));

      } else if (gameState.phase === 'PLAYING') {
        if (gameState.passCount >= 2) { gameState.lastTrick = null; gameState.passCount = 0; }
        const activeP = gameState.players[gameState.currentTurn];

        if (activeP.id === 0) {
          updateHint(!gameState.lastTrick || gameState.lastTrick.playerId === 0 ? '👑 自由出牌 Lead Control!' : '轮到你跟牌！');
        } else {
          triggerAIThinking(activeP.id, '寻找最佳牌型...', () => {
            const cards = activeP.cards;
            if (!gameState.lastTrick || gameState.lastTrick.playerId === activeP.id) {
              playCardsAction(activeP.id, [cards[cards.length - 1]]);
            } else {
              const higher = cards.filter(c => c.value > gameState.lastTrick.cards[0].value);
              if (higher.length > 0 && gameState.lastTrick.cards.length === 1) playCardsAction(activeP.id, [higher[higher.length - 1]]);
              else passCardsAction(activeP.id);
            }
          });
        }
      }
    }

    function triggerAIThinking(aiId, thoughtMsg, callback) {
      document.getElementById(`reasoning-${aiId}`).innerText = thoughtMsg;
      document.getElementById(`thought-${aiId}`).classList.remove('hidden');

      gameState.aiThinkingTimeout = setTimeout(() => {
        document.getElementById(`thought-${aiId}`).classList.add('hidden');
        callback();
      }, Math.floor(Math.random() * 2000) + 3000);
    }

    function makeBid(playerId, bid) {
      const p = gameState.players[playerId];
      p.bid = bid > 0 ? bid : -1;
      if (bid > gameState.highestBid) { gameState.highestBid = bid; gameState.highestBidder = playerId; }
      gameState.currentTurn = (gameState.currentTurn + 1) % 3;
      processTurn();
    }

    function finalizeLandlord(landlordId) {
      gameState.landlordId = landlordId;
      gameState.phase = 'PLAYING';
      const landlord = gameState.players[landlordId];
      landlord.role = 'LANDLORD';
      landlord.cards = sortHand([...landlord.cards, ...gameState.holeCards]);
      gameState.currentTurn = landlordId;
      processTurn();
    }

    function playCardsAction(playerId, cards) {
      const p = gameState.players[playerId];
      p.cards = p.cards.filter(c => !cards.some(sc => sc.id === c.id));
      gameState.lastTrick = { playerId, cards };
      gameState.passCount = 0;

      if (playerId > 0) renderPlayedCards(`played-${playerId}`, cards);
      if (p.cards.length === 0) { updateHint(`🏆 ${p.name} 获胜！ Win!`); gameState.phase = 'GAME_OVER'; updateUI(); return; }

      gameState.currentTurn = (gameState.currentTurn + 1) % 3;
      processTurn();
    }

    function passCardsAction(playerId) {
      gameState.passCount++;
      if (playerId > 0) document.getElementById(`played-${playerId}`).innerHTML = `<span class="text-xs font-bold text-slate-500 italic">不要 Pass</span>`;
      gameState.currentTurn = (gameState.currentTurn + 1) % 3;
      processTurn();
    }

    function updateUI() {
      const hole = document.getElementById('hole-cards-container');
      hole.innerHTML = '';
      gameState.holeCards.forEach(c => {
        const show = gameState.phase !== 'BIDDING';
        hole.innerHTML += `<div class="w-8 h-11 rounded border flex flex-col items-center justify-center font-bold text-xs ${show ? 'bg-slate-100 text-slate-900' : 'bg-amber-600/30 text-amber-400'}">${show ? c.label : '🂠'}</div>`;
      });

      gameState.players.forEach(p => {
        document.getElementById(`card-count-${p.id}`).innerText = `${p.cards.length} Cards`;
        const avatar = document.getElementById(`avatar-${p.id}`);
        if (gameState.currentTurn === p.id && gameState.phase !== 'GAME_OVER') avatar?.classList.add('active-turn-avatar');
        else avatar?.classList.remove('active-turn-avatar');
      });

      if (gameState.lastTrick && gameState.lastTrick.cards.length > 0) {
        renderPlayedCards('center-trick-cards', gameState.lastTrick.cards);
      } else {
        document.getElementById('center-trick-cards').innerHTML = `<span class="text-xs text-slate-500 italic">等待出牌 Waiting...</span>`;
      }

      renderHumanControls();
      renderHumanHand();
    }

    function renderPlayedCards(id, cards) {
      const c = document.getElementById(id);
      c.innerHTML = '';
      cards.forEach(card => {
        c.innerHTML += `<div class="w-9 h-12 bg-slate-100 text-slate-900 rounded border p-1 font-bold text-xs flex flex-col justify-between"><div>${card.label}</div><div class="${card.color}">${card.suit}</div></div>`;
      });
    }

    function renderHumanHand() {
      const container = document.getElementById('human-hand-container');
      container.innerHTML = '';
      gameState.players[0].cards.forEach(card => {
        const selected = gameState.selectedCards.has(card.id);
        const el = document.createElement('div');
        el.className = `card-item w-12 h-18 bg-slate-100 text-slate-900 rounded-lg border p-1.5 shadow cursor-pointer -ml-4 first:ml-0 ${selected ? 'selected' : ''}`;
        el.onclick = () => {
          if (gameState.selectedCards.has(card.id)) gameState.selectedCards.delete(card.id);
          else gameState.selectedCards.add(card.id);
          renderHumanHand();
        };
        el.innerHTML = `<div class="font-bold text-sm">${card.label}</div><div class="${card.color} text-xl">${card.suit}</div>`;
        container.appendChild(el);
      });
    }

    function renderHumanControls() {
      const bar = document.getElementById('action-controls-bar');
      bar.innerHTML = '';
      if (gameState.phase === 'BIDDING' && gameState.currentTurn === 0) {
        [0, 1, 2, 3].forEach(b => {
          if (b > 0 && b <= gameState.highestBid) return;
          const btn = document.createElement('button');
          btn.className = 'px-3 py-1.5 rounded bg-amber-500 text-slate-950 font-bold text-xs';
          btn.innerText = b === 0 ? '不叫 Pass' : `叫 ${b} 分`;
          btn.onclick = () => makeBid(0, b);
          bar.appendChild(btn);
        });
      } else if (gameState.phase === 'PLAYING' && gameState.currentTurn === 0) {
        if (gameState.lastTrick && gameState.lastTrick.playerId !== 0) {
          const passBtn = document.createElement('button');
          passBtn.className = 'px-4 py-1.5 rounded bg-slate-800 text-slate-200 text-xs font-bold';
          passBtn.innerText = '不要 Pass';
          passBtn.onclick = () => passCardsAction(0);
          bar.appendChild(passBtn);
        }

        const playBtn = document.createElement('button');
        playBtn.className = 'px-5 py-1.5 rounded bg-amber-500 text-slate-950 text-xs font-black';
        playBtn.innerText = '出牌 Play';
        playBtn.onclick = () => {
          const selectedList = gameState.players[0].cards.filter(c => gameState.selectedCards.has(c.id));
          if (selectedList.length === 0) return;
          gameState.selectedCards.clear();
          playCardsAction(0, selectedList);
        };
        bar.appendChild(playBtn);
      }
    }

    function updateHint(msg) {
      document.getElementById('live-hint-text').innerText = msg;
      document.getElementById('table-status-text').innerText = msg;
    }

    window.onload = restartGame;
  </script>
</body>
</html>ploading gemini-code-1792434088650.html…]()





## Future coding


### **I would include these main ones in my future website development:**



1. Organizing Your Game Data (gameState)
Think of gameState like a scoreboard and game log rolled into one.

In programming, instead of having dozens of separate variables scattered everywhere, you group them inside one big object. This makes it super easy to check what's happening at any moment.


// A simple object holding all the current game info
let gameState = {
  phase: 'BIDDING',  // What part of the game are we in? ('BIDDING', 'PLAYING', 'GAME_OVER')
  currentTurn: 0,    // Whose turn is it? (0 = You, 1 = AI West, 2 = AI East)
  multiplier: 1,     // Current point multiplier
  cardsLeft: 17      // How many cards are left
};




2. Shuffling Cards Fairly (Fisher-Yates Shuffle)
If you shuffle cards in real life, you want them mixed up completely randomly. In code, a simple loop swaps every card in the deck with another random card.

function shuffleDeck(deck) {
  // Loop backwards through the deck
  for (let i = deck.length - 1; i > 0; i--) {
    // Pick a random card position before the current one
    let randomIndex = Math.floor(Math.random() * (i + 1));

    // Swap the current card with the random card
    let temp = deck[i];
    deck[i] = deck[randomIndex];
    deck[randomIndex] = temp;
  }
  return deck;
}



3. Controlling Game Steps (Game Phases)A game moves in order: Start $\rightarrow$ Bid $\rightarrow$ Play Cards $\rightarrow$ Game Over.Instead of letting players do whatever they want whenever they want, an if statement checks what phase the game is currently in before allowing actions.

function processTurn() {
  if (gameState.phase === 'BIDDING') {
    // Only show bidding buttons (1 Point, 2 Points, Pass)
    showBiddingControls();
  } else if (gameState.phase === 'PLAYING') {
    // Only allow playing cards or passing
    showPlayCardControls();
  } else if (gameState.phase === 'GAME_OVER') {
    // Show winner message
    showWinnerScreen();
  }
}


4. Making the AI "Think" (setTimeout)
Computers make calculations in milliseconds. If an AI player played its card instantly, the game would move too fast for a human to follow!

We use setTimeout to create a fake 3 to 5 second timer so it feels like the computer is actually thinking.


function aiTurn() {
  // Pick a random delay time between 3000ms (3 seconds) and 5000ms (5 seconds)
  let thinkTime = Math.floor(Math.random() * 2000) + 3000;

  console.log("AI is thinking...");

  // Wait for the timer to finish, then execute the AI move
  setTimeout(function() {
    console.log("AI played a card!");
    makeAIMove();
  }, thinkTime);
}


# Sources
https://baike.baidu.com/item/欢乐斗地主/2754884








