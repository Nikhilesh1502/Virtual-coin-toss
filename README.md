import random
import os

# File to store history
HISTORY_FILE = "coin_toss_history.txt"

# Function to load previous history
def load_history():
    if os.path.exists(HISTORY_FILE):
        with open(HISTORY_FILE, "r") as file:
            history = file.read().splitlines()
    else:
        history = []
    return history

# Function to save history
def save_history(history):
    with open(HISTORY_FILE, "w") as file:
        file.write("\n".join(history))

# Function to flip a coin
def flip_coin():
    return random.choice(["Heads", "Tails"])

# Function to start the coin toss simulation
def start_simulation():
    history = load_history()
    
    while True:
        try:
            flips = int(input("\nHow many times would you like to flip the coin? (Enter 0 to exit): "))
            if flips == 0:
                print("Exiting... Thank you for using the Coin Toss Simulator!")
                break
            
            heads_count = 0
            tails_count = 0
            
            print("\nFlipping the coin...\n")
            for _ in range(flips):
                result = flip_coin()
                print(f"Result: {result}")
                history.append(result)
                if result == "Heads":
                    heads_count += 1
                else:
                    tails_count += 1
            
            # Display final results
            print("\nFinal Results:")
            print(f"Heads: {heads_count} times ({(heads_count / flips) * 100:.2f}%)")
            print(f"Tails: {tails_count} times ({(tails_count / flips) * 100:.2f}%)")
            
            # Save updated history
            save_history(history)
            
            # Show last 5 flips from history
            print("\nLast 5 Results:", history[-5:])
            
        except ValueError:
            print("Invalid input! Please enter a valid number.")

# Run the simulation
if __name__ == "__main__":
    start_simulation()
