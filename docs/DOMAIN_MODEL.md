# BookFlow - Domain Model Class Diagram

## Overview
This document describes the key entities and their relationships within the BookFlow application domain, based on the Software Requirements Specification (SRS). This model serves as a conceptual foundation for the system's local SQLite database schema and object-oriented design, focusing on offline, on-device data management.

## Class Diagram Schema

![Class Diagram](/docs/diagrams/domain_model.png)

## Class Diagram Description

The core domain of BookFlow revolves around user profiles, their personal book libraries, and tracking individual reading progress. The main entities are:

*   **`User`**: The central actor. Each user has their own distinct library of books.
*   **`Book`**: Represents a single digital book (EPUB or PDF) that has been imported into the application by a user.
*   **`ReadingProgress`**: An entity that links a specific `User` to a specific `Book` to store data about their reading session, such as the last page they were on.

The following diagram illustrates the relationships between these entities:

### Key Relationships Explained:

1.  **User - Book (One-to-Many)**:
    *   A single `User` profile can own many `Book`s, which collectively form their personal library. Each `Book` is owned by exactly one `User`. This is the core relationship for library management.

2.  **(User, Book) - ReadingProgress (Association)**:
    *   A `ReadingProgress` entity directly links one `User` to one `Book`. This design ensures that each user's progress in a specific book is stored independently. One `User` can have many `ReadingProgress` records (one for each book they have started reading), and one `Book` can also have multiple `ReadingProgress` records if different user profiles on the same device read it.

### Attributes:
*   **`User`**: `userId` (Primary Key), `name`, `createdAt`.
*   **`Book`**: `bookId` (Primary Key), `title`, `author`, `filePath`, `format` (Enum: EPUB, PDF), `userId` (Foreign Key to User), `addedAt`.
*   **`ReadingProgress`**: `progressId` (Primary Key), `currentPage`, `lastReadDate`, `userId` (Foreign Key to User), `bookId` (Foreign Key to Book).

This model provides a clear and robust structure for managing user-specific libraries and progress data locally on a device, ensuring that all information is isolated between profiles and fully available offline.
