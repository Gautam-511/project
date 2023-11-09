import java.util.*;

class Book {
    String title;
    String author;
    int ISBN;
    boolean isAvailable;

    public Book(String title, String author, int ISBN) {
        this.title = title;
        this.author = author;
        this.ISBN = ISBN;
        this.isAvailable = true;
    }
}

class User {
    String username;
    String role;

    public User(String username, String role) {
        this.username = username;
        this.role = role;
    }
}

public class LibraryManagementSystem {
    private List<Book> books = new ArrayList<>();
    private List<User> users = new ArrayList<>();

    public void addBook(String title, String author, int ISBN) {
        books.add(new Book(title, author, ISBN));
    }

    public void listBooks() {
        for (Book book : books) {
            System.out.println("Title: " + book.title);
            System.out.println("Author: " + book.author);
            System.out.println("ISBN: " + book.ISBN);
            System.out.println("Availability: " + (book.isAvailable ? "Available" : "Checked Out"));
            System.out.println();
        }
    }

    public void checkOutBook(String username, int ISBN) {
        for (Book book : books) {
            if (book.ISBN == ISBN && book.isAvailable) {
                book.isAvailable = false;
                System.out.println("Book checked out successfully by " + username);
                return;
            }
        }
        System.out.println("Book not found or already checked out.");
    }

    public void returnBook(int ISBN) {
        for (Book book : books) {
            if (book.ISBN == ISBN && !book.isAvailable) {
                book.isAvailable = true;
                System.out.println("Book returned successfully.");
                return;
            }
        }
        System.out.println("Book not found or already available.");
    }

    public static void main(String[] args) {
        LibraryManagementSystem library = new LibraryManagementSystem();
        library.users.add(new User("librarian1", "librarian"));
        library.users.add(new User("member1", "member"));

        library.addBook("Book 1", "Author 1", 12345);
        library.addBook("Book 2", "Author 2", 54321);
        library.addBook("Book 3", "Author 3", 98765);

        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("1. List Books");
            System.out.println("2. Check Out Book");
            System.out.println("3. Return Book");
            System.out.println("4. Exit");
            System.out.print("Select an option: ");

            int choice = scanner.nextInt();
            scanner.nextLine();  // Consume the newline

            switch (choice) {
                case 1:
                    library.listBooks();
                    break;
                case 2:
                    System.out.print("Enter your username: ");
                    String username = scanner.nextLine();
                    System.out.print("Enter the book ISBN: ");
                    int ISBN = scanner.nextInt();
                    library.checkOutBook(username, ISBN);
                    break;
                case 3:
                    System.out.print("Enter the book ISBN: ");
                    ISBN = scanner.nextInt();
                    library.returnBook(ISBN);
                    break;
                case 4:
                    System.out.println("Goodbye!");
                    scanner.close();
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please select a valid option.";
            }
        }
        
    }
}
