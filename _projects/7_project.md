---
layout: page
title: Adventure Game
description: an adventure game using if, elif, and else statements
img: assets/img/Adventure_game.png
importance: 2
category: work
giscus_comments: true
---

This project features a text-based adventure game implemented in Python. It demonstrates the use of conditional logic (`if`, `elif`, `else`), loops, functions, and user input handling.

```python
#This is out section for listing the options the player will go through will choosing their class, items and adventuring area.
a = "Welcome to Gillinor! A land full of choices, mystery and potential for massive rewards. Anybody can make it in this world with the right loadout. Now, select your class: Knight or Wizard. "
choice = input(a).capitalize()

tasks = ["Shop", "Adventuring"]
items = ["Potion", "Armor", "Weapons"]
potion_items = ["Healing Potion", "Harming Potion", "Physical Potion"]
armor_items = ["Adamant equipment", "Mithril equipment", "Rune equipment"]
weapons_items = ["Adamant sword", "Mithril sword", "Rune sword"]
actions = ["Open the Tomb", "Hack the Branches", "Open the Door"]

#By labeling this def shop I can have all of the options the players choices inside the shop added into a easy to read format I will do the same for adventuring later I also need the while true statement here to give the player the option to come back to the start.
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

#As with the shop tab this is for the player to choose their adventure and what will happen with their choses I cannot code a full game at the moment so the choices aren't as indepth.
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

#This section is for the choice on what class they want along with what they plan to do after selecting their class.
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
