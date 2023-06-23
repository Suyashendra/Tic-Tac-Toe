# Tic Tac Toe

## Introduction
**Tic-Tac-Toe** is among the games played between two players played on a **3 x 3 square grid**. Each player inhabits a cell in their respective turns, keeping the objective of placing three similar marks in a vertical, horizontal, or diagonal pattern. The first player utilizes the **Cross (X)** as the marker, whereas the other utilizes the **Naught or Zero (O)**.

## Design of Tic-Tac-Toe
We will be using the command prompt in order to play Tic-Tac-Toe. Thus, it is the primary objective to construct a design for the Tic-Tac-Toe game.

**Objective:** If a player needs to mark a specific block, he/she must input the corresponding digit displayed in the grid. For instance, we wanted to occupy the upper right block, and then we have to enter digit 3 in the terminal.

Let us understand the snippet of code to generate the grid.

**Code:**
```Python 
# Function to print the Tic-Tac-Toe Design
def mytictactoe(value):
    print("\n")
	print("\t      _____ _____ _____")
	print("\t     |     |     |     |")
	print(f"\t     |  {value[0]}  |  {value[1]}  |  {value[2]}  |")
	print(f"\t     |_____|_____|_____|")
	# printing the second three boxes of the 3x3 game board
	print("\t     |     |     |     |")
	print(f"\t     |  {value[3]}  |  {value[4]}  |  {value[5]}  |")
	print(f"\t     |_____|_____|_____|")
	print("\t     |     |     |     |")
	# printing the last three boxes of the 3x3 game board
	print(f"\t     |  {value[6]}  |  {value[7]}  |  {value[8]}  |")
	print(f"\t     |_____|_____|_____|")
	print("\n")
```

**Explanation:** \
In the above snippet of code, we have defined a function for the Tic-Tac-Toe game that takes the values as the parameter. Here the **value** parameter is a list consists of the status of each cell in the grid. Within the function, we have then printed the design of the Tic-Tac-Toe grid.

## Storing Data using the Data Structures
At any point in Time, there are two crucial pieces of information required:
1. **Grid Status:** We have to create a data structure that will contain the state of each cell. The state can either be occupied or vacant.
2. **Moves of each player:** The knowledge of past and present moves of each player is somehow required, that is, the positions occupied by 'X' and 'O'.

**Code:** 
```Python
# Function for a single game of Tic-Tac-Toe
def singlegame(curplayer):

    # Representing the Tic-Tac-Toe
    value = ['' for i in range(9)]

    # Storing the positions occupied by X and O
    playerpos = {'X':[], 'O':[]}
```
**Explanation:** \
In the above snippet of code, we have defined a function for a single game of Tic-Tac-Toe where the val represents the parameter for the previous function and playerpos stores the position of the block occupied by the cross (X) and naught (O), respectively.

There are generally three values in a list of characters that manages the Grid Status:

1. ' ' - This character signifies the vacant or empty cell.
    
2. 'X' - This character signifies that a Cell is inhabited by the X Player.

3. 'O' - This character signifies that a Cell is inhabited by the O Player.

Moves of each player are kept as a dictionary of a list of integers where the keys are denoted by 'X' and 'O' for the corresponding player. Their respective lists consist of the digits provided to the cells in the grid they inhabit.

The curplayer variable stores the current player making a move, as in 'X' or 'O'.

## Understanding the Game Loop
Every game consists of some type of game loop that allows the player to play the game until a player wins or the game is a tie. In the game of Tic-Tac-Toe, every loop iteration denotes a single move made by any player.

**Syntax:**
```Python
# Loop of Game for a single game of Tic-Tac-Toe
while True:
    mytictactoe(value)
``` 
**Explanation:**\
As we can observe, we have used the while loop to print the values for the function mytictactoe(), generating a game loop for a single game of Tic-Tac-Toe.\
Handling the input from Player for every iteration in the game, the player has to provide the input for his move. Let us consider the following code in order to handle the Player's input.

**Code:**
```Python
# Try-Exception block for CHANCE input
try:
    print("Player ",curplayer,"turn. Choose your Block : ",end="")
    chance = int(input())
except ValueError:
    print("Invalid Input!!! Try Again")
    continue

# Sanity check for CHANCE input
if chance < 1 or chance > 9:
    print("Invalid Input!!! Try Again")
    continue

# Checking if the block is not occupied already 
if value[chance - 1]!= '':
    print("Oops! The Place is already occupied. Try again!!")
    continue
```
**Explanation:**\
For the above snippet of code, we have created a try block to handle the unintended value of the players. We have then handled the exception of **ValueError** so that the game msut not be stopped. Later we have performed few sanity checks, such as whether the entered value is a valid position or not, and if it is a valid position, is it filled already or not.

## Updating the Game information

As per the input provided by the player, we have to update the information for the smooth working of the game. We can update the game information by adding the following snippet of code to the main project.

**Code:**
```Python
# Updating the game information

# Update the status of the grid
value[chance - 1] = curplayer

# Update the positions of the player
playerpos[curplayer].append(chance)
```
**Explanation:**\
In the above code snippet of code, we have updated the game information by updating the status of the grid and position of the player. The **value** list will update the cell filled as per the current player. The position of the player will add the position just occupied by the current player.\
Once the **value** list is updated, we will call the mytictactoe() function, and the grid would look like the following:\
**Output:**
```
              _____ _____ _____
             |     |     |     |
             |  1  |  2  |  3  |
             |_____|_____|_____|
             |     |     |     |
             |  4  |  5  |  6  |
             |_____|_____|_____|
             |     |     |     |
             |  7  |  8  |  9  |
             |_____|_____|_____|
```

## Checking Win or Tie

After each move we need to check if any player has won the match or the match has been tied. We can check it with the help of the syntax given below:

**Syntax:**
```Python
# Calling Function to checkVictory  
if check_Victory(playerpos, curplayer):  
    mytictactoe(value)  
    print("Congratulations!Player ", curplayer, "has won thegame!")       
    print("\n")  
    return curplayer  
          
# Calling Function to check Tie  
if check_Tie(playerpos):  
    mytictactoe(value)  
    print("Oh! Game Tied")  
    print("\n")  
    return 'D'  
```
**Explanation:**\
In the above syntax, we have used the **if** statement to check for Win or Tie. The **singlegame()** function will return the current player if he/she wins the game. Otherwise, the game is tied, **'D'** is sent back.

Let us consider the function checking whether any player has won.

**Code:**
```Python
    # Defining Function to check Victory  
    def check_Victory(playerpos, curplayer):  
       
        # All probable winning combinations  
        solution = [[1, 2, 3], [4, 5, 6], [7, 8, 9], [1, 4, 7], [2, 5, 8], [3, 6, 9], [1, 5, 9], [3, 5, 7]]  
       
        # Loop to check whether any winning combination is satisfied or not  
        for i in solution:  
            if all(j in playerpos[curplayer] for j in i):  
       
                # Return True if any winning combination is satisfied  
                return True  
        # Return False if no combination is satisfied   
        return False         
       
    # Defining Function to check if the game is Tied  
    def check_Tie(playerpos):  
        if len(playerpos['X']) + len(playerpos['O']) == 9:  
            return True  
        return False     
```

**Explanation:**\
In the above snippet of code, we have defined the functions to check the Victory or Tie. These functions are **check_Victory()** and **check_Tie()**, respectively.

1. **check_Victory():** It stores all the combinations for winning the game. The function checks if the position of the current player satisfies any of the winning combinations. If it does, it will return TRUE; else, it will FALSE for not satisfying the requirement.

2. **check_Tie():** It is pretty simple, which checks if all 'Nine' positions are occupied, the game is tied.

## Switching the current player

Every player got only one chance at a time. Thus, after every successful more, the current player will be swapped. Let us consider the following snippet of code for the same:

**Code:**
```Python
    # Switching moves of the player  
    if curplayer == 'X':  
        curplayer = 'O'  
    else:  
        curplayer = 'X'  
```

**Explanation:**\
In the following snippet of code, we have used the if-else statement in order to switch moves of the player in such a way that if the current player marks one position, then the current player will be changed, and the other player will mark their move.

These are some steps we need to be concerned about while making a single game. However, we will be creating a Scoreboard System to keep track of the players wanting to play multiple games.

## Entering the Names of the Players

Since we are creating a Scoreboard, it becomes necessary for us to display the names of each player.

Here is the syntax is shown below for the same:

**Code:**
```Python
    if __name__ == "__main__":  
       
        print("First Player")  
        FirstPlayer = input("Specify the Name: ")  
        print("\n")  
       
        print("Second Player")  
        SecondPlayer = input("Specify the Name: ")  
        print("\n")  
```

**Explanation:**\
As we can observe, we have used the special variable **__name__** to have the value of **"__main__"**. We have then provided the input for the names of the first and second players, respectively. This will become the entry point for the program, and when the program we will be executed, it will ask for the names first.

## Storing the Information regarding the Game

We have to store the information such as the current player, the player's selection (i.e., X or O), the available selections (X or O), and the scoreboard.

**Code:**
```Python
    # Storing the player who chooses X and O  
    curplayer = FirstPlayer  
       
    # Storing the Players' choice  
    playerchoice = {'X' : "", 'O' : ""}  
       
    # Storing the options  
    opt = ['X', 'O']  
       
    # Storing the scoreboard  
    scoreboard = {FirstPlayer: 0, SecondPlayer: 0}  
    myscoreboard(scoreboard)  
```

**Explanation:**\
In the above snippet of code, we have set the current player as the First player. We have also stored the selections made by Players, available options, and the scoreboard.

## Designing the Scoreboard

We will design a scoreboard in a dictionary data structure. For this scoreboard, the player names will act as the keys, and their total number of victories will act as the values. Let us consider the following snippet of code to design the Scoreboard for Tic-Tac-Toe.

**Code:**
```Python
    def myscoreboard(scoreboard):  
        print("\t--------------------------------")  
        print("\t         SCORE BOARD       ")  
        print("\t--------------------------------")  
       
        listlistofplayers = list(scoreboard.keys())  
        print("\t   ", listofplayers[0], "\t    ", scoreboard[listofplayers[0]])  
        print("\t   ", listofplayers[1], "\t    ", scoreboard[listofplayers[1]])  
       
        print("\t--------------------------------\n")  
```

**Explanation:**\
In the above snippet of code, we have defined the function as myscoreboard that takes the parameter as the scoreboard. We have then printed the design for the Score Board. We have defined the variable that stores the names of the players as a list using the .keys() function. We have then indexed them into the scoreboard and displayed the scores.
Creating an Outer Game Loop

In order to maintain multiple matches of Tic-Tac-Toe, we require another loop for the game. The current player will choose the mark for each match. The menu for selection should be displayed in every iteration of the game.

Let us consider the following syntax to create the Outer Gamer Loop.

**Code:**
```Python
    # Loop for a series of Tic-Tac-Toe game  
    # The loop executes until the players quit  
    while True:  
       
         # Main Menu for Players  
         print(curplayer, "will make the choice:")  
         print("Press 1 for X")  
         print("Press 2 for O")  
         print("Press 3 to Quit")  
```

**Explanation:**\
In the above snippet of code, we have created a while loop to display the main menu for the Players where the current player can make the selection between the marks (Cross 'X' or Naught 'O') or exit the game.

**Output:**
```
First Player
Specify the Name: Andy


Second Player
Specify the Name: Carlo


        --------------------------------
                 SCORE BOARD       
        --------------------------------
            Andy             0
            Carlo            0
        --------------------------------

Andy will make the choice: </br>
Press 1 for X </br>
Press 2 for O </br>
Press 3 to Quit </br>
```
Handling and Assigning the Selections for Player

We need to handle and store the choice of the current player for each iteration. Let us consider the following snippet of code for the same.

**Code:**
```Python
    # Try exception for THE_CHOICE input  
    try:  
        the_choice = int(input())     
      except ValueError:  
        print("Invalid Input!!! Try Again\n")  
        continue  
       
    # Conditions for player choice    
    if the_choice == 1:  
        playerchoice['X'] = curplayer  
        if curplayer == FirstPlayer:  
            playerchoice['O'] = SecondPlayer  
        else:  
            playerchoice['O'] = FirstPlayer  
       
    elif the_choice == 2:  
         playerchoice['O'] = curplayer  
         if curplayer == FirstPlayer:  
             playerchoice['X'] = SecondPlayer  
         else:  
             playerchoice['X'] = FirstPlayer  
               
    elif the_choice == 3:  
         print("The Final Scores")  
         myscoreboard(scoreboard)  
         break    
       
    else:  
         print("Invalid Selection!! Try Again\n")  
```

**Explanation:**\
In the above snippet of code, we have used the try-exception block to handle any exception for the the_choice input. We have then used the if-else statement to create the choice menu for the current player to select from.

As per the selection made by the player, the data will be stored. This is significant as it will tell us which player won after every match.
Executing the Game

Once all the required information is stored, we can execute an independent match and record the victory mark.

The syntax for the same has been shown below.

**Code:**
```Python
    # Storing the winner in a single game of Tic-Tac-Toe  
    win = singlegame(opt[the_choice - 1])  
```

**Explanation:**\
In the above snippet of code, we have stored the winner details for a single game of Tic-Tac-Toe.
Updating the Scoreboard

We have to update the scoreboard after every match of the Tic-Tac-Toe game.

Let us consider the following snippet of code to update the scoreboard.

**Code:**
```Python
    # Updation of the scoreboard as per the winner  
    if win != 'D' :  
        playerWon = playerchoice[win]  
        scoreboard[playerWon] = scoreboard[playerWon] + 1  
       
    myscoreboard(scoreboard)  
```

**Explanation:**\
In the above snippet of code, we have used the if statement to check if the match is not tied. Once the match is not drawn, the scoreboard will be updated.
Switching the Selecting Player

While playing a game, it becomes mandatory to switch the chance of choosing the mark. So, let us consider the following syntax to understanding the swapping.

**Code:**
```Python
    # Switching player who chooses X or O  
    if curplayer == FirstPlayer:  
        curplayer = SecondPlayer  
    else:  
        curplayer = FirstPlayer  
```

**Explanation:**\
In the above snippet of code, we have again used the if-else statement to switch between the players to choose the marks (Cross or Naught).

## Final Result:

```
First Player
Specify the Name: A


Second Player
Specify the Name: B


        --------------------------------
                 SCORE BOARD       
        --------------------------------
            A        0
            B        0
        --------------------------------

A will make the choice:
Press 1 for X
Press 2 for O
Press 3 to Quit
1


              _____ _____ _____
             |     |     |     |
             |     |     |     |
             |_____|_____|_____|
             |     |     |     |
             |     |     |     |
             |_____|_____|_____|
             |     |     |     |
             |     |     |     |
             |_____|_____|_____|


Player  X  turn. Choose your Block : 1 


              _____ _____ _____
             |     |     |     |
             |  X  |     |     |
             |_____|_____|_____|
             |     |     |     |
             |     |     |     |
             |_____|_____|_____|
             |     |     |     |
             |     |     |     |
             |_____|_____|_____|


Player  O  turn. Choose your Block : 9


              _____ _____ _____
             |     |     |     |
             |  X  |     |     |
             |_____|_____|_____|
             |     |     |     |
             |     |     |     |
             |_____|_____|_____|
             |     |     |     |
             |     |     |  O  |
             |_____|_____|_____|


Player  X  turn. Choose your Block : 3


              _____ _____ _____
             |     |     |     |
             |  X  |     |  X  |
             |_____|_____|_____|
             |     |     |     |
             |     |     |     |
             |_____|_____|_____|
             |     |     |     |
             |     |     |  O  |
             |_____|_____|_____|


Player  O  turn. Choose your Block : 2


              _____ _____ _____
             |     |     |     |
             |  X  |  O  |  X  |
             |_____|_____|_____|
             |     |     |     |
             |     |     |     |
             |_____|_____|_____|
             |     |     |     |
             |     |     |  O  |
             |_____|_____|_____|


Player  X  turn. Choose your Block : 2
Oops! The Place is already occupied. Try again!!


              _____ _____ _____
             |     |     |     |
             |  X  |  O  |  X  |
             |_____|_____|_____|
             |     |     |     |
             |     |     |     |
             |_____|_____|_____|
             |     |     |     |
             |     |     |  O  |
             |_____|_____|_____|


Player  X  turn. Choose your Block : 4


              _____ _____ _____
             |     |     |     |
             |  X  |  O  |  X  |
             |_____|_____|_____|
             |     |     |     |
             |  X  |     |     |
             |_____|_____|_____|
             |     |     |     |
             |     |     |  O  |
             |_____|_____|_____|


Player  O  turn. Choose your Block : 6


              _____ _____ _____
             |     |     |     |
             |  X  |  O  |  X  |
             |_____|_____|_____|
             |     |     |     |
             |  X  |     |  O  |
             |_____|_____|_____|
             |     |     |     |
             |     |     |  O  |
             |_____|_____|_____|


Player  X  turn. Choose your Block : 7

              _____ _____ _____
             |     |     |     |
             |  X  |  O  |  X  |
             |_____|_____|_____|
             |     |     |     |
             |  X  |     |  O  |
             |_____|_____|_____|
             |     |     |     |
             |  X  |     |  O  |
             |_____|_____|_____|


Congratulations! Player  X  has won the game!!


        --------------------------------
                 SCORE BOARD
        --------------------------------
            A        1
            B        0
        --------------------------------

B will make the choice:
Press 1 for X
Press 2 for O
Press 3 to Quit
3
The Final Scores
        --------------------------------
                 SCORE BOARD
        --------------------------------
            A        1
            B        0
        --------------------------------
```
