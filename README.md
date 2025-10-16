employees = {}
while True:
    print("\n===== Employee Performance Analyzer =====")
    print("1. Add Employee Performance")
    print("2. View All Records")
    print("3. Generate Report")
    print("4. Exit")

    choice = input("Enter your choice: ")

    if choice == '1':
        name = input("Enter employee name: ").title()
        try:
            score = float(input("Enter performance score (0-10): "))
            if 0 <= score <= 10:
                employees[name] = score
                print(f"✅ Record added for {name}")
            else:
                print("⚠️ Score must be between 0 and 10.")
        except ValueError:
            print("⚠️ Invalid input! Please enter a number.")

    elif choice == '2':
        if not employees:
            print("No records found.")
        else:
            print("\n--- Employee Records ---")
            for name, score in employees.items():
                print(f"{name}: {score}/10")

    elif choice == '3':
        if not employees:
            print("No data to analyze.")
        else:
            avg_score = sum(employees.values()) / len(employees)
            top_employee = max(employees, key=employees.get)
            low_employee = min(employees, key=employees.get)
            print("\n===== Performance Report =====")
            print(f"Average Score: {avg_score:.2f}")
            print(f"🏆 Top Performer: {top_employee} ({employees[top_employee]}/10)")
            print(f"🔻 Needs Improvement: {low_employee} ({employees[low_employee]}/10)")
            with open("performance_report.txt", "w") as f:
                f.write("Employee Performance Report\n")
                f.write(f"Average Score: {avg_score:.2f}\n")
                f.write(f"Top Performer: {top_employee}\n")
                f.write(f"Lowest Performer: {low_employee}\n")
            print("✅ Report saved to performance_report.txt")

    elif choice == '4':
        print("Exiting program. Goodbye!")
        break

    else:
        print("Invalid choice! Please enter 1–4.")
