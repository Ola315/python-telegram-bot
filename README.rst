Here is the complete and corrected code:

```
import random
import time
import paypalrestsdk

# PayPal API credentials
client_id = "YOUR_CLIENT_ID"
client_secret = "YOUR_CLIENT_SECRET"
paypal_email = "imranridwan201@gmail.com"

# Set up PayPal API
paypal = paypalrestsdk.Api({
    "mode": "sandbox",  # or "live" for production
    "client_id": client_id,
    "client_secret": client_secret
})

class TigerGame:
    def __init__(self):
        self.player_progress = 0
        self.energy = 100
        self.telegram_stars = 0
        self.consecutive_wins = 0
        self.leaderboard = {}
        self.tiger_data = ["Defensive Tiger", "Protective Tiger", "Defensive Attacking Tiger", "Flexibility Tiger", "Attacking Tiger"]
        self.tiger_ranks = ["Novice", "Apprentice", "Warrior", "Master", "Champion", "Legend", "Mythic", "Heroic", "Epic", "Rare", "Unique", "Elite", "Superior", "Exceptional", "Ultimate", "Supreme", "Dominant", "Fearless", "Invincible", "Unstoppable", "Unbeatable", "Legendary", "Mythical", "Godly", "Transcendent", "Omni", "Alpha", "Omega"]
        self.player_tiger = {"Type": "Defensive Tiger", "Rank": "Novice", "Level": 1, "Experience": 0}
        self.in_app_purchases = {
            "100 Telegram Stars": 4.99,
            "500 Telegram Stars": 19.99,
            "1000 Telegram Stars": 39.99,
            "Energy Boost": 1.99,
            "Rare Tiger": 9.99,
            "Legendary Tiger": 19.99,
            "Theta Coin Pack": 9.99
        }
        self.player_inventory = {
            "Energy": 100,
            "Tigers": ["Defensive Tiger"],
            "Items": [],
            "Theta Coins": 0,
            "Tiger Tones": 0
        }

    def play_game(self):
        while True:
            print("\n1. Battle")
            print("2. Tap")
            print("3. Buy Telegram Stars")
            print("4. View Progress")
            print("5. Leaderboard")
            print("6. Shop")
            print("7. Upgrade Tiger")
            print("8. Exit")

            choice = input("Enter choice: ")

            if choice == "1":
                self.battle()
            elif choice == "2":
                self.tap()
            elif choice == "3":
                amount = int(input("Enter Telegram Stars to buy: "))
                self.buy_telegram_stars(amount)
                print(f"Telegram Stars: {self.telegram_stars}")
            elif choice == "4":
                self.view_progress()
            elif choice == "5":
                self.display_leaderboard()
            elif choice == "6":
                self.display_shop()
            elif choice == "7":
                self.upgrade_tiger()
            elif choice == "8":
                break
            else:
                print("Invalid choice")

            if self.energy <= 0:
                print("Game Over! You ran out of energy.")
                break

            self.replenish_energy()

    def battle(self):
        print("Battle started!")
        time.sleep(2)
        print("Battle finished!")
        self.player_inventory["Tiger Tones"] += 10
        self.player_tiger["Experience"] += 10
        if self.player_tiger["Experience"] >= 100:
            self.player_tiger["Level"] += 1
            self.player_tiger["Experience"] = 0
            print("Tiger leveled up!")

    def tap(self):
        print("Tapped!")
        time.sleep(1)
        self.player_inventory["Tiger Tones"] += 1

    def buy_telegram_stars(self, amount):
        payment = paypal.Payment({
            "intent": "sale",
            "payer": {
                "payment_method": "paypal"
            },
            "transactions": [{
                "amount": {
                    "currency": "USD",
                    "total": self.in_app_purchases[f"{amount} Telegram Stars"]
                },
                "description": f"{amount} Telegram Stars"
            }],
            "redirect_urls": {
                "return_url": "http://localhost:3000/payment/execute",
                "cancel_url": "http://localhost:3000/"
            }
        })
        payment_response = payment.create()
        for link in payment_response.links:
            if link.rel == "approval_url":
                approval_url = link.href
                print("Redirecting to PayPal payment page...")
                print(approval_url)
        self.telegram_stars += amount

    def view
```
