# ExpNo 9: Solve Wumpus World Problem using Python demonstrating Inferences from Propositional Logic

### Name: EZHILARASI N

### Register Number : 212224040088
### Aim:

To solve Wumpus World Problem using Python demonstrating Inferences from Propositional Logic.

# Problem Description

---

## Wumpus World

---

The Wumpus world is a simple world example to illustrate the worth of a knowledge-based agent and to represent knowledge representation.

The figure below shows a Wumpus world containing one pit and one Wumpus. There is an agent in room [1,1]. The goal of the agent is to exit the Wumpus world alive. The agent can exit the Wumpus world by reaching room [4,4]. The wumpus world contains exactly one Wumpus and one pit. There will be a breeze in the rooms adjacent to the pit, and there will be a stench in the rooms adjacent to Wumpus.

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/cd6b68dc-c79f-4dcb-8126-04da90d65912)

<center>Wumpus World Representation</center>

This is a python program that uses propositional logic sentences to check which rooms are safe.

It is assumed that there will always be a safe path that the agent can take to exit the Wumpus world. The logical agent can take four actions: Up, Down, Left and Right. These actions help the agent move from one room to an adjacent room. The agent can perceive two things: Breeze and Stench.

---

# Sample Input and Output:

---

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8696111a-a4a7-47cb-ba4b-43a4ef88573f)

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/4be5bf06-79fa-4fa0-9334-38a33f06060b)

## PROGRAM:

```python
WUMPUS = (3, 3)
PIT = (2, 3)
GOLD = (4, 4)

# Starting position
position = (1, 1)

score = 0
game_over = False





def adjacent_cells(cell):
    """Return all valid cells adjacent to the given cell."""
    x, y = cell

    neighbours = []

    if x > 1:
        neighbours.append((x - 1, y))
    if x < 4:
        neighbours.append((x + 1, y))
    if y > 1:
        neighbours.append((x, y - 1))
    if y < 4:
        neighbours.append((x, y + 1))

    return neighbours



def infer_percepts(cell):
    """
    Infer Breeze, Stench and Gold from the knowledge base.

    Propositional rules:
        Pit(x,y) -> Breeze(adjacent cells)
        Wumpus(x,y) -> Stench(adjacent cells)
        Gold(x,y) -> Gold at that cell
    """

    percepts = []

    
    if PIT in adjacent_cells(cell):
        percepts.append("Breeze")

    
    if WUMPUS in adjacent_cells(cell):
        percepts.append("Stench")

    
    if cell == GOLD:
        percepts.append("GOLD")

    return percepts



def is_safe(cell):
    """
    A cell is safe if it does not contain a Wumpus or Pit.
    This represents inference from the propositional knowledge base.
    """
    return cell != WUMPUS and cell != PIT



def show_current_location():
    """Display the current inferred percept."""
    percepts = infer_percepts(position)

    print()
    if "GOLD" in percepts:
        print("current location:  GOLD")
    elif percepts:
        print("current location: ", " ".join(percepts))
    else:
        print("current location:  Safe")





def display_controls():
    print()
    print("press u to move up")
    print("press d to move down")
    print("press l to move left")
    print("press r to move right")





def move(direction):
    global position, score, game_over

    x, y = position

    if direction == 'u':
        new_position = (x, y + 1)

    elif direction == 'd':
        new_position = (x, y - 1)

    elif direction == 'l':
        new_position = (x - 1, y)

    elif direction == 'r':
        new_position = (x + 1, y)

    else:
        print("Invalid input!")
        return

    if not (1 <= new_position[0] <= 4 and
            1 <= new_position[1] <= 4):
        print("Cannot move outside the Wumpus World!")
        return

    position = new_position
    score -= 10

    if position == WUMPUS:
        print()
        print("You entered the Wumpus room!")
        print("WUMPUS FOUND! You lose...")
        game_over = True
        return

    if position == PIT:
        print()
        print("You fell into a pit!")
        print("GAME OVER!")
        game_over = True
        return

    if position == GOLD:
        print()
        print("current location:  GOLD")
        print()
        print("GOLD FOUND! You won....")
        print("Your score is:", 1000)
        game_over = True
        return



    show_current_location()



print("========================================")
print("        WUMPUS WORLD")
print("========================================")

print()
print("Agent starts at location [1,1]")
print("Goal: Reach [4,4] and collect GOLD")

show_current_location()

while not game_over:

    display_controls()

    choice = input().lower().strip()

    if choice in ['u', 'd', 'l', 'r']:
        move(choice)
    else:
        print("Please enter only u, d, l or r.")

print()
print("========================================")
print("             GAME OVER")
print("========================================")
```

## OUTPUT:

<img width="516" height="792" alt="image" src="https://github.com/user-attachments/assets/3a462e30-e91c-4209-ac7a-7fbc33173d02" />


## RESULT : 
Solving Wumpus World Problem using Python demonstrating Inferences from Propositional Logic is successfully implemented.
