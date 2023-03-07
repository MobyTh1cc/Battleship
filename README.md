# Battleship
battleship game in ejs
the page localhost:1234 is for player 1 & page localhost:1234/p2 is for player 2
functions in ejs:
* ```function start()``` is being called when the player presses on the rady button. if the player didnt put 5 ships on the board he'll get a pop up warning him that he didnt put 5 ships, else the game will mark that he start and wait for the other player if the other player didnt press the ready button.
* ```function rotate()`` is being called when the player presses the rotate button. when its called its rotates the ship 90 degrees.
* ```function hit(c)``` when a player lands a hit the function being called coloring the cell in red
* ```function miss(c)``` when a player miss a ship the function being called coloring the cell in light grey
* ```async function change(cell)``` being called when a player presses on a cell. if the game didnt start it will put the ship on the board. else, it will check if the player hit the enemy ship or miss it.
* ```async function getTurn()``` is a function that checking if the game ended and if so ends it and show the number of the player that won. also the function says which player's turn it is and the massege that tell the player that the other player isnt ready.
* ```setInterval(getTurn,500)``` calls the function getTurn() every 0.5 seconds

js file:
* var board1 is the board of player 1
* var board2 is the board of player 2
* lastMove is an object that is being send to the player as an answer. if the move is legal it will return the cell that the player clicked, else it will return -1.
* ```router.get('/GetMove1/:c/:s/:r', function(req,res)``` gets the cell the player clicked on, the size of the ship and the way he want to place it, meaning 0 is horizontal and 1 is vertical, and acordint to that it changes the boards. in addition it checking if the move is legal if so it puts it on the board is not it send to the player -1 using lastMove.
* ```router.get('/sendMove1/:c', function(req,res){})``` is a function that used when the game starts and player 1 presses on a cell. if he hits a cell the server return him the object lastMove with last = 1 and cell = 1 (which means that the next turn is for player 1 and that he got a hit = 1). if the player misses the server return him the object lastMove with last = 2 and cell = -1 (which means that the next turn is for player 2 and that he got a hit = -1). it checking in board2 if its 1 (there is a ship) or 0 (there is no ship).
* ```router.get('/p1Ready', function(req,res){})``` set that player 1 is ready
* ```function checkBoard1()``` return 1 if the board1 has a ship and 0 if doesnt
* ```router.get('/GetMove2/:c/:s/:r', function(req,res){``` same as for player 1 but for player 2 and board2
* ```router.get('/sendMove2/:c', function(req,res){})``` same as for player 1 but for player 2 and board1
* ```router.get('/p2Ready', function(req,res){})``` set that player 2 is ready
* ```function checkBoard2()``` return 1 if the board2 has a ship and 0 if doesnt
* turn is the object returned to the function getTurn() is the ejs is consist of which player is ready, who went last and if the game is on.
* ```router.get('/whoTurn', function(req,res){})``` checking if the game has ended or not
