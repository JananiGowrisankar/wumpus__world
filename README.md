<h1>ExpNo 9: Solve Wumpus World Problem using Python demonstrating Inferences from Propositional Logic</h1> 
<h3>Name: Janani Gowrisankar                      </h3>
<h3>Register Number/Staff Id: 212224100022               </h3>
<H3>Aim:</H3>
<p>
    To solve  Wumpus World Problem using Python demonstrating Inferences from Propositional Logic
</p>
<h1>Problem Description</h1>
<hr>
<h2>Wumpus World</h2>
<hr>
The Wumpus world is a simple world example to illustrate the worth of a knowledge-based agent and to represent knowledge representation.

The figure below shows a Wumpus world containing one pit and one Wumpus. There is an agent in room [1,1]. The goal of the agent is to exit the Wumpus world alive. The agent can exit the Wumpus world by reaching room [4,4]. The wumpus world contains exactly one Wumpus and one pit. There will be a breeze in the rooms adjacent to the pit, and there will be a stench in the rooms adjacent to Wumpus.

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/cd6b68dc-c79f-4dcb-8126-04da90d65912)

<center>Wumpus World Representation</center>
<p>
This is a python program that uses propositional logic sentences to check which rooms are safe. 

It is assumed that there will always be a safe path that the agent can take to exit the Wumpus world. The logical agent can take four actions: Up, Down, Left and Right. These actions help the agent move from one room to an adjacent room. The agent can perceive two things: Breeze and Stench.
</p>

# Program

```
# Wumpus World Agent

class WumpusWorld:
    def __init__(self):
        self.grid_size = 4
        self.agent_pos = [1, 1]
        self.visited = set()
        self.safe = set()
        self.wumpus = (2, 2)
        self.pit = (3, 3)
        self.gold = (4, 3)
        self.exit = (4, 4)
        self.score = 0
        self.game_over = False

    def is_adjacent(self, a, b):
        return abs(a[0] - b[0]) + abs(a[1] - b[1]) == 1

    def perceive(self, pos):
        senses = []
        if self.is_adjacent(pos, self.pit):
            senses.append("Breeze")
        if self.is_adjacent(pos, self.wumpus):
            senses.append("Stench")
        if pos == self.gold:
            senses.append("GOLD")
        return senses

    def move(self, direction):
        if self.game_over:
            return

        x, y = self.agent_pos
        if direction == 'u' and x > 1:
            x -= 1
        elif direction == 'd' and x < self.grid_size:
            x += 1
        elif direction == 'l' and y > 1:
            y -= 1
        elif direction == 'r' and y < self.grid_size:
            y += 1

        self.agent_pos = [x, y]
        self.visited.add(tuple(self.agent_pos))

        current = tuple(self.agent_pos)
        senses = self.perceive(current)

        print(f"current location:  {', '.join(senses) if senses else 'Save'}")

        if current == self.pit or current == self.wumpus:
            print("You DIED. Game over.")
            self.game_over = True
            return

        if "GOLD" in senses:
            self.score = 1000
            print("GOLD FOUND! You won....")
            print("Your score is:   ", self.score)
            self.game_over = True
            return

    def run(self):
        while not self.game_over:
            print("press u to move up")
            print("press d to move down")
            print("press l to move left")
            print("press r to move right")
            move = input()
            self.move(move)


if __name__ == "__main__":
    world = WumpusWorld()
    world.run()

```
<hr>
<h1>Sample Input and Output:</h1>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8696111a-a4a7-47cb-ba4b-43a4ef88573f)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/4be5bf06-79fa-4fa0-9334-38a33f06060b)

