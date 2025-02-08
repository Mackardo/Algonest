# Algimport tkinter as tk
from tkinter import messagebox
from datetime import datetime
import random
import matplotlib.pyplot as plt
from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg

# List of motivational quotes
quotes = [
    "The journey of a thousand miles begins with a single step.",
    "Believe in yourself, and you can achieve anything.",
    "The hardest part is starting, but you've already taken that step!",
    "One day at a time, one step at a time.",
    "You are stronger than your cravings."
]

# Function to get a random motivational quote
def get_motivational_quote():
    return random.choice(quotes)

# Function to calculate the number of smoke-free days
def calculate_days_smoke_free():
    try:
        start_date = datetime.strptime(start_date_entry.get(), "%Y-%m-%d")
        today = datetime.today()
        delta = today - start_date
        return delta.days
    except ValueError:
        messagebox.showerror("Invalid Date", "Please enter a valid start date (YYYY-MM-DD).")
        return 0

# Function to calculate money saved (assuming a pack costs $6 and a person smokes a pack per day)
def calculate_money_saved():
    days_smoke_free = calculate_days_smoke_free()
    pack_cost = 6
    daily_consumption = 1  # Assume 1 pack a day
    money_saved = days_smoke_free * pack_cost * daily_consumption
    return money_saved

# Function to plot the savings and smoke-free days graph
def plot_graph():
    days_smoke_free = calculate_days_smoke_free()
    money_saved = calculate_money_saved()
    
    if days_smoke_free > 0:
        # Data for plotting
        x = [0, days_smoke_free]
        y = [0, money_saved]

        fig, ax = plt.subplots()
        ax.plot(x, y, label="Money Saved ($)")
        ax.set(xlabel='Days Smoke-Free', ylabel='Money Saved ($)', title="Your Progress")
        ax.grid(True)
        ax.legend()

        # Embed the graph into the tkinter window
        canvas = FigureCanvasTkAgg(fig, master=graph_frame)  
        canvas.draw()
        canvas.get_tk_widget().pack()

# Function to show the app's main dashboard
def show_dashboard():
    # Get current data
    days_smoke_free = calculate_days_smoke_free()
    money_saved = calculate_money_saved()
    
    # Update labels with current progress
    days_label.config(text=f"Days Smoke-Free: {days_smoke_free}")
    money_label.config(text=f"Money Saved: ${money_saved:.2f}")
    
    # Display a motivational quote
    quote_label.config(text=f"Motivational Quote: {get_motivational_quote()}")

# Main App Setup
root = tk.Tk()
root.title("Smoke-Free Journey")
root.geometry("600x600")

# Start Date Entry
start_date_label = tk.Label(root, text="Enter Your Quit Date (YYYY-MM-DD):")
start_date_label.pack(pady=10)
start_date_entry = tk.Entry(root)
start_date_entry.pack(pady=10)

# Button to show the dashboard
show_button = tk.Button(root, text="Show Dashboard", command=show_dashboard)
show_button.pack(pady=10)

# Labels for tracking progress
days_label = tk.Label(root, text="Days Smoke-Free: 0")
days_label.pack(pady=10)
money_label = tk.Label(root, text="Money Saved: $0.00")
money_label.pack(pady=10)

# Quote label
quote_label = tk.Label(root, text="Motivational Quote: ")
quote_label.pack(pady=10)

# Frame for the graph
graph_frame = tk.Frame(root)
graph_frame.pack(pady=20)

# Button to plot the graph
plot_button = tk.Button(root, text="Show Progress Graph", command=plot_graph)
plot_button.pack(pady=10)

# Run the Tkinter main loop
root.mainloop()
import tkinter as tk
from tkinter import messagebox
from datetime import datetime
import random
import matplotlib.pyplot as plt
from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg
import json
import os

# List of motivational quotes
quotes = [
    "The journey of a thousand miles begins with a single step.",
    "Believe in yourself, and you can achieve anything.",
    "The hardest part is starting, but you've already taken that step!",
    "One day at a time, one step at a time.",
    "You are stronger than your cravings."
]

# Daily Challenges
challenges = [
    "Complete a 5-minute meditation.",
    "Go for a 10-minute walk outside.",
    "Drink a glass of water and relax for 5 minutes.",
    "Write down your reasons for quitting and remind yourself.",
    "Call or message someone you trust to talk."
]

# Achievements
achievements = {
    "First Week": 7,
    "First Month": 30,
    "Smoke-Free 100": 100,
    "Smoke-Free 200": 200,
    "Money Saved $100": 100,
    "Money Saved $500": 500
}

# Function to get a random motivational quote
def get_motivational_quote():
    return random.choice(quotes)

# Function to get a random daily challenge
def get_daily_challenge():
    return random.choice(challenges)

# Function to calculate the number of smoke-free days
def calculate_days_smoke_free():
    try:
        start_date = datetime.strptime(start_date_entry.get(), "%Y-%m-%d")
        today = datetime.today()
        delta = today - start_date
        return delta.days
    except ValueError:
        messagebox.showerror("Invalid Date", "Please enter a valid start date (YYYY-MM-DD).")
        return 0

# Function to calculate money saved (assuming a pack costs $6 and a person smokes a pack per day)
def calculate_money_saved():
    days_smoke_free = calculate_days_smoke_free()
    pack_cost = 6
    daily_consumption = 1  # Assume 1 pack a day
    money_saved = days_smoke_free * pack_cost * daily_consumption
    return money_saved

# Function to check if the user has achieved a milestone
def check_achievements():
    days_smoke_free = calculate_days_smoke_free()
    money_saved = calculate_money_saved()
    
    earned_achievements = []
    
    # Check achievements based on days smoke-free
    for achievement, milestone in achievements.items():
        if "Smoke-Free" in achievement and days_smoke_free >= milestone:
            earned_achievements.append(achievement)
        elif "Money Saved" in achievement and money_saved >= milestone:
            earned_achievements.append(achievement)
    
    return earned_achievements

# Function to plot the savings and smoke-free days graph
def plot_graph():
    days_smoke_free = calculate_days_smoke_free()
    money_saved = calculate_money_saved()
    
    if days_smoke_free > 0:
        # Data for plotting
        x = [0, days_smoke_free]
        y = [0, money_saved]

        fig, ax = plt.subplots()
        ax.plot(x, y, label="Money Saved ($)")
        ax.set(xlabel='Days Smoke-Free', ylabel='Money Saved ($)', title="Your Progress")
        ax.grid(True)
        ax.legend()

        # Embed the graph into the tkinter window
        canvas = FigureCanvasTkAgg(fig, master=graph_frame)  
        canvas.draw()
        canvas.get_tk_widget().pack()

# Function to show the app's main dashboard
def show_dashboard():
    # Get current data
    days_smoke_free = calculate_days_smoke_free()
    money_saved = calculate_money_saved()
    
    # Update labels with current progress
    days_label.config(text=f"Days Smoke-Free: {days_smoke_free}")
    money_label.config(text=f"Money Saved: ${money_saved:.2f}")
    
    # Display a motivational quote
    quote_label.config(text=f"Motivational Quote: {get_motivational_quote()}")
    
    # Show earned achievements
    earned_achievements = check_achievements()
    achievements_label.config(text=f"Achievements Unlocked: {', '.join(earned_achievements)}")
    
    # Show daily challenge
    challenge_label.config(text=f"Today's Challenge: {get_daily_challenge()}")

# Function to save and load user data (avatar progress, date, etc.)
def save_user_data():
    user_data = {
        "start_date": start_date_entry.get(),
        "days_smoke_free": calculate_days_smoke_free(),
        "money_saved": calculate_money_saved(),
        "achievements": check_achievements(),
    }
    
    if not os.path.exists("user_data.json"):
        with open("user_data.json", "w") as f:
            json.dump(user_data, f)
    
def load_user_data():
    if os.path.exists("user_data.json"):
        with open("user_data.json", "r") as f:
            data = json.load(f)
            return data
    return None

# Main App Setup
root = tk.Tk()
root.title("Smoke-Free Journey")
root.geometry("600x600")

# Start Date Entry
start_date_label = tk.Label(root, text="Enter Your Quit Date (YYYY-MM-DD):")
start_date_label.pack(pady=10)
start_date_entry = tk.Entry(root)
start_date_entry.pack(pady=10)

# Button to show the dashboard
show_button = tk.Button(root, text="Show Dashboard", command=show_dashboard)
show_button.pack(pady=10)

# Labels for tracking progress
days_label = tk.Label(root, text="Days Smoke-Free: 0")
days_label.pack(pady=10)
money_label = tk.Label(root, text="Money Saved: $0.00")
money_label.pack(pady=10)

# Quote label
quote_label = tk.Label(root, text="Motivational Quote: ")
quote_label.pack(pady=10)

# Achievements label
achievements_label = tk.Label(root, text="Achievements Unlocked: ")
achievements_label.pack(pady=10)

# Daily Challenge label
challenge_label = tk.Label(root, text="Today's Challenge: ")
challenge_label.pack(pady=10)

# Frame for the graph
graph_frame = tk.Frame(root)
graph_frame.pack(pady=20)

# Button to plot the graph
plot_button = tk.Button(root, text="Show Progress Graph", command=plot_graph)
plot_button.pack(pady=10)

# Button to save user data
save_button = tk.Button(root, text="Save Progress", command=save_user_data)
save_button.pack(pady=10)

# Button to load user data
load_button = tk.Button(root, text="Load Progress", command=load_user_data)
load_button.pack(pady=10)

# Run the Tkinter main loop
root.mainloop()
onest
