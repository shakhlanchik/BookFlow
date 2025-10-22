# BookFlow - Component Diagram

## Overview
This document presents the Component Diagram for the BookFlow application. This diagram illustrates the high-level software components that make up the system, their responsibilities, and the interfaces through which they communicate. As BookFlow is a standalone application, this diagram focuses on its internal logical architecture rather than a client-server relationship.

## Component Diagram Schema

![Component Diagram](/docs/diagrams/component_diagram.png)

## Component Diagram Description

The BookFlow system is designed as a monolithic, multi-layered application where all parts run on a single device. It is logically divided into three primary internal components:

### Components:

1.  **User Interface (UI Layer)**:
    *   **Description**: This is the top-level component that the user directly interacts with. It is responsible for rendering all screens, controls (buttons, lists), and visual feedback.
    *   **Technology**: Python, Kivy Framework.
    *   **Key Responsibilities**:
        *   Displaying the welcome screen, user list, and library view.
        *   Rendering the reader view for displaying book content.
        *   Capturing all user input, such as taps, swipes, and text entry.
        *   Delegating user actions to the Application Logic component.

2.  **Application Logic (Business Logic Layer)**:
    *   **Description**: This is the core component that contains the application's business logic. It acts as a coordinator between the UI and the Data Access Layer, processing user requests and managing the application's state.
    *   **Technology**: Python.
    *   **Key Responsibilities**:
        *   Handling user profile management (registration, login).
        *   Orchestrating the process of adding, deleting, and searching for books.
        *   Managing reading sessions, including opening books and tracking progress.
        *   Interfacing with specialized parsing libraries to extract content and metadata from book files.

3.  **Data Access Layer (Persistence Component)**:
    *   **Description**: This component is responsible for all communication with the device's persistent storage. It abstracts the details of data storage from the rest of the application.
    *   **Technology**: Python, SQLite.
    *   **Key Responsibilities**:
        *   Performing CRUD (Create, Read, Update, Delete) operations on the local SQLite database for user profiles, book records, and reading progress.
        *   Managing the physical book files (e.g., copying imported books into the application's internal storage).

### Interfaces:

*   **Internal Method Calls**: Unlike a web application, the primary interfaces in BookFlow are internal. The **UI Layer** communicates with the **Application Logic** layer by calling its public methods (e.g., `logic.add_new_book()`). This is a tightly coupled but highly efficient interface.
*   **Data Access Interface**: The **Application Logic** uses a defined set of functions or methods provided by the **Data Access Layer** to request or save data (e.g., `data_access.save_book_record(book_object)`). This decouples the business logic from the specifics of the database schema.
*   **External Library APIs**: The application interacts with external libraries through their specific APIs. For example, the **Application Logic** uses the API of a book parsing library, and the **Data Access Layer** uses the API of the SQLite driver.
