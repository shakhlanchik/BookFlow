# Software Requirements Specification (SRS)

## 1 Introduction

### 1.1 Purpose

This document, the Software Requirements Specification (SRS), describes the functional and non-functional requirements for the BookFlow application. The purpose of this application is to provide users with a comprehensive and intuitive tool for managing their personal collection of digital books and comfortable reading on various platforms.

### 1.2 Business requirements

#### 1.2.1 Initial Data

Currently, a huge number of people prefer e-books. Users collect extensive digital libraries on their devices, but often encounter problems with organisation and access. E-books are stored in different folders on different devices, and it can be difficult for users to find the book they want or keep track of what page they left off on. Many reading apps require a constant internet connection for synchronisation and also have an inconvenient interface or intrusive advertising. This creates a need for a simple and effective tool to manage one's collection.

#### 1.2.2 Business opportunities

Many users want an application that allows them to easily manage their digital library and read books comfortably, with minimal technical literacy. An app like BookFlow will allow them to spend less time searching for the right book, automatically save their reading progress, and access their collection regardless of internet availability. The interface, designed with a focus on simplicity and convenience for users of all ages, will significantly increase the app's audience.

#### 1.2.3 Project boundaries

The BookFlow app will allow users to import e-books in EPUB and PDF formats, organise them into a personal library, read them with a customisable interface, and track their reading progress. The main functionality (reading and library management) will be available without the need for an internet connection.

### 1.3 Analogues

Analogues include applications such as Moon+ Reader, FBReader, eBoox, and others. A distinctive feature of these analogues is that they provide a wide range of functions for reading and customising the interface. Most of them support various formats and allow data to be synchronised between devices.

However, many of these applications have disadvantages:
- Inconvenient library management: some of them are not well suited for working with large collections, and their cataloguing functions are limited.
- Dependence on the internet: many similar applications actively use cloud services for synchronisation, which makes them less useful when there is no internet connection.
- Advertising: some free versions of similar applications contain intrusive advertising that distracts from the reading process.

The BookFlow project aims to overcome these shortcomings by offering a simple, clean and completely autonomous solution for managing a digital library.

## 2 User requirements

### 2.1 Software interfaces

The BookFlow application uses the following software interfaces:

- Kivy is the main framework that provides an API for creating a user interface, managing events, and ensuring cross-platform compatibility (Android, iOS, Windows, macOS).
- File handling libraries are nessesary to handle various e-book formats, the application will require specialised libraries such as:
  - PyMuPDF (also known as `fitz`) for working with PDF files.
  - PythEpub or a similar library for parsing and displaying EPUB files.

### 2.2 User interface

The application login window.

<img width="570" height="505" alt="image" src="https://github.com/user-attachments/assets/37011c87-9437-490f-b514-bace147cfd5f" />

New user registration window.

<img width="570" height="505" alt="image" src="https://github.com/user-attachments/assets/0d469686-0d5e-4fec-a984-d261138e9e84" />

Login window for registered users.

<img width="570" height="505" alt="image" src="https://github.com/user-attachments/assets/cc351a00-331f-4523-9299-7a87bcfb27ad" />

Main application window.

<img width="570" height="505" alt="image" src="https://github.com/user-attachments/assets/961e752a-50bd-4d6a-9b02-da7006e3ccc8" />

### 2.3 User characteristics

#### 2.3.1 User classes

| User class | Description |
|:----|:----|
| Visitors | Users who do not want to register in the application. They have access to partial functionality. |
| Registered users | Users who have logged into the application under their own name and want to view information about their favourite films, selected according to their preferences, and add reviews to them. They have access to full functionality. |

#### 2.3.2 Application audience

##### 2.3.2.1 Target audience

BookFlow's target audience is people who actively read, collect, and store hundreds of e-books. They often use different sources to obtain content and need to organise this chaos.

##### 2.3.2.2 Secondary audience

The app's secondary audience is people who work with large amounts of educational materials, technical documents, and articles (often in PDF format).

### 2.4 Assumptions and dependencies

1. The application cannot add books to your personal collection without an Internet connection.
1. The application cannot view data about books that have not been added to your personal collection without an Internet connection.

## 3 System requirements

### 3.1 Functional requirements

#### 3.1.1 Main functions

##### 3.1.1.1 Library management

| Function  |  Requirements |
|:----|:----|
| Adding a new book | The application must allow the user to select a file (EPUB or PDF) from the device's file system and add it to the local library. |
| Deleting a book  | The application must allow the user to permanently delete a book from the local library. Confirmation must be requested before deletion. |
| Search and filtering | The application must allow the user to search by title and author, as well as filter the list of books by genre or reading status. |
