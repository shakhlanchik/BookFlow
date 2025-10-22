# BookFlow - Deployment Diagram

## Overview
This document provides a Deployment Diagram for the BookFlow application. This diagram illustrates the physical hardware node (the user's device) and shows how the application's software artifacts (the compiled code, local database, and book files) are mapped onto it. It provides a clear view of the application's simple, self-contained runtime architecture.

## Deployment Diagram Schema

![Deployment Diagram](/docs/diagrams/deployment_diagram.png)

## Deployment Diagram Description

The BookFlow application is a standalone, cross-platform application. Unlike a client-server application, all of its components are deployed and run on a single end-user device. There is no external server or cloud infrastructure involved.

### Nodes:

1.  **User's Device**: This represents the end-user's physical hardware, which could be a desktop computer (Windows, macOS), a laptop, or a mobile device (Android, iOS).
2.  **Operating System**: This is the execution environment running on the user's device. It hosts the BookFlow application and manages the underlying file system.

### Artifacts:

*   **BookFlow Application (.exe, .apk, .app)**: This is the primary software artifact—the compiled, executable application built from the Python and Kivy source code. It contains all business logic, the user interface, and file parsing capabilities.
*   **SQLite Database (library.db)**: A single database file stored on the device's local storage. This artifact contains all the user's data, including profiles, the book catalog, and reading progress. It is not a running server but a file that the application reads from and writes to.
*   **Book Files (.epub, .pdf)**: These are the user's e-book files that have been imported into the application. They are copied into the application's private storage area on the device's file system.

### Communication Paths:

1.  **File System I/O (Input/Output)**: This is the primary method of communication. The BookFlow Application interacts directly with the Operating System's file system to:
    *   Read and write data to the `library.db` SQLite file.
    *   Read the content of `.epub` and `.pdf` book files when the user opens them for reading.
