# projectOOP-erick
this is my project for the library management system
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// Book storage
class Book {
private:
    string name;
    string genre;
    string author;
    bool isBorrowed;

public:
    Book(string n, string g, string a) : name(n), genre(g), author(a), isBorrowed(false) {}

    void display() const {
        cout << name << " " << genre << " " << author << (isBorrowed ? " (Borrowed)" : "") << endl;
    }

    string getName() const { return name; }
    string getGenre() const { return genre; }
    string getAuthor() const { return author; }
    bool getIsBorrowed() const { return isBorrowed; }
    void setIsBorrowed(bool status) { isBorrowed = status; }
};

// User storage
class User {
private:
    string name;
    string admno;
    string libno;

public:
    User(string n, string t, string a) : name(n), admno(t), libno(a) {}

    void display() const {
        cout << name << " " << admno << " " << libno << endl;
    }

    string getName() const { return name; }
    string getAdmno() const { return admno; }
    string getLibno() const { return libno; }
};

class Library {
private:
    vector<Book> books;
    vector<User> users;

public:
    void addBook(const Book& book) {
        books.push_back(book);
        cout << "Book added successfully." << endl;
    }

    void showBooks() const {
        if (books.empty()) {
            cout << "No books available in the library." << endl;
        } else {
            for (size_t i = 0; i < books.size(); ++i) {
                books[i].display();
            }
        }
    }

    void addUser(const User& user) {
        users.push_back(user);
        cout << "User added successfully." << endl;
    }

    void showUsers() const {
        if (users.empty()) {
            cout << "No users available in the library." << endl;
        } else {
            for (size_t i = 0; i < users.size(); ++i) {
                users[i].display();
            }
        }
    }

    void searchBook(const string& searchTerm) const {
        bool found = false;
        for (size_t i = 0; i < books.size(); ++i) {
            if (books[i].getName() == searchTerm || books[i].getGenre() == searchTerm || books[i].getAuthor() == searchTerm) {
                books[i].display();
                found = true;
            }
        }
        if (!found) {
            cout << "No book found with the search term: " << searchTerm << endl;
        }
    }

    void searchUser(const string& searchTerm) const {
        bool found = false;
        for (size_t i = 0; i < users.size(); ++i) {
            if (users[i].getName() == searchTerm || users[i].getAdmno() == searchTerm || users[i].getLibno() == searchTerm) {
                users[i].display();
                found = true;
            }
        }
        if (!found) {
            cout << "No user found with the search term: " << searchTerm << endl;
        }
    }

    void borrowBook(const string& searchTerm) {
        for (size_t i = 0; i < books.size(); ++i) {
            if ((books[i].getName() == searchTerm || books[i].getGenre() == searchTerm || books[i].getAuthor() == searchTerm) && !books[i].getIsBorrowed()) {
                books[i].setIsBorrowed(true);
                cout << "Book borrowed successfully." << endl;
                return;
            }
        }
        cout << "Book not available for borrowing." << endl;
    }

    void returnBook(const string& searchTerm) {
        for (size_t i = 0; i < books.size(); ++i) {
            if ((books[i].getName() == searchTerm || books[i].getGenre() == searchTerm || books[i].getAuthor() == searchTerm) && books[i].getIsBorrowed()) {
                books[i].setIsBorrowed(false);
                cout << "Book returned successfully." << endl;
                return;
            }
        }
        cout << "Book not found or already returned." << endl;
    }
};

int main() {
    string name, genre, author, searchTerm;
    int choice;
    Library library;

    // Adding predefined books
    Book book1("Inheritance", "Inheritance", "Paul Kariuki");
    Book book2("Chozi La Heri", "Drama", "Jane Omondi");
    Book book3("River and the Source", "Fiction", "Margret A. Ogolla");
    Book book4("Kigogo", "Political", "Pauline Kea");

    library.addBook(book1);
    library.addBook(book2);
    library.addBook(book3);
    library.addBook(book4);

    while (true) {
        cout << "Input the choice you want" << endl;
        cout << "1: add a book" << endl;
        cout << "2: show all books" << endl;
        cout << "3: add a user" << endl;
        cout << "4: show users" << endl;
        cout << "5: search book by name, genre, or author" << endl;
        cout << "6: search user by name, admno, or lib no" << endl;
        cout << "7: borrow a book" << endl;
        cout << "8: return a book" << endl;
        cout << "0: exit" << endl;
        cin >> choice;
        cin.ignore(); // Ignore newline character left in the buffer

        if (choice == 1) {
            cout << "Input the name, genre, and author: " << endl;
            getline(cin, name);
            getline(cin, genre);
            getline(cin, author);
            Book newBook(name, genre, author);
            library.addBook(newBook);
        } else if (choice == 2) {
            library.showBooks();
        } else if (choice == 3) {
            cout << "Input the name, admno, and libno: " << endl;
            getline(cin, name);
            getline(cin, genre); // admno
            getline(cin, author); // libno
            User newUser(name, genre, author);
            library.addUser(newUser);
        } else if (choice == 4) {
            library.showUsers();
        } else if (choice == 5) {
            cout << "Enter the name, genre, or author to search: ";
            getline(cin, searchTerm);
            library.searchBook(searchTerm);
        } else if (choice == 6) {
            cout << "Enter the name, admno, or libno to search: ";
            getline(cin, searchTerm);
            library.searchUser(searchTerm);
        } else if (choice == 7) {
            cout << "Enter the name, genre, or author of the book to borrow: ";
            getline(cin, searchTerm);
            library.borrowBook(searchTerm);
        } else if (choice == 8) {
            cout << "Enter the name, genre, or author of the book to return: ";
            getline(cin, searchTerm);
            library.returnBook(searchTerm);
        } else if (choice == 0) {
            break;
        } else {
            cout << "Invalid choice. Please enter a valid option." << endl;
        }
    }

    return 0;
}
