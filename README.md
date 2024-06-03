# Book-Repository
#include <stdio.h>
#include <string.h>

struct Book {
    int id;
    char title[100];
    char author[100];
    int availableCopies;
};

struct Book library[100];
int bookCount = 0;

void addBook() {
    printf("Enter book title: ");
    scanf("%s", library[bookCount].title);
    printf("Enter author name: ");
    scanf("%s", library[bookCount].author);
    printf("Enter number of copies: ");
    scanf("%d", &library[bookCount].availableCopies);
    library[bookCount].id = bookCount + 1;
    bookCount++;
}

void displayBooks() {
    for (int i = 0; i < bookCount; i++) {
        printf("ID: %d, Title: %s, Author: %s, Available Copies: %d\n",
               library[i].id, library[i].title, library[i].author,
               library[i].availableCopies);
    }
}

void searchBook() {
    char title[100];
    printf("Enter book title to search: ");
    scanf("%s", title);
    for (int i = 0; i < bookCount; i++) {
        if (strcmp(library[i].title, title) == 0) {
            printf("Book found: ID: %d, Title: %s, Author: %s, Available Copies: %d\n",
                   library[i].id, library[i].title, library[i].author,
                   library[i].availableCopies);
            return;
        }
    }
    printf("Book not found.\n");
}

void deleteBook() {
    int id;
    printf("Enter book ID to delete: ");
    scanf("%d", &id);
    for (int i = 0; i < bookCount; i++) {
        if (library[i].id == id) {
            library[i] = library[bookCount - 1];  // Replace with the last book
            bookCount--;
            printf("Book deleted.\n");
            return;
        }
    }
    printf("Book not found.\n");
}

void initializeLibrary() {
    strcpy(library[0].title, "1984");
    strcpy(library[0].author, "George Orwell");
    library[0].id = 1;
    library[0].availableCopies = 5;

    strcpy(library[1].title, "To Kill a Mockingbird");
    strcpy(library[1].author, "Harper Lee");
    library[1].id = 2;
    library[1].availableCopies = 3;

    strcpy(library[2].title, "The Great Gatsby");
    strcpy(library[2].author, "F. Scott Fitzgerald");
    library[2].id = 3;
    library[2].availableCopies = 4;

    bookCount = 3;
}

int main() {
    initializeLibrary();
    int choice;
    while (1) {
        printf("1. Add Book\n2. Display Books\n3. Search Book\n4. Delete Book\n5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        switch (choice) {
            case 1: addBook(); break;
            case 2: displayBooks(); break;
            case 3: searchBook(); break;
            case 4: deleteBook(); break;
            case 5: return 0;
            default: printf("Invalid choice\n");
        }
    }
   
    return 0;
}
