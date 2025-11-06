🧩 Description
The Library Book Tracking System is a console-based application built in C# that helps manage books in a library.
It allows users (librarians) to:
Add new books
View all books
Search for a book by ID or title
Update book details
Delete books from the system
This system uses Object-Oriented Programming (OOP) concepts such as classes, objects, constructors, and encapsulation.
Data is stored temporarily in a list, simulating a basic in-memory database.

🧠 Concepts Used
Concept	Description
Class and Objects the Book class represents the data model.
Encapsulation Book attributes are private, accessed using getters/setters.
List Collection	Used to store multiple book records dynamically.
Methods and Functions Separate functions for each CRUD operation.
Control Structures switch, foreach, and loops manage user actions.

💻 Full Source Code (C# Console App)


using System;
using System.Collections.Generic;

namespace LibraryTrackingSystem
{
    // ==============================
    // Book Class (Data Model)
    // ==============================
    class Book
    {
        // Private Fields (Encapsulation)
        private int id;
        private string title;
        private string author;
        private bool isAvailable;

        // Constructor
        public Book(int id, string title, string author, bool isAvailable = true)
        {
            this.id = id;
            this.title = title;
            this.author = author;
            this.isAvailable = isAvailable;
        }

        // Getters and Setters
        public int Id { get { return id; } set { id = value; } }
        public string Title { get { return title; } set { title = value; } }
        public string Author { get { return author; } set { author = value; } }
        public bool IsAvailable { get { return isAvailable; } set { isAvailable = value; } }

        // Display Book Info
        public void Display()
        {
            Console.WriteLine($"ID: {id}, Title: {title}, Author: {author}, Available: {(isAvailable ? "Yes" : "No")}");
        }
    }

    // ==============================
    // Main Library System Class
    // ==============================
    class LibrarySystem
    {
        private List<Book> books = new List<Book>();

        // Add a New Book
        public void AddBook()
        {
            Console.Write("\nEnter Book ID: ");
            int id = int.Parse(Console.ReadLine());

            Console.Write("Enter Book Title: ");
            string title = Console.ReadLine();

            Console.Write("Enter Author Name: ");
            string author = Console.ReadLine();

            books.Add(new Book(id, title, author));
            Console.WriteLine("\n Book added successfully!");
        }

        // Display All Books
        public void ViewBooks()
        {
            Console.WriteLine("\n Library Book List:");
            if (books.Count == 0)
            {
                Console.WriteLine("No books available.");
                return;
            }

            foreach (Book b in books)
                b.Display();
        }

        // Search for a Book
        public void SearchBook()
        {
            Console.Write("\nEnter Book ID or Title to Search: ");
            string input = Console.ReadLine();

            bool found = false;
            foreach (Book b in books)
            {
                if (b.Id.ToString() == input || b.Title.Equals(input, StringComparison.OrdinalIgnoreCase))
                {
                    Console.WriteLine("\n🔍 Book Found:");
                    b.Display();
                    found = true;
                    break;
                }
            }

            if (!found)
                Console.WriteLine(" Book not found.");
        }

        // Update Book Availability
        public void UpdateBook()
        {
            Console.Write("\nEnter Book ID to Update: ");
            int id = int.Parse(Console.ReadLine());

            Book book = books.Find(b => b.Id == id);
            if (book != null)
            {
                Console.Write("Is the book available (yes/no)? ");
                string response = Console.ReadLine().ToLower();
                book.IsAvailable = response == "yes";
                Console.WriteLine(" Book updated successfully!");
            }
            else
            {
                Console.WriteLine(" Book not found.");
            }
        }

        // Delete a Book
        public void DeleteBook()
        {
            Console.Write("\nEnter Book ID to Delete: ");
            int id = int.Parse(Console.ReadLine());

            Book book = books.Find(b => b.Id == id);
            if (book != null)
            {
                books.Remove(book);
                Console.WriteLine(" Book deleted successfully!");
            }
            else
            {
                Console.WriteLine(" Book not found.");
            }
        }
    }

    // ==============================
    // Main Program Entry Point
    // ==============================
    class Program
    {
        static void Main(string[] args)
        {
            LibrarySystem library = new LibrarySystem();
            int choice;

            do
            {
                Console.WriteLine("\n===== LIBRARY BOOK TRACKING SYSTEM =====");
                Console.WriteLine("1. Add Book");
                Console.WriteLine("2. View Books");
                Console.WriteLine("3. Search Book");
                Console.WriteLine("4. Update Book");
                Console.WriteLine("5. Delete Book");
                Console.WriteLine("6. Exit");
                Console.Write("Enter your choice: ");

                choice = int.Parse(Console.ReadLine());

                switch (choice)
                {
                    case 1:
                        library.AddBook();
                        break;
                    case 2:
                        library.ViewBooks();
                        break;
                    case 3:
                        library.SearchBook();
                        break;
                    case 4:
                        library.UpdateBook();
                        break;
                    case 5:
                        library.DeleteBook();
                        break;
                    case 6:
                        Console.WriteLine(" Exiting... Thank you!");
                        break;
                    default:
                        Console.WriteLine(" Invalid choice. Please try again.");
                        break;
                }

            } while (choice != 6);
        }
    }
}

🧾 How It Works (Workflow)
The Library Book Tracking System operates through a simple and user-friendly console interface that allows users to manage library books efficiently. When the program is executed, it begins by displaying a main menu that presents the user with several options to choose from—such as Add Book, View Books, Search Book, Update Book, Delete Book, and Exit.
The workflow of the program proceeds as follows:
Program Initialization:
When the program starts, it creates an instance of the LibrarySystem class and displays the main menu to the user.
User Selection:
The user selects an operation from the menu by entering the corresponding number (1–6). Each choice corresponds to a specific function within the system.
Operation Execution:
Based on the user’s selection, the system performs the required task:
Add Book: Prompts the user to enter details such as ID, title, and author, then adds the book to the list.
View Books: Displays all the books currently stored in the system.
Search Book: Allows the user to find a specific book by its ID or title.
Update Book: Lets the user modify a book’s availability status.
Delete Book: Removes a specific book record from the system.
Data Handling:
All the book records are stored in a List<Book>, which acts as an in-memory database. This allows for efficient storage, retrieval, and management of book data during program execution.
Continuous Loop:
After each operation, the main menu reappears, allowing the user to perform more actions. This loop continues until the user chooses the Exit option, at which point the program terminates gracefully.
Overall, this workflow ensures that the system runs smoothly, providing a logical and organized flow of operations that closely mimics how a real-world library would manage its collection of books.

 Example Output
===== LIBRARY BOOK TRACKING SYSTEM =====
1. Add Book
2. View Books
3. Search Book
4. Update Book
5. Delete Book
6. Exit
Enter your choice: 1

Enter Book ID: 101
Enter Book Title: C# Basics
Enter Author Name: John Doe

 Book added successfully!

===== LIBRARY BOOK TRACKING SYSTEM =====
2
 Library Book List:
ID: 101, Title: C# Basics, Author: John Doe, Available: Yes

 Conclusion
 
The Library Book Tracking System in C# effectively demonstrates how object-oriented programming (OOP) concepts can be applied to design and develop real-world management systems. Through the use of classes, objects, and encapsulation, the system maintains structured and organized data handling, making it easier to manage book-related information within a library environment.
The project uses Lists to store book details dynamically, showcasing the power of C# collections for efficient in-memory data management. By implementing essential operations such as adding, viewing, searching, updating, and deleting books, the project provides a practical simulation of how an actual library management process works in real life.
Beyond its current capabilities, this project serves as a strong foundation for future improvements and scalability. It can be enhanced further by integrating file storage or database systems (such as SQL Server or SQLite) to ensure data persistence even after the program closes. Additional features like a user login system, role-based access (admin or librarian), and book borrowing and returning functionalities can also be implemented to make the system more comprehensive and closer to a professional-grade application.
In conclusion, this project not only demonstrates technical programming skills in C# but also highlights the importance of applying software design principles to solve practical problems efficiently and systematically.

