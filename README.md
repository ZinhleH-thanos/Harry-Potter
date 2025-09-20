# 🧙‍♂️ Hogwarts Trials


Welcome to the **Hogwarts Trials** — a text-based adventure game challenge where you’ll use your Python skills to guide a magical character through mysterious hidden rooms beneath Hogwarts in search of the legendary **Wand of Merlin**.

---

## 📖 Game Overview

You will guide a **Hogwarts student** through a secret underground trial system where they must pass three challenges to retrieve the **Wand of Merlin**.

To win the game, players must:

- Explore the map
- Solve 3 magical trials
- Collect:
  - 🧠 **Diadem of Wit**
  - 💛 **Medallion of Loyalty**
  - ❤️ **Heart of Courage**
- Unlock the final room: **The Room of Secrets**

---

## 🗂️ Project Structure

```text
hogwarts_trials/
├── game.py               # Main game loop
├── player.py             # Player class and character logic
├── room.py               # Room class
├── commands.py           # Commands class
├── game_data.json        # Prebuilt map and item locations
├── characters.txt        # Your custom character list (5 total)
├── save_load.py          # File I/O save/load logic
├── HogwartsTrials.md     # Instructions on how to play the game (DO NOT EDIT)
```

---

## 👥 Characters

Create a list, minimum, of **5 Hogwarts characters** (either from the Harry Potter world or originals that fit). For each character, specify:

- Name
- House
- Strength
- Weakness

📝 Example (`characters.txt`):

```text
Luna Lovegood,Ravenclaw,Insightful,Easily Distracted
Dean Thomas,Gryffindor,Resourceful,Doubts Himself
Maisie Flint,Slytherin,Ambitious,Trust Issues
Elijah Bramble,Hufflepuff,Loyal to Friends,Slow to Decide
```

In `game.py`, your player should be created from one of these entries.

---

## 🧭 Provided Rooms

A sample `game_data.json` file has been included with six Hogwarts-themed rooms and their connections. These include:

- **Library** (start)
- **Potion Storeroom**
- **Mirror Hallway**
- **Ravenclaw Chamber** (🧠 Trial)
- **Hufflepuff Garden** (💛 Trial)
- **Gryffindor Arena** (❤️ Trial)
- **Room of Secrets** (final room)

**NOTE** - You don’t need to invent the whole map, just build the logic and flavour of the trial rooms!

---

## 🧠 Trial Room Example: Ravenclaw’s Riddle

Here’s a basic example of a puzzle you can trigger when a player attempts to pick up the item in the **Ravenclaw Chamber** → test of wit.

```python
def ravenclaw_riddle(player, item_name):
    # Only trigger in Ravenclaw Chamber for the Diadem
    if item_name.lower() != "diadem of wit":
        return False  # normal take behavior for other items

    if "Diadem of Wit" in player.inventory:
        print("You've already solved the riddle and claimed the Diadem of Wit.")
        return True

    print("\nA tall bronze eagle door knocker speaks:")
    print("\"I speak without a mouth and hear without ears. I have no body, but I come alive with the wind. What am I?\"")
    answer = input("Your answer: ").strip().lower()

    if answer in ["echo", "an echo"]:
        print("\nThe door swings open silently. A glowing Diadem floats before you.")
        player.inventory.append("Diadem of Wit")
        return True
    else:
        print("\nThe door remains closed. Perhaps think differently and try again later.")
        return True  # prevent direct pickup unless solved

```

**NOTE** - You **DO NOT** need to implement your riddle trigger functions exactly as this example

You will need to create this for the other rooms:

- Gryffindor Arena → lock the Heart of Courage behind a bravery test (e.g. walk into darkness).
- Hufflepuff Garden → lock the Medallion of Loyalty behind a choice (e.g. give up an item in inventory).

---

## 🎮 Player Commands Guide

These are the basic commands your player can use in the game. The game loop should listen for these inputs and trigger the appropriate actions.

| Command        | Description |
|----------------|-------------|
| `go [direction]` | Move the player in a specified direction. E.g. `go north`, `go east` |
| `look`         | Show the current room's description, available exits, and visible items |
| `take [item]`  | Pick up an item in the current room and add it to the player’s inventory. E.g. `take map` |
| `use [item]`   | Use an item in your inventory. For example, `use key` might unlock a door |
| `inventory`    | Show all items currently in the player’s inventory |
| `help`         | List all available commands and a short description of each |
| `save`         | Save the current game state to a file |
| `load`         | Load the previously saved game state |
| `quit` / `exit`| Exit the game loop |

---

### 🧑‍💻 Example Input/Output

```text
> look
You are in the Potion Storeroom.
Shelves of dusty bottles line the stone walls. A cauldron still steams in the corner.
You see: truth serum, silver ladle
Exits: south, east, west

> take truth serum
You added the truth serum to your inventory.

> go east
You moved into the Ravenclaw Chamber.

> inventory
You are carrying: truth serum
```

---

## 🔄 Suggested Steps

### Phase 1: World & Room Setup

- Implement `Room` and `Command` classes
- Load rooms from `game_data.json`

### Phase 2: Player Logic

- Implement `Player` class
- Load a player from `characters.txt`

### Phase 3: Core Game Engine

- Build command loop
- Allow room-to-room movement

### Phase 4: Save/Load

- Add ability to save and load game state

### Phase 5: Polish & Stretch

- Riddle logic, loyalty tests, courage moments
- Different behavior based on character strengths/weaknesses
- Room unlock logic

---

## 🧪 Optional Extras

- Write tests for all your classes
- Store riddles in a JSON file and load randomly
- Let characters have special powers (e.g. Luna sees secrets)
- Add a spell-casting system or duel
- Add visual flavour using `colorama` (text colors)

**Note** - These should only be attempted once all basic funtionality is in place

---

## ✅ End Goal

Once the player collects all 3 artifacts and reaches the **Room of Secrets**, display this:

> “The trials have accepted you. With wisdom, loyalty, and courage, you now hold the Wand of Merlin. What will you do with such power?”

---

## 🧙‍♀️ Good Luck, Wizards!

All examples in this document are guides only. You have the creative freedom to structure your code however you like — from how commands are written, to how input/output appears during gameplay. This is your time to shine! Work with your group, write clean code, tell a great story, and *may your logic be as sharp as your wand*.
