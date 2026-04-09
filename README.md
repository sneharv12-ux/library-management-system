# Library Management System

books = {}          # Stores book name and quantity
issued_books = {}   # Stores issued books with user names


# Add Book
def add_book():
    name = input("Enter book name: ")
    qty = int(input("Enter quantity: "))
    
    if name in books:
        books[name] += qty
    else:
        books[name] = qty
    
    print(f"{qty} copies of '{name}' added.\n")


# Issue Book
def issue_book():
    name = input("Enter book name: ")
    user = input("Enter user name: ")
    
    if name in books and books[name] > 0:
        books[name] -= 1
        
        if name in issued_books:
            issued_books[name].append(user)
        else:
            issued_books[name] = [user]
        
        print(f"'{name}' issued to {user}.\n")
    else:
        print("Book not available.\n")


# Return Book
def return_book():
    name = input("Enter book name: ")
    user = input("Enter user name: ")
    
    if name in issued_books and user in issued_books[name]:
        books[name] += 1
        issued_books[name].remove(user)
        
        if len(issued_books[name]) == 0:
            del issued_books[name]
        
        print(f"'{name}' returned by {user}.\n")
    else:
        print("Invalid return request.\n")


# Check Availability
def check_availability():
    print("\nAvailable Books:")
    if not books:
        print("No books available.")
    else:
        for book, qty in books.items():
            print(f"{book}: {qty} copies")
    print()


# View Issued Books
def view_issued_books():
    print("\nIssued Books:")
    if not issued_books:
        print("No books issued.")
    else:
        for book, users in issued_books.items():
            print(f"{book} issued to: {', '.join(users)}")
    print()


# Main Menu
while True:
    print("===== Library Menu =====")
    print("1. Add Book")
    print("2. Issue Book")
    print("3. Return Book")
    print("4. Check Availability")
    print("5. View Issued Books")
    print("6. Exit")
    
    choice = input("Enter your choice: ")
    
    if choice == '1':
        add_book()
    elif choice == '2':
        issue_book()
    elif choice == '3':
        return_book()
    elif choice == '4':
        check_availability()
    elif choice == '5':
        view_issued_books()
    elif choice == '6':
        print("Exiting system...")
        break
    else:
        print("Invalid choice. Try again.\n")
