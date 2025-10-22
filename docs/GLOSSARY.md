# BookFlow - Glossary of Key Terms

**User Profile**
A local identity within the BookFlow application, identified by a unique user-provided name. It is not an online account and stores all data on the device. Each profile is associated with its own personal library and reading progress.

**Library (Personal Library)**
A user's personal collection of digital books stored within the application. The library is the main screen after login and allows for adding, viewing, searching, and deleting books.

**Book**
The core digital item within the application, representing an e-book file (e.g., EPUB or PDF). Each book object stores its metadata (title, author) and a reference to its file in the application's internal storage.

**Reader View**
The dedicated user interface screen for displaying the contents of a selected book. It provides features for page navigation (swiping, tapping) and appearance customization (font size, background color).

**Reading Progress**
Data that tracks the user's current position within a book, typically the last-read page number. This progress is saved automatically and locally, allowing the user to resume reading from the same spot later.

**Metadata (Book Metadata)**
Descriptive information about a book, such as its title and author. BookFlow attempts to extract this data from the book file upon import to help organize and identify books in the library.

**Book Format (EPUB, PDF)**
The specific file types that BookFlow can import, parse, and display. The application is designed to support standard e-book formats like EPUB and document formats like PDF.

**Kivy**
The open-source Python framework used to build the BookFlow application. It is responsible for creating the cross-platform user interface and managing user interactions on all supported operating systems (Android, iOS, Windows, macOS).

**SQLite Database**
The local, file-based database engine used by BookFlow to store all user data. This includes user profiles, the library catalog (book metadata), and saved reading progress for each book. It enables the application to function entirely offline.
