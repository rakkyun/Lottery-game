# Lottery-game
import tkinter as tk
from tkinter import ttk, messagebox
import random


class HomePage:
    def __init__(self, root):
        self.root = root
        self.root.title("Lottery Game - Home")
        self.root.geometry("1200x900")

        # ASCII Art Design
        ascii_art = """

        💸💰💰💰💰💰💰💰💰💰💰💰💰💰💰💰💰💰💸
        💸💰💰💰💰💰💰💰💰💰💰💰💰💰💰💰💰💰💸
    ╔══════════════════════════════════╗
    ║  WELCOME TO THE LOTTERY GAME!    ║   
    ║     Press 'Start' to Begin!      ║
    ╚══════════════════════════════════╝
        
█████   ███   █████ ████████ ████        █████████    ███████  ██████   ███████████████    ███████████ ███████                    
░░███   ░███  ░░██░░███░░░░░ ░███        ███░░░░░███ ███░░░░░██░░██████ █████░░███░░░░░█   ░█░░░███░░░███░░░░░███                  
 ░███   ░███   ░███░███      ░███       ███     ░░░ ███     ░░██░███░█████░███░███  █ ░    ░   ░███  ███     ░░███                 
 ░███   ░███   ░███░████████ ░███      ░███        ░███      ░██░███░░███ ░███░██████          ░███ ░███      ░███                 
 ░░███  █████  ███ ░███░     ░███      ░███        ░███      ░██░███ ░░░  ░███░███░░█          ░███ ░███      ░███                 
  ░░░█████░█████░  ░███      ░███      ░░███     ██░░███     ███░███      ░███░███ ░   █       ░███ ░░███     ███                  
    ░░███ ░░███    █████████ ███████████░░█████████ ░░░███████░ █████     ██████████████       █████ ░░░███████░                   
     ░░░   ░░░     ░░░░░░░░░░░░░░░░░░░░░  ░░░░░░░░░    ░░░░░░░  ░░░░░     ░░░░░░░░░░░░░░       ░░░░░    ░░░░░░░                     
                                                                                                                                   
                                                                                                                                   
                                                                                                                                   
 █████         ███████   ███████████████████████████████████████████ █████ █████      █████████  █████████ ██████   ███████████████
░░███        ███░░░░░███░█░░░███░░░░█░░░███░░░░░███░░░░░░░███░░░░░██░░███ ░░███      ███░░░░░██████░░░░░██░░██████ █████░░███░░░░░█
 ░███       ███     ░░██░   ░███  ░░   ░███  ░ ░███  █ ░ ░███    ░███░░███ ███      ███     ░░░░███    ░███░███░█████░███░███  █ ░ 
 ░███      ░███      ░███   ░███       ░███    ░██████   ░██████████  ░░█████      ░███        ░███████████░███░░███ ░███░██████   
 ░███      ░███      ░███   ░███       ░███    ░███░░█   ░███░░░░░███  ░░███       ░███    ████░███░░░░░███░███ ░░░  ░███░███░░█   
 ░███      ░░███     ███    ░███       ░███    ░███ ░   █░███    ░███   ░███       ░░███  ░░███░███    ░███░███      ░███░███ ░   █
 ███████████░░░███████░     █████      █████   ███████████████   █████  █████       ░░██████████████   █████████     ██████████████
░░░░░░░░░░░   ░░░░░░░      ░░░░░      ░░░░░   ░░░░░░░░░░░░░░░   ░░░░░  ░░░░░         ░░░░░░░░░░░░░░   ░░░░░░░░░     ░░░░░░░░░░░░░░ 
                                                                                                                                   
                                                                                                                                   
                                                                                                                                   
        """

        self.label = tk.Label(
            root, text=ascii_art, font=("Courier", 10), justify="left", fg="blue"
        )
        self.label.pack(pady=10)

        self.start_button = tk.Button(
            root, text="Start Lottery Game", command=self.start_lottery_game, bg="blue", fg="white"
        )
        self.start_button.pack(pady=10)

    def start_lottery_game(self):
        self.root.destroy()  # Close the home page
        lottery_game_window = tk.Tk()
        app = LotteryGame(lottery_game_window)
        lottery_game_window.mainloop()


class ResultsPage:
    def __init__(self, root, user_numbers, lottery_numbers, reward):
        self.root = root
        self.root.title("Lottery Results")
        self.root.geometry("1200x1000")

        self.user_numbers = user_numbers
        self.lottery_numbers = lottery_numbers
        self.reward = reward

        # Display winning or losing ASCII art
        result_ascii_art = self.get_result_ascii_art()

        self.result_label = tk.Label(root, text=result_ascii_art, font=("Courier", 16), bg="aquamarine2")
        self.result_label.pack(pady=20)

        result_text = f"Your Numbers: {user_numbers}\nLottery Numbers: {lottery_numbers}\nReward: {reward} RUPESS"
        self.result_details_label = tk.Label(root, text=result_text, font=("Helvetica", 14), bg="aquamarine2")
        self.result_details_label.pack(pady=20)

        # Play Again button
        self.play_again_button = tk.Button(root, text="Play Again", command=self.play_again, bg="green", fg="white")
        self.play_again_button.pack(pady=10)

    def get_result_ascii_art(self):
        if self.reward > 0:
            return """
    ╔═══════════════════════════════════╗
    ║         CONGRATULATIONS!          ║
    ║      You're a Lottery Winner!     ║
    ║                                   ║
    ╚═══════════════════════════════════╝
    ⢀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⣀⠀⠀⠀⠀
⢠⣤⣤⣤⣼⡇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣿⣄⣤⣤⣠
⢸⠀⡶⠶⠾⡇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⡷⠶⠶⡆⡼
⠈⡇⢷⠀⠀⣇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢰⠇⠀⢸⢁⡗
⠀⢹⡘⡆⠀⢹⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⡸⠀⢀⡏⡼⠀
⠀⠀⢳⡙⣆⠈⣇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⠇⢀⠞⡼⠁⠀
⠀⠀⠀⠙⣌⠳⣼⡄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣞⡴⣫⠞⠀⠀⠀
⠀⠀⠀⠀⠈⠓⢮⣻⡄⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⡼⣩⠞⠉⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠉⠛⣆⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⠞⠋⠁⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠳⢤⣀⠀⠀⠀⠀⢀⣠⠖⠁⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠈⠉⡇⢸⡏⠉⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⡇⢸⡇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢠⠖⠒⠓⠚⠓⠒⣦⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⣀⣠⣞⣉⣉⣉⣉⣉⣉⣉⣉⣉⣉⣙⣆⣀⡀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⡇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⡇⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⡇⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⡇⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⠀⠀⠀⠓⠲⠶⠶⠶⠶⠶⠶⠶⠶⠶⠶⠶⠶⠶⠖⠃⠀⠀⠀⠀⠀⠀
"""
        else:
            return """
        ╔══════════════════════════════════════╗
        ║        BETTER LUCK NEXT TIME!        ║
        ║        SORRY YOU DIDN'T WIN          ║
        ╚══════════════════════════════════════╝
⠀⠀⠀⠀⠀⢀⡀⠀⠀⠀⠀⠀⠀⠀⠀⠀
⠀⠀⠀⠀⢰⣿⡿⠗⠀⠠⠄⡀⠀⠀⠀⠀
⠀⠀⠀⠀⡜⠁⠀⠀⠀⠀⠀⠈⠑⢶⣶⡄
⢀⣶⣦⣸⠀⢼⣟⡇⠀⠀⢀⣀⠀⠘⡿⠃
⠀⢿⣿⣿⣄⠒⠀⠠⢶⡂⢫⣿⢇⢀⠃⠀
⠀⠈⠻⣿⣿⣿⣶⣤⣀⣀⣀⣂⡠⠊⠀⠀
⠀⠀⠀⠃⠀⠀⠉⠙⠛⠿⣿⣿⣧⠀⠀⠀
⠀⠀⠘⡀⠀⠀⠀⠀⠀⠀⠘⣿⣿⡇⠀⠀
⠀⠀⠀⣷⣄⡀⠀⠀⠀⢀⣴⡟⠿⠃⠀⠀
⠀⠀⠀⢻⣿⣿⠉⠉⢹⣿⣿⠁⠀⠀⠀⠀
⠀⠀⠀⠀⠉⠁⠀⠀⠀⠉⠁⠀⠀"""
    def play_again(self):
        self.root.destroy()  # Close the result page
        home_page_window = tk.Tk()
        home_page = HomePage(home_page_window)
        home_page_window.mainloop()


class LotteryGame:
    def __init__(self, root):
        self.root = root
        self.root.title("Lottery Game")
        self.root.geometry("800x600")
        
        #3### Set the background color
        self.root.configure(bg="lightskyblue")
        
        ### Lottery Game
        self.lottery_frame = tk.Frame(root, bg="darksalmon")
        self.lottery_frame.pack(expand=True)
        
        self.label = tk.Label(self.lottery_frame, text="Welcome to the Lottery Game!", font=("Helvetica", 16), bg="darksalmon")
        self.label.pack(pady=10)

        self.label = tk.Label(self.lottery_frame, text="Each Draw costs Rs.200 only.", font=("Helvetica", 12), bg="darksalmon")
        self.label.pack(pady=10)

        self.label = tk.Label(self.lottery_frame, text="Spend money wisely", font=("Helvetica", 12), bg="darksalmon")
        self.label.pack(pady=10)
    

    
        
        self.numbers_frame = tk.Frame(self.lottery_frame, bg="darksalmon")
        self.numbers_frame.pack()
        
        self.number_entries = [tk.Entry(self.numbers_frame, width=2) for _ in range(6)]
        for entry in self.number_entries:
            entry.pack(side=tk.LEFT, padx=5)
        
        self.generate_button = tk.Button(self.lottery_frame, text="Generate Numbers", command=self.generate_numbers, bg="blue", fg="white")
        self.generate_button.pack(pady=10)
        
        self.check_button = tk.Button(self.lottery_frame, text="Check Results", command=self.check_results, bg="blue", fg="white")
        self.check_button.pack(pady=10)

        #### Result Tables
        self.result_table = ttk.Treeview(self.lottery_frame, columns=('User Numbers', 'Lottery Numbers', 'Reward'), show='headings')
        self.result_table.heading('User Numbers', text='User Numbers')
        self.result_table.heading('Lottery Numbers', text='Lottery Numbers')
        self.result_table.heading('Reward', text='Reward')
        self.result_table.pack(pady=10)
        
        ### Reward Dictionary
        self.reward_dict = {
            0: 0,
            1: 1000,
            2: 15000,
            3: 45000,
            4: 80000,
            5: 150000
        }
    
    def generate_numbers(self):
        lottery_numbers = [random.randint(1, 49) for _ in range(6)]
        for i in range(6):
            self.number_entries[i].delete(0, tk.END)
            self.number_entries[i].insert(0, str(lottery_numbers[i]))
    
    def check_results(self):
        user_numbers = [int(entry.get()) for entry in self.number_entries]
        lottery_numbers = [random.randint(1, 49) for _ in range(6)]
        
        matching_numbers = set(user_numbers).intersection(lottery_numbers)
        
        ### Calculate reward based on matching numbers
        reward = self.reward_dict[len(matching_numbers)]
        
        ### Update the result table
        self.result_table.delete(*self.result_table.get_children())
        self.result_table.insert('', 'end', values=(user_numbers, lottery_numbers, reward))
        
        if matching_numbers:
            result_text = f"Well done! You matched {len(matching_numbers)} number(s): {', '.join(map(str, matching_numbers))}."
        else:
            result_text = "Sorry, you didn't match any numbers. Try again!"
        
        messagebox.showinfo("Results", result_text)
        self.show_results_page(user_numbers, lottery_numbers, reward)
    
    def show_results_page(self, user_numbers, lottery_numbers, reward):
        results_window = tk.Toplevel(self.root)
        results_page = ResultsPage(results_window, user_numbers, lottery_numbers, reward)

if __name__ == "__main__":
    root = tk.Tk()
    home_page = HomePage(root)
    root.mainloop()


