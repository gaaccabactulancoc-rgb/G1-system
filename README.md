import time, datetime

tasks = {} # Use a dictionary to store tasks and deadlines


def task_schedule_organizer():
    print("Start")
    print("LOG IN")
    while True:
        username = input("ENTER USERNAME: ")
        if username != "Baby":
            print("===Incorrect username.===")
            continue # Restart the loop to re-enter username
        password = input("ENTER PASSWORD: ")
        if password != "12345678":
            print("===Incorrect password.===")
            continue # Restart the loop to re-enter password
       

        while True:
            choice = input("Main Menu\n1. Add Task\n2. View Tasks\n3. Notify Task\n4. Delete Task\n5. Log Out\n6. Exit\nEnter Number: ")

            if choice == "1":
                task = input("Enter Task: ")
                tasks[task] = None # Initialize without a deadline
                print("===Task Successfully Added.===")

            elif choice == "2":
                now = datetime.datetime.now()
                for task, deadline in tasks.items():
                    if deadline:
                        remaining = deadline - now
                        print(f"- {task}: {remaining}")
                        if remaining <= datetime.timedelta(seconds=0):
                            print(f" !!! Task '{task}' is OVERDUE !!!")
                    else:
                        print(f"- {task}: No deadline set")

            elif choice == "3":
                task = input("Task to Notify: ")
                if task in tasks:
                    date_str = input("Date & Time (YYYY-MM-DD HH:MM:SS): ")
                    try:
                        tasks[task] = datetime.datetime.strptime(date_str, '%Y-%m-%d %H:%M:%S')
                        print("===Notification Successfully Added.===")
                    except ValueError:
                        print("===Invalid date format===")
                else:
                    print("===Task not found===")

            elif choice == "4":
                task = input("Enter Task to Delete: ")
                if task in tasks:
                    del tasks[task]
                    print("===Task Successfully Deleted.===")
                else:
                    print("===Task not found===")
                
            elif choice == "5":
                print("===Log out===")
                break
                
            elif choice == "6":
                break

            else:
                print("===Invalid Number===")


task_schedule_organizer()
