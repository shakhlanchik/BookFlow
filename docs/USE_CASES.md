# BookFlow - Use Case Analysis

## Actors
1.  **Unregistered User (Guest)**: A user who has not created a profile. They can enter the application anonymously to explore its interface but cannot manage a personal library.
2.  **Registered User**: A user who has created a local profile by providing a name. This actor can access all application features, including adding, managing, and reading books in their persistent personal library.


## Use Case Scenarios

### UC1: Register New User Profile

**Actor:** Unregistered User
**Precondition:** The user is on the application's initial welcome/login screen.
**Flow of Events:**
1.  The user selects the "Register" option.
2.  The application displays a view asking the user to enter a name to create a profile (as per SRS 3.1.1.4).
3.  The user enters their desired name and confirms the action.
4.  The application sends a query to the local SQLite database to check if the provided name already exists in the `users` table.
5.  If the name is unique, the application creates a new record for the user in the `users` table.
6.  The application sets the newly created profile as the active session.
7.  The application navigates the user to the main library screen, which is initially empty.
    **Alternative Flow (A):** User name already exists.
    *   4a. The database query finds an existing user with the same name.
    *   4b. The application displays an error message to the user, such as "A user with that name already exists. Please enter a different name" (as per SRS 3.1.1.4).
    *   4c. The user remains on the registration screen and can either enter a different name or cancel the action.
        **Postcondition:** A new user profile is created and stored in the local application database, and the user is logged into their new account.

![UC1: Register New User Profile](/docs/diagrams/UC1.png)

### UC2: Login as Existing User

**Actor:** Unregistered User
**Precondition:** The user is on the application's login screen, and at least one user profile has been previously created.
**Flow of Events:**
1.  The application queries the local SQLite database and displays a list of all existing user profile names (as per SRS 3.1.1.4).
2.  The user selects their profile name from the list and confirms.
3.  The application validates the selection.
4.  The application sets the selected profile as the active session, loading its associated library and reading progress data.
5.  The application navigates the user to their personal main library screen.
    **Alternative Flow (A):** User cancels login.
    *   2a. The user decides not to log in and clicks a "Cancel" or "Back" button.
    *   2b. The application remains on the initial welcome/login screen.
        **Postcondition:** The application session is associated with the selected user, giving them access to their personal library.

![UC2: Login as Existing User](/docs/diagrams/UC2.png)

### UC3: Add a New Book to the Library

**Actor:** Registered User
**Precondition:** The user is logged in and is viewing their library screen.
**Flow of Events:**
1.  The user clicks the "Add Book" button in the UI.
2.  The application, via the Kivy framework, triggers the operating system's native file chooser dialog.
3.  The user navigates their device's file system and selects a file with a supported format (e.g., `my_book.epub` or `document.pdf`).
4.  The application receives the file path of the selected book.
5.  The application's backend logic performs the following steps:
    a. Validates that the file has a supported extension (`.epub` or `.pdf`).
    b. Copies the selected file into a designated, secure internal storage directory managed by the application.
    c. Uses a specialized library (e.g., `PyMuPDF` for PDF, `PythEpub` for EPUB) to parse the file and extract metadata such as title and author.
    d. Persists a new record in the `books` table of the local SQLite database, storing the metadata and the path to the copied file, associated with the current user's ID.
6.  The application's library view is refreshed to display the new book, typically showing its cover or title.
    **Alternative Flow (A):** Unsupported file format selected.
    *   5a. The application's validation logic detects an unsupported file format (e.g., `.docx`, `.txt`).
    *   5b. The application displays an error notification to the user, such as "Unsupported file format. Please choose an EPUB or PDF file." The operation is aborted.
        **Postcondition:** The book file is integrated into the application's local storage, its metadata is saved, and it is now visible and accessible from the user's library.

![UC3: Add a New Book to the Library](/docs/diagrams/UC3.png)

### UC4: Open and Read a Book

**Actor:** Registered User
**Precondition:** The user is logged in, and at least one book exists in their library.
**Flow of Events:**
1.  From the library screen, the user taps or clicks on a book they wish to read.
2.  The application navigates from the library view to the dedicated reader view.
3.  The application's logic queries the database to retrieve the book's file path and any saved reading progress (e.g., last page number) for that book and user.
4.  The appropriate file parsing library is used to load the content of the book file.
5.  The reader interface is rendered, displaying the book's content starting from the last saved page (or from the beginning if it's the first time reading).
6.  As the user turns pages, the application automatically saves the new page number to the database in the `reading_progress` table.
7.  The user can access controls to change appearance settings (font size, background color).
    **Alternative Flow (A):** User closes the book.
    *   6a. The user clicks a "Back" or "Close" button to exit the reader view.
    *   6b. The application ensures the final reading position is saved to the database.
    *   6c. The application navigates the user back to the library screen.
        **Postcondition:** The user is able to view and navigate the content of the selected book. Their reading progress is tracked automatically for future sessions.

![UC4: Open and Read a Book](/docs/diagrams/UC4.png)
