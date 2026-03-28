---
layout: page
title: Adventure Game
description: A text-based adventure demonstrating conditional logic, loops, and modular programming.
img: assets/img/Adventure_game.png
importance: 5
category: work
---

This project serves as a technical demonstration of core programming concepts using Python. It features a text-based adventure game where player choices dictate the flow of the narrative and the availability of resources.

### Technical Overview

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <strong>Conditional Logic</strong>
        <p>Utilizes <code>if/elif/else</code> blocks to manage complex branching paths and decision-making trees based on player input.</p>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <strong>Data Normalization</strong>
        <p>Employs string methods like <code>.capitalize()</code> and <code>.upper()</code> to ensure input sanitization and program robustness.</p>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <strong>Functional Design</strong>
        <p>Demonstrates modularity by encapsulating game systems (Shop, Adventure) into reusable Python functions.</p>
    </div>
</div>
<div class="caption">
    A summary of the programming principles showcased in this implementation.
</div>

### Why this shows Concept Mastery

1.  **Nested `if` Statements:** By nesting conditions inside the `shop()` function, you show you can handle "sub-choices" (e.g., first picking a category, then picking an item).
2.  **Boolean Logic:** Using `if choice == "Knight" or choice == "Wizard"` demonstrates how to evaluate multiple valid conditions at once.
3.  **State Management:** The `while True` loop keeps the "webpage" (game) running until the user explicitly chooses to exit, showing an understanding of program lifecycle.

### Source Code

```python
# Character and Area Setup
a = "Welcome to Gillinor! Select your class (Knight/Wizard): "
choice = input(a).capitalize()
items = ["Potion", "Armor", "Weapons"]
potion_items = ["Healing Potion", "Harming Potion", "Physical Potion"]
armor_items = ["Adamant equipment", "Mithril equipment", "Rune equipment"]
weapons_items = ["Adamant sword", "Mithril sword", "Rune sword"]

# Shop System
def shop():
    while True:
        print("\nWelcome to the shop! Here are your items: ")
        print(items)

        selected_item = input("Please select an item, or type 'Exit' to leave: ").capitalize()

        if selected_item == "Potion":
            print("You have selected Potions: ", potion_items)
            potion_choice = input("Which potion would you like to buy? ").title()
            if potion_choice in potion_items:
                print(f"You have obtained a {potion_choice}.")
            else:
                print("Please select a valid potion.")

        elif selected_item == "Armor":
            print("You have selected Armor: ", armor_items)
            armor_choice = input("Which armor would you like to buy? ").title()
            if armor_choice in armor_items:
                print(f"You have obtained {armor_choice}.")
            else:
                print("Please select a valid armor choice.")

        elif selected_item == "Weapons":
            print("You have selected Weapons: ", weapons_items)
            weapon_choice = input("Which weapon would you like to buy? ").title()
            if weapon_choice in weapon_items:
                print(f"You have obtained a {weapon_choice}.")
            else:
                print("Please select a valid weapon choice.")

        elif selected_item == "Exit":
            print("Returning to the main menu...")
            break  
        else:
            print("Invalid choice. Please select Potion, Armor, or Weapons.")

# Adventure Logic
def adventuring():
    print("\nWelcome to the start of your adventure!")
    selected_action = input("Where to explore? (Open the Tomb / Hack the Branches / Open the Door): ").title()

    if selected_action == "Open The Tomb":
        print("You approach the ancient tomb...")
        door_choice = input("What door do you go through? N, W, E, S: ").upper()
        if door_choice in ["N", "W", "E", "S"]:
            print("You fall through a trapdoor and perish.")

    elif selected_action == "Hack The Branches":
        print("You reveal a hidden path into the forest...")
        building_choice = input("Do you enter the building? Y/N ").upper()
        if building_choice == "Y":
            print("You are stabbed from behind and slain.")
        else:
            print("You decide to return to the village.")

    elif selected_action == "Open The Door":
        print("You step into a grand hall...")
        book_choice = input("Do you reach for the floating book? Y/N ").upper()
        if book_choice == "Y":
            print("The book attacks you. You fall.")
        else:
            print("You decide to return to the village.")

# Main Game Loop
if choice == "Knight" or choice == "Wizard":
    while True:  
        activity = input("\nWould you like to go to the Shop, Adventuring, or Exit? ").capitalize()
        if activity == "Shop":
            shop()
        elif activity == "Adventuring":
            adventuring()
        elif activity == "Exit":
            break  
        else:
            print("Invalid activity.")
```