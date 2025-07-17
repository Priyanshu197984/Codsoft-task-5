# Codsoft-task-5
import tkinter as tk
from tkinter import messagebox, simpledialog


contacts = []

def add_contact():
    name = name_entry.get()
    phone = phone_entry.get()
    email = email_entry.get()

    if name and phone and email:
        contacts.append((name, phone, email))
        update_listbox()
        clear_entries()
    else:
        messagebox.showwarning("Input Error", "All fields are required.")

def delete_contact():
    selected = contact_listbox.curselection()
    if selected:
        index = selected[0]
        contacts.pop(index)
        update_listbox()
    else:
        messagebox.showwarning("Selection Error", "No contact selected.")

def update_listbox():
    contact_listbox.delete(0, tk.END)
    for contact in contacts:
        contact_listbox.insert(tk.END, f"{contact[0]} | {contact[1]} | {contact[2]}")

def clear_entries():
    name_entry.delete(0, tk.END)
    phone_entry.delete(0, tk.END)
    email_entry.delete(0, tk.END)


root = tk.Tk()
root.title("Contact List")

# Labels and Entries
tk.Label(root, text="Name").grid(row=0, column=0)
tk.Label(root, text="Phone").grid(row=1, column=0)
tk.Label(root, text="Email").grid(row=2, column=0)

name_entry = tk.Entry(root)
phone_entry = tk.Entry(root)
email_entry = tk.Entry(root)

name_entry.grid(row=0, column=1)
phone_entry.grid(row=1, column=1)
email_entry.grid(row=2, column=1)


add_button = tk.Button(root, text="Add Contact", command=add_contact)
delete_button = tk.Button(root, text="Delete Selected", command=delete_contact)

add_button.grid(row=3, column=0, pady=5)
delete_button.grid(row=3, column=1, pady=5)


contact_listbox = tk.Listbox(root, width=50)
contact_listbox.grid(row=4, column=0, columnspan=2, pady=10)


root.mainloop()
