import random

class Player:
    def __init__(self, name, health=100, location=(0, 0)):
        self.name = name
        self.health = health
        self.location = location
        self.weapon = None

    def take_damage(self, damage):
        self.health -= damage
        if self.health <= 0:
            print(f"{self.name} has been eliminated!")

    def move(self, new_location):
        self.location = new_location
        print(f"{self.name} moves to {self.location}")

    def pick_up_weapon(self, weapon):
        self.weapon = weapon
        print(f"{self.name} picks up {self.weapon}")

    def attack(self, target):
        if self.weapon:
            damage = random.randint(20, 50)  # Damage range for the weapon
            print(f"{self.name} attacks {target.name} with {self.weapon} and deals {damage} damage!")
            target.take_damage(damage)
        else:
            print(f"{self.name} has no weapon to attack with!")

class FortniteGame:
    def __init__(self, player1, player2, play_area_size=(100, 100)):
        self.player1 = player1
        self.player2 = player2
        self.play_area_size = play_area_size

    def drop_weapons(self):
        weapons = ["Assault Rifle", "Shotgun", "Sniper Rifle", "Pistol", "Submachine Gun"]
        return random.choice(weapons)

    def play_game(self):
        print("Welcome to the Fortnite Battle Royale!")
        print(f"{self.player1.name} vs {self.player2.name}")

        self.player1.pick_up_weapon(self.drop_weapons())
        self.player2.pick_up_weapon(self.drop_weapons())

        while self.player1.health > 0 and self.player2.health > 0:
            print("\n--- Next Round ---")
            # Simulate player movement (random for simplicity)
            self.player1.move((random.randint(0, self.play_area_size[0]), random.randint(0, self.play_area_size[1])))
            self.player2.move((random.randint(0, self.play_area_size[0]), random.randint(0, self.play_area_size[1])))

            self.player1.attack(self.player2)
            if self.player2.health <= 0:
                break
            self.player2.attack(self.player1)
            if self.player1.health <= 0:
                break

        print("\n--- Game Over ---")
        if self.player1.health <= 0:
            print(f"{self.player2.name} wins!")
        elif self.player2.health <= 0:
            print(f"{self.player1.name} wins!")

if __name__ == "__main__":
    # Initialize players
    player1_name = input("Enter name for Player 1: ")
    player2_name = input("Enter name for Player 2: ")
    player1 = Player(player1_name)
    player2 = Player(player2_name)

    # Initialize and start the game
    game = FortniteGame(player1, player2)
    game.play_game()
