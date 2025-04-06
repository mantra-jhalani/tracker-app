# tracker-app
import tkinter as tk
from tkinter import messagebox

class TaskTrackerApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Task Tracker")
        self.root.geometry("400x400")
        
        # List of tasks
        self.tasks = []

        # Task input field
        self.task_entry = tk.Entry(self.root, width=30)
        self.task_entry.grid(row=0, column=0, padx=10, pady=10)
        
        # Add task button
        self.add_button = tk.Button(self.root, text="Add Task", width=20, command=self.add_task)
        self.add_button.grid(row=0, column=1, padx=10, pady=10)

        # Task list box
        self.task_listbox = tk.Listbox(self.root, width=40, height=10)
        self.task_listbox.grid(row=1, column=0, columnspan=2, padx=10, pady=10)

        # Remove task button
        self.remove_button = tk.Button(self.root, text="Remove Task", width=20, command=self.remove_task)
        self.remove_button.grid(row=2, column=0, columnspan=2, padx=10, pady=10)

    def add_task(self):
        task = self.task_entry.get()
        if task != "":
            self.tasks.append(task)
            self.update_task_listbox()
            self.task_entry.delete(0, tk.END)
        else:
            messagebox.showwarning("Input Error", "Please enter a task.")

    def remove_task(self):
        try:
            selected_task_index = self.task_listbox.curselection()[0]
            self.tasks.pop(selected_task_index)
            self.update_task_listbox()
        except IndexError:
            messagebox.showwarning("Selection Error", "Please select a task to remove.")

    def update_task_listbox(self):
        self.task_listbox.delete(0, tk.END)
        for task in self.tasks:
            self.task_listbox.insert(tk.END, task)

# Create main window
root = tk.Tk()
app = TaskTrackerApp(root)
root.mainloop()
