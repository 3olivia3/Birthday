# Birthday
import tkinter as tk
from tkinter import messagebox
from datetime import datetime

def generate_greeting():
    name = name_entry.get()
    gender = gender_var.get()
    date_str = date_entry.get()
    
    try:
        birthday_date = datetime.strptime(date_str, '%Y-%m-%d')
        today = datetime.today()
        if birthday_date < today:
            messagebox.showerror("Invalid Date", "The date must be in the future.")
            return
    except ValueError:
        messagebox.showerror("Invalid Date", "Please enter the date in YYYY-MM-DD format.")
        return
    
    if gender == "Male":
        greeting = f"Happy Birthday, Mr. {name}!"
    elif gender == "Female":
        greeting = f"Happy Birthday, Ms. {name}!"
    else:
        greeting = f"Happy Birthday, {name}!"
    
    greeting_label.config(text=greeting)

# Initialize the Tkinter window
root = tk.Tk()
root.title("Birthday Greeting App")

# Name input
tk.Label(root, text="Name:").grid(row=0, column=0, padx=10, pady=10)
name_entry = tk.Entry(root)
name_entry.grid(row=0, column=1, padx=10, pady=10)

# Gender input
tk.Label(root, text="Gender:").grid(row=1, column=0, padx=10, pady=10)
gender_var = tk.StringVar(value="Other")
tk.Radiobutton(root, text="Male", variable=gender_var, value="Male").grid(row=1, column=1, padx=10, pady=10)
tk.Radiobutton(root, text="Female", variable=gender_var, value="Female").grid(row=1, column=2, padx=10, pady=10)
tk.Radiobutton(root, text="Other", variable=gender_var, value="Other").grid(row=1, column=3, padx=10, pady=10)

# Date input
tk.Label(root, text="Birthday Date (YYYY-MM-DD):").grid(row=2, column=0, padx=10, pady=10)
date_entry = tk.Entry(root)
date_entry.grid(row=2, column=1, padx=10, pady=10)

# Generate greeting button
generate_button = tk.Button(root, text="Generate Greeting", command=generate_greeting)
generate_button.grid(row=3, column=0, columnspan=4, padx=10, pady=10)

# Greeting label
greeting_label = tk.Label(root, text="", font=("Arial", 12))
greeting_label.grid(row=4, column=0, columnspan=4, padx=10, pady=10)

# Start the GUI event loop
root.mainloop()
