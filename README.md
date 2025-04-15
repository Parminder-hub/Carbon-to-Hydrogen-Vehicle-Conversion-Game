# Carbon-to-Hydrogen-Vehicle-Conversion-Game
import random

# Initial game variables
total_vehicles = 5000
carbon_vehicles = total_vehicles
hydrogen_vehicles = 0
funds = 1000000  # Initial funds in USD
hydrogen_cost_per_vehicle = 5000  # Cost to convert one vehicle to hydrogen
conversion_rate = 0.1  # Percentage of vehicles converted per round

# Function to convert vehicles to hydrogen
def convert_to_hydrogen():
    global carbon_vehicles, hydrogen_vehicles, funds
    if carbon_vehicles > 0:
        vehicles_to_convert = min(carbon_vehicles, int(conversion_rate * total_vehicles))
        conversion_cost = vehicles_to_convert * hydrogen_cost_per_vehicle

        if funds >= conversion_cost:
            funds -= conversion_cost
            carbon_vehicles -= vehicles_to_convert
            hydrogen_vehicles += vehicles_to_convert
            print(f"Converted {vehicles_to_convert} vehicles to hydrogen. Remaining carbon vehicles: {carbon_vehicles}")
            print(f"Funds remaining: ${funds}")
        else:
            print("Insufficient funds to convert more vehicles.")
    else:
        print("All vehicles have been converted to hydrogen!")

# Function to track emissions reduction
def track_emissions():
    carbon_emissions_reduction = (total_vehicles - carbon_vehicles) * 100
    print(f"Total emissions reduced: {carbon_emissions_reduction} tons of CO2.")

# Main game loop
def play_game():
    global funds
    print("Welcome to the Carbon to Hydrogen Vehicle Conversion Game!")
    print("Goal: Convert 5000 carbon-powered vehicles to hydrogen-powered vehicles.")
    
    while carbon_vehicles > 0:
        print(f"\nCurrent Status: {carbon_vehicles} carbon-powered vehicles remaining.")
        print(f"Hydrogen vehicles: {hydrogen_vehicles}")
        print(f"Funds: ${funds}")
        
        action = input("Would you like to convert vehicles? (yes/no): ").lower()
        if action == "yes":
            convert_to_hydrogen()
            track_emissions()
        else:
            print("You decided to not convert vehicles this round.")
        
        # Random event that could add funds or cost
        event = random.choice(["funds", "nothing"])
        if event == "funds":
            extra_funds = random.randint(50000, 200000)
            funds += extra_funds
            print(f"You received a grant of ${extra_funds} to aid in the conversion process.")
    
    print("Congratulations! You have converted all vehicles to hydrogen!")

# Start the game
play_game()
