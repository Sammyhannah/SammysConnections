# Sammy's Connections
## Video Demo:  <URL HERE>
## Description: My re-creation of the classic New York Times Game "Connections."

### Why I chose this project

> [Main Points] My re-creation of Connections allows the user to play multiple games in day and keep playing even if they lose. It also allows allows me to create my own word categories!

My project, Sammy's Connections, is my re-creation of the classic New York Times Game "Connections."

I decided to attempt this project because though I love the New York Times version, it only allows the user to play one game per day. This can be frustrating to the user in several cases. When the game is too easy, the user will complete the game quickly and want to play again, but will then have to wait a full day for the next game. When the game is too challenging, the user may not find the solution within the allotted number of mistakes allowed, which will end the game. They will not only have to wait another day to play again, but will also be shown all the answers to the current game and won't be allowed to try again.


Sammy's Connections solves this probleming by both allowing users to play multiple different games in a row, and entering a free play game mode when the user loses the game, in which they can keep trying to find the correct solutions with an infinite number of mistakes allowed.


Another reason I attempted this project was because I recently found myself coming up with my own ideas for connection puzzles and wanted to share them!


### How the Gameplay works

> [Main Points] In a 16-word grid, players must find four groups of four words that share commanilities, without making four mistakes.

The object of the game is to find commonalities between words in a 16-word grid. Players can win the game by correctly grouping four groups of four words without making more than four incorrect guesses.If four mistakes are made before the 16 words are grouped, players enter Free Play mode in which they can continue attempting to find the correct groupings for fun.

Players can select up to 4 buttons at a time by clicking on them. To deselect buttons, players can click on a selected button, or can use the Deselect All button to deselect all currently selected buttons. To get a different perspective, players can shuffle all the buttons in the grid by pressing the Shuffle button, which will also unselect any currently selected buttons. Once players think they know a correct grouping, they can submit exactly 4 selected buttons as a guess. Players can reload or refresh the page to start a new randomly selected game with a new grid of words.


### My game.html File

> [Main Points] In this file, I establish my layout, and then continue into Javascript to create functions that make the gameplay work.


My HTML file starts with establishing my layout, which consists of a header, instructions, word grid, mistake count, and game buttons, as well as hidden solutions that are made visible when the player correctly submits a guess. The header establishes the title of the game, and the instructions tell the player how to play. The word grid, mistake count, and game buttons are a part of the gameplay.


Continuing into Javascript, I establish a variable for my data that holds arrays for each game and their respective solutions. These solutions include four groups of four related words, each group being a correct solution with its own category. The category for each group includes the title of the category (for example, "Articles of Clothing"), and the level of difficulty.


#### Start Game Function / Shuffle Array Function

> [Main Points]
These Functions work together to set up the game initially (on a page load or refresh) by randomly selecting a game and assigning words to the 16-word grid. They are also called when the "shuffle" button is clicked during gameplay to shuffle the word grid so the player can see a different perspective.


On page load, I first initialize a variable to say that no Random Game is chosen yet. I then call a `Start Game Function` that starts the game. In this Function, a variable for the current game is set. If the game is not started yet (which will happen on page load or refresh) the Function will select a random game from my array of games and set it as the current game. If the game is started (this will be used later in the case of this Function being called by the player clicking the "shuffle" button), the randomly selected game that the player is in will be set as the current game. Next, the Function will make an array of all the words in the current game, and then pass this array of words to the `Shuffle Array Function.`


The `Shuffle Array Function` takes in the array of words from the current game, excluding any deleted buttons (which will matter later in the game when buttons are deleted as correct groupings are found). The Function shuffles the array by iterating over the array, picking a random button, and swapping it with the current button. It passes back the shuffled buttons to the `Start Game Function.`


The `Start Game Function takes` the shuffled buttons loops through them, assigning the text content of each to a word button (which are the individual buttons in the word grid that the player sees).


#### Event Listener on the Shuffle Button / Shuffle Function


> [Main Points] When the Shuffle Button is clicked during gameplay, the Shuffle Function calls to the Start Game Function and Shuffle Array Function to shuffle the word grid so the player can see a different perspective, passing the information that the game is already started so a new game doesn't get selected.


The Shuffle Button has an `event listener` that listens for a click. When the Shuffle Button is clicked by a player, the `event listener` takes all the word buttons and passes them to the `Shuffle Function.`


The `Shuffle Function` then tells the `Start Game Function` that the game has already been started so it will only shuffle the words in the current game instead of randomly selecting a new game and shuffling those words like we did for the setup.


The `Start Game Function` calls to the `Shuffle Array Function,` like it does during the game setup, to shuffle the word grid so the player can see the words in a different arrangement which may help them find the correct groupings.




#### Event Listener on Word Buttons / Select Function


> [Main Points] When a Word Button is clicked during gameplay, the word button that was clicked is passed to the Select Function, which either selects or deselects the word button depending on its current state.


In the gameplay, players can select four words at a time, which they can then submit as a guess. To keep track of this, I initialize a variable for the number of word buttons currently selected, and initialize all word buttons with a data set that says they are unselected.


The `Select Function` is called when a word button is clicked, and it takes in the specific word button that was clicked (passed from an event listener listening for the click).


If the word button that was clicked and passed to the Function has a selected status of unselected, and the number of word buttons currently selected is not yet four, the word button proceeds to be selected. Being selected entails changing the word button's status to selected, class to selected (which is defined in styles.ss to add a darker color), and adding a tally to the number of word buttons currently selected.


If the word button that was clicked and passed to the Function has a selected status, the word button proceeds to be unselected (for the player this is helpful because if they want to deselect a button they simply have to click it again). Being deselected entails changing the word button's status to deselected, class to desselected (the normal color), and subtracting a tally from the number of word buttons currently selected.


In both of these cases, the Function afterwards checks how many word buttons are currently selected. If the number is 1 or more, it makes the Deselect All button clickable (used in gameplay to deselect all buttons currently selected), if not it makes it unclickable. If the number is 4, it makes the Submit button clickable (used in gameplay to submit 4 words as a grouping guess), if not it makes it unclickable. Clickability involves both a clickability status which can stop an event listener, and also a clickable class (which changes the opacity so the player can assume the button can't be clicked.)


#### Event Listener on the Deselect All Button / Deselect Function


> [Main Points] When the Deselect All Button is clicked during gameplay, all the word buttons that are currently in the game are passed to and deselected in the Deselect Function.


In gameplay, a player can press the Select All button to deselect any currently selected words. (Reminder, we established that this button is only clickable if there is at least one button selected) The `Deselect Function` is called when the Deselect All button is clicked, and it takes in all the word buttons in the current game (passed from an `event listener` listening for the click). The `Deselect Function` deselects all the word buttons, which entails changing each word button's status to deselected, class to desselected (the normal color), and setting the number of word buttons currently selected back to 0.


#### Event Listener on the Submit Button / Validate Answer Function


> [Main Points] When the Submit Button is clicked during gameplay, the 4 word buttons that are currently selected are passed to Validate Function, which checks if the guess is correct or not.If the guess is correct, the 4 buttons are deleted from the word grid, and the solution for that grouping is displayed. When all 4 groupings are found a congratulatory message appears. If the guess is incorrect, a mistake is tallied. When all 4 mistakes have been made, a message appears letting the user know they can keep trying in freeplay mode for fun.


In the gameplay, players must find 4 groupings of 4 to win. Additionally, if players make 4 incorrect guesses they lose / enter free play mode. To keep track of this, I initialize variables for the number of solutions found and mistakes made.


In the gameplay, when a player thinks they know a correct grouping they can click the Submit button to submit 4 selected words as a guess. (Reminder, we established that this button is only clickable when 4 buttons are selected.) The `Validate Function` is called when the Submit button is clicked (passed from an `event listener` listening for the click). The 4 selected words are put into an array, and that array is then passed to the `Validate Function.`


The `Validate Function` takes in a guess array (the array of the four words being guessed) and loops through the four answer arrays (the arrays of words that are in the currently selected game) to compare the guess array to each one. It does this by putting the guess array next to one answer array at a time and checking if each item in the guess array appears in the answer array.


If the guess finds a correct match, the 4 buttons are deleted from the word grid, the information describing the category of the found solution is stored in a variable, and the tally of how many solutions have been found is incremented. That tally then tells us the solution order, which is used in a switch statement to determine the visual presentation of the solution that is then displayed(The found solution is displayed at the top of the grid, with the first solution found at the top, the second solution found below it, etc. The word grid and everything below it also moves down with the use of classes to allow room for the solutions to be displayed) In the found solution display, the player can see the category title and the words they guessed that are in that grouping, as well as the level of difficulty of the category which is represented by a color. The `Validate Function` calls to the `Color Solution Function` to assign these values, passing it the guess array of words, the category it matched with, and the solution order.


When all 4 groupings are found a congratulatory message appears.


If the guess doesn't find a correct match, the tally of how many mistakes have been made is incremented, which is displayed to the player by removing one of 4 dots that represents the player's remaining mistakes. An if else statement is used to decide which dot to remove depending on the number of mistakes that have been made so far. The dots are removed by changing their class (defined in styles.css to make them hidden).


When all 4 mistakes have been made, a message appears letting the user know they can keep trying in freeplay mode for fun.


#### Color Solution Function

> [Main Points] When called by the Validate Answer Function, this function applies the corresponding text and color to the solution display.


The `Color Solution Function` is called by the `Validate Answer Function` if an answer is correct, taking in the guess array, category, and solution order of the found solution. It uses a switch statement to add the class (color change) based on the level of difficulty of the category. It then applies the corresponding text content for the category title and solution words (which are found in the answer array).


#### Animations

> [Main Points] I added some animations for user experience, and some just for fun.


I added some animations to the game to improve the user experience by making the results of the player's actions and the current status of their game clear. The selected buttons jump up when they are submitted, then shake if it is an incorrect guess. The results of winning or losing the game are displayed with stretching letters to draw the player's attention to them. I also added an animation just for fun that the player will have to find if they want to see it, which is that the title of the page spins around if you click it.


### My styles.css File

> [Main Points] I created various classes to improve user experience, and an overall style to mirror the original NYT game.


I used my cascading style sheet to help me establish a similar structure to the New York Times' version of the game, while adding my own flourishes such as a different colored header, and some fun animations.


To improve the user experience, I made various classes for elements so that they could be swapped out to show their current state. For example, the buttons are sometimes stylized with a clickable class and other times an unclickable class, so the player doesn't have to ponder whether or not the button can be clicked in this state.


I also used classes to keep some elements on the page in a hidden state so I could easily retrieve them when needed in the game, such as containers for found solutions.
