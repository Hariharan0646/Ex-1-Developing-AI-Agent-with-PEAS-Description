# Ex-1-Developing-AI-Agent-with-PEAS-Description
### Name: Hariharan S

### Register Number: 2305001009

### Aim:
To find the PEAS description for the given AI problem and develop an AI agent.

### Theory :
PEAS stands for:
'''
P-Performance measure

E-Environment

A-Actuators

S-Sensors
'''

It’s a framework used to define the task environment for an AI agent clearly.

### Pick an AI Problem

```

1. Self-driving car

2. Chess playing agent

3. Vacuum cleaning robot

4. Email spam filter

5. Personal assistant (like Siri or Alexa)
```

### Chess playing agent
### Algorithm:
Step 1: Initialize:

Set agent’s location to A

Set environment dirt status for locations A and B (True = dirty, False = clean)

Step 2 :Repeat until all locations are clean (no dirt):
a. Sense if current location has dirt
b. If current location has dirt:
- Suck dirt (set dirt status at current location to False)
c. Else:
- If current location is A, move right to location B
- Else if current location is B, move left to location A
d. Print the agent’s current location and dirt status (optional for debugging)

Step 3: Stop when all locations are clean

Step 4: Print total steps taken (optional)

### Program:
```
import random
board = [
    ["r","n","b","q","k","b","n","r"],
    ["p","p","p","p","p","p","p","p"],
    [".",".",".",".",".",".",".","."],
    [".",".",".",".",".",".",".","."],
    [".",".",".",".",".",".",".","."],
    [".",".",".",".",".",".",".","."],
    ["P","P","P","P","P","P","P","P"],
    ["R","N","B","Q","K","B","N","R"]
]

def print_board():
    print("   a b c d e f g h")
    for i, row in enumerate(board):
        print(f"{8-i}  " + " ".join(row))
    print()

def notation_to_pos(move):
    col_map = "abcdefgh"
    return 8-int(move[1]), col_map.index(move[0])

def pos_to_notation(pos):
    row,col = pos
    col_map = "abcdefgh"
    return f"{col_map[col]}{8-row}"

def get_moves(is_white):
    moves = []
    for r in range(8):
        for c in range(8):
            piece = board[r][c]
            if piece == ".": 
                continue
            if is_white and piece.isupper() or (not is_white and piece.islower()):
                for rr in range(8):
                    for cc in range(8):
                        if (rr,cc)!=(r,c) and board[rr][cc]=="." or (is_white and board[rr][cc].islower()) or (not is_white and board[rr][cc].isupper()):
                            moves.append(((r,c),(rr,cc)))
    return moves

def make_move(start,end):
    r1,c1=start; r2,c2=end
    board[r2][c2]=board[r1][c1]
    board[r1][c1]="."

def game():
    white_turn=True
    print_board()
    while True:
        flat=sum(board,[])
        if "K" not in flat:
            print("Black wins! King captured.")
            break
        if "k" not in flat:
            print("White wins! King captured.")
            break

        if white_turn:
            move=input("Your move (e.g., e2 e4): ").split()
            try:
                start=notation_to_pos(move[0]); end=notation_to_pos(move[1])
                make_move(start,end)
            except:
                print("Invalid input, try again."); continue
        else:
            moves=get_moves(False)
            if not moves: 
                print("Stalemate!"); break
            start,end=random.choice(moves)
            make_move(start,end)
            print(f"AI plays {pos_to_notation(start)} {pos_to_notation(end)}")

        print_board()
        white_turn=not white_turn

game()
```
### Sample Output:

<img width="291" height="323" alt="image" src="https://github.com/user-attachments/assets/6018986c-e311-434a-9baa-37985e718f55" />

<img width="396" height="600" alt="image" src="https://github.com/user-attachments/assets/925d6c51-1014-4960-b4af-9d3a5ae1b57f" />


### Result: 
