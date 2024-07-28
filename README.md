import pickle 

def load_tasks(filename='tasks.pkl'):
    try:
        with open(filename, 'rb') as f:
            return pickle.load(f)
    except FileNotFoundError:
        return []

def save_tasks(tasks, filename='tasks.pkl'):
    with open(filename, 'wb') as f:
        pickle.dump(tasks, f)

def display_tasks(tasks):
    if not tasks:
        print("No tasks available.")
    for i, task in enumerate(tasks, start=1):
        status = "Completed" if task['completed'] else "Pending"
        print(f"{i}. {task['description']} [{status}]")

def add_task(tasks):
    description = input("Enter task description: ")
    tasks.append({'description': description, 'completed': False})

def update_task(tasks):
    display_tasks(tasks)
    try:
        task_num = int(input("Enter task number to update: ")) - 1
        if 0 <= task_num < len(tasks):
            tasks[task_num]['completed'] = not tasks[task_num]['completed']
        else:
            print("Invalid task number.")
    except ValueError:
        print("Please enter a valid number.")

def delete_task(tasks):
    display_tasks(tasks)
    try:
        task_num = int(input("Enter task number to delete: ")) - 1
        if 0 <= task_num < len(tasks):
            tasks.pop(task_num)
        else:
            print("Invalid task number.")
    except ValueError:
        print("Please enter a valid number.")

def main():
    tasks = load_tasks()
    while True:
        print("\n1. View Tasks\n2. Add Task\n3. Update Task\n4. Delete Task\n5. Exit")
        choice = input("Enter your choice: ")
        if choice == '1':
            display_tasks(tasks)
        elif choice == '2':
            add_task(tasks)
        elif choice == '3':
            update_task(tasks)
        elif choice == '4':
            delete_task(tasks)
        elif choice == '5':
            save_tasks(tasks)
            break
        else:
            print("Invalid choice.")

if __name__ == "__main__":
    main()

def add(x, y):
    return x + y

def subtract(x, y):
    return x - y

def multiply(x, y):
    return x * y

def divide(x, y):
    if y != 0:
        return x / y
    else:
        return "Error! Division by zero."

def main():
    print("Welcome to the Simple Calculator!")

    try:
        # Get user input
        num1 = float(input("Enter the number1: "))
        num2 = float(input("Enter the number2: "))

        print("\nChoose an operation:")
        print("1. Add")
        print("2. Subtract")
        print("3. Multiply")
        print("4. Divide")

        choice = input("Enter the number of the operation (1/2/3/4): ")

        if choice == '1':
            print(f"\nResult: {num1} + {num2} = {add(num1, num2)}")
        elif choice == '2':
            print(f"\nResult: {num1} - {num2} = {subtract(num1, num2)}")
        elif choice == '3':
            print(f"\nResult: {num1} * {num2} = {multiply(num1, num2)}")
        elif choice == '4':
            result = divide(num1, num2)
            if isinstance(result, str):
                print(result)
            else:
                print(f"\nResult: {num1} / {num2} = {result}")
        else:
            print("Invalid input! Please choose a valid operation.")

    except ValueError:
        print("Invalid input! Please enter numeric values for the numbers.")

if __name__ == "__main__":
    main()

import random

def get_computer_choice():
    choices = ['rock', 'paper', 'scissors']
    return random.choice(choices)

def get_user_choice():
    while True:
        choice = input("Enter your choice (rock, paper, or scissors): ").lower()
        if choice in ['rock', 'paper', 'scissors']:
            return choice
        else:
            print("Invalid choice. Please enter 'rock', 'paper', or 'scissors'.")

def determine_winner(user_choice, computer_choice):
    if user_choice == computer_choice:
        return "tie"
    elif (user_choice == 'rock' and computer_choice == 'scissors') or \
         (user_choice == 'scissors' and computer_choice == 'paper') or \
         (user_choice == 'paper' and computer_choice == 'rock'):
        return "user"
    else:
        return "computer"

def main():
    print("Welcome to Rock, Paper, Scissors!")
    
    user_score = 0
    computer_score = 0
    
    while True:
        user_choice = get_user_choice()
        computer_choice = get_computer_choice()
        
        print(f"\nYou chose: {user_choice}")
        print(f"Computer chose: {computer_choice}")
        
        winner = determine_winner(user_choice, computer_choice)
        
        if winner == "user":
            print("You win!")
            user_score += 1
        elif winner == "computer":
            print("Computer wins!")
            computer_score += 1
        else:
            print("It's a tie!")
        
        print(f"\nScore: You {user_score} - {computer_score} Computer")
        
        play_again = input("\nDo you want to play another round? (yes/no): ").lower()
        if play_again != 'yes':
            break
    
    print("\nThanks for playing! Final Score:")
    print(f"You {user_score} - {computer_score} Computer")
    if user_score > computer_score:
        print("You are the overall winner!")
    elif user_score < computer_score:
        print("Computer is the overall winner!")
    else:
        print("The game is a tie!")

if __name__ == "__main__":
    main()
