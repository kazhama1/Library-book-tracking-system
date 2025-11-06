
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
            Console.WriteLine("\n✅ Book added successfully!");
        }

        // Display All Books
        public void ViewBooks()
        {
            Console.WriteLine("\n📚 Library Book List:");
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
                Console.WriteLine("❌ Book not found.");
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
                Console.WriteLine("✅ Book updated successfully!");
            }
            else
            {
                Console.WriteLine("Book not found.");
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
