import random
import tkinter as tk
from tkinter import messagebox, StringVar, Entry

# Sample character string for password generation
character_string = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()"

# Initialize Tkinter Window
password_gen = tk.Tk()
password_gen.title("Password Generator")
password_gen.geometry("350x250")

#Password generator function
def generate_password():
    try:
        repeat = int(repeat_entry.get())  # Get if repetition is allowed (0 or 1)
        length = int(length_entry.get())  # Get the desired password length
    except ValueError:
        messagebox.showerror(message="Please enter valid inputs")
        return

    # Check if the user allows repetition of characters
    if repeat == 1:
        password = random.choices(character_string, k=length)  # Repetition allowed
    else:
        if length > len(character_string):
            messagebox.showerror(message="Length exceeds available unique characters!")
            return
        password = random.sample(character_string, length)  # No repetition allowed

    # Since the returned value is a list, we convert it to a string using join
    password = ''.join(password)

    # Update the StringVar to show the password
    password_v.set("Created password: " + password)

# Declare a StringVar to hold the password text
password_v = StringVar()

# Create the Entry widgets and labels for inputs
tk.Label(password_gen, text="Allow Repetition (0 or 1):").place(x=10, y=20)
repeat_entry = tk.Entry(password_gen)
repeat_entry.place(x=200, y=20)

tk.Label(password_gen, text="Password Length:").place(x=10, y=60)
length_entry = tk.Entry(password_gen)
length_entry.place(x=200, y=60)

# Create a button to generate the password
generate_btn = tk.Button(password_gen, text="Generate Password", command=generate_password)
generate_btn.place(x=10, y=100)

# Create a read-only entry box to display the generated password
password_label = tk.Entry(password_gen, bd=0, bg="gray85", textvariable=password_v, state="readonly")
password_label.place(x=10, y=140, height=50, width=320)

# Run the Tkinter main loop
password_gen.mainloop()
