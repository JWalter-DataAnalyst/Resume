---
layout: page
title: Adventure Game
description: an adventure game using if, elif, and else statements
img: assets/img/Adventure_game.png
importance: 2
category: work
giscus_comments: true
---

Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width.

To give your project a background in the portfolio page, just add the img tag to the front matter like so:

    ---
    layout: page
    title: project
    description: a project with a background image
    img: /assets/img/Adventure_game.png
    ---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/1.jpg" title="Logic Flow" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/3.jpg" title="World Map" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Adventure_game.png" title="Game Splash" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, logic branches artistically fall into place. Right, the splash screen for our Adventure Game.
</div>

You can also put regular text between your rows of images and code snippets.
Say you wanted to write a little bit about your project before you posted the rest of the logic.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next sections.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <p>This project features a text-based adventure game implemented in Python. It demonstrates the use of conditional logic (<code>if</code>, <code>elif</code>, <code>else</code>), loops, functions, and user input handling. Below is a breakdown of the game's core modules.</p>
    </div>
</div>

<h3 class="mt-4">1. Initialization and Setup</h3>
<p>The game begins by defining the world and allowing the player to select their class. We also initialize lists for the shop inventory and adventure locations.</p>

```python
# Character and world setup: Defining classes, items, and actions
a = "Welcome to Gillinor! A land full of choices, mystery and potential for massive rewards. Anybody can make it in this world with the right loadout. Now, select your class: Knight or Wizard. "
choice = input(a).capitalize()

tasks = ["Shop", "Adventuring"]
items = ["Potion", "Armor", "Weapons"]
potion_items = ["Healing Potion", "Harming Potion", "Physical Potion"]
armor_items = ["Adamant equipment", "Mithril equipment", "Rune equipment"]
weapons_items = ["Adamant sword", "Mithril sword", "Rune sword"]
actions = ["Open the Tomb", "Hack the Branches", "Open the Door"]
```

<h3 class="mt-4">2. The Shopping System</h3>
<p>The <code>shop()</code> function manages item acquisition. It uses a <code>while True</code> loop to keep the player in the shop menu until they explicitly choose to "Exit". Nested conditionals handle the selection of specific items within categories.</p>

```python
def shop():
    while True:
        print("Welcome to the shop! Here are your items: ")
        print(items)

        selected_item = input("Please select an item (Potion, Armor, Weapons), or type 'Exit' to leave the shop: ").capitalize()

        if selected_item == "Potion":
            print("You have selected Potions: ", potion_items)
            potion_choice = input("Which potion would you like to buy? ").title()
            if potion_choice == "Healing Potion":
                print("You have obtained a Healing Potion.")
            elif potion_choice == "Harming Potion":
                print("You have obtained a Harming Potion.")
            elif potion_choice == "Physical Potion":
                print("You have obtained a Physical Potion.")
            else:
                print("Please select a potion choice.")

        elif selected_item == "Armor":
            print("You have selected Armor: ", armor_items)
            armor_choice = input("Which armor would you like to buy? ").title()
            if armor_choice == "Adamant Equipment":
                print("You have obtained Adamant equipment.")
            elif armor_choice == "Mithril Equipment":
                print("You have obtained Mithril equipment.")
            elif armor_choice == "Rune Equipment":
                print("You have obtained Rune equipment.")
            else:
                print("Please select an armor choice.")

        elif selected_item == "Weapons":
            print("You have selected Weapons: ", weapons_items)
            weapon_choice = input("Which weapon would you like to buy? ").title()
            if weapon_choice == "Adamant Sword":
                print("You have obtained an Adamant sword.")
            elif weapon_choice == "Mithril Sword":
                print("You have obtained a Mithril sword.")
            elif weapon_choice == "Rune Sword":
                print("You have obtained a Rune sword.")
            else:
                print("Please select a weapon choice.")

        elif selected_item == "Exit":
            print("Thank you for visiting the shop. See you next time!")
            break  

        else:
            print("That is not an item choice. Please select Potion, Armor, or Weapons.")
```

<h3 class="mt-4">3. Exploration and Narrative Logic</h3>
<p>The <code>adventuring()</code> function contains the narrative branches. Depending on the player's choice of location, different outcomes are triggered using Python's branching logic.</p>

```python
def adventuring():
    print("Welcome to the start of your adventure!")
    selected_action = input("Where do you want to explore? Choose one: Open the Tomb, Hack the Branches, Open the Door: ").title()

    if selected_action == "Open The Tomb":
        print("You approach the ancient tomb. The stone door creaks open as you step inside...")
        print("You notice four red doorways that illuminate the area")
        door_choice = input("What door do you go through? N, W, E, S: ").upper()
        if door_choice in ["N", "W", "E", "S"]:
            print("You fall through a trapdoor and perish.")
        else:
            print("Please select a door choice.")

    elif selected_action == "Hack The Branches":
        print("You hack your way through the thick branches, revealing a hidden path into the forest...")
        print("As you walk through the forest you see a building. Do you enter? Y/N ")
        building_choice = input("Do you enter? Y/N ").upper()
        if building_choice == "Y":
            print("You are stabbed from behind and slain")
        else:
            print("You decide to turn around returning to the village.")

    elif selected_action == "Open The Door":
        print("You push the door open and step into a grand hall filled with mysteries...")
        print("You see a book that looks extra special. Do you reach for the book? Y/N ")
        book_choice = input("Y/N ").upper()
        if book_choice == "Y":
            print("The book levitates off from the bookshelf and begins attacking you. You were unable to get proper footing and fall to the book.")
        else:
            print("You decide to turn around returning to the village.")

    else:
        print("Please select a listed action. Please choose 'Open the Tomb', 'Hack the Branches', or 'Open the Door'.")
```

<h3 class="mt-4">4. Core Game Loop</h3>
<p>The script checks for a valid class selection and enters the primary loop, driving the interaction between the shop and the adventuring zones.</p>

```python
if choice == "Knight" or choice == "Wizard":
    while True:  
        activity = input("Would you like to go to the Shop, Adventuring, or Exit? ").capitalize()

        if activity == "Shop":
            shop()
        elif activity == "Adventuring":
            adventuring()
        elif activity == "Exit":
            print("Thank you for playing!")
            break  
        else:
            print("Please select a listed choice, please choose Shop, Adventuring, or Exit.")
```

{% endraw %}
