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
