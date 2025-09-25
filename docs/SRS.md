# Software Requirements Specification (SRS)

## Table of contents

1 [Introduction](#introduction)

1.1 [Purpose](#purpose)

1.2 [Business requirements](#business-requirements)

1.2.1 [Initial Data](#initial-data)

1.2.2 [Business opportunities](#business-opportunities)

1.2.3 [Project boundaries](#project-boundaries)

1.3 [Analogues](#analogues)

2 [User requirements](#user-requirements)

2.1 [Software interfaces](#software-interfaces)

2.2 [User interface](#user-interface)

2.3 [User characteristics](#user-characteristics)

2.3.1 [User classes](#user-classes)

2.3.2 [Application audience](#application-audience)

2.3.2.1 [Target audience](#target-audience)

2.3.2.2 [Secondary audience](#secondary-audience)

2.4 [Assumptions and dependencies](#assumptions-and-dependencies)

3 [System requirements](#system-requirements)

3.1 [Functional requirements](#functional-requirements)

3.1.1 [Main functions](#main-functions)

3.1.1.1 [Library management](#library-management)

3.1.1.2 [Reading and progress](#reading-and-progress)

3.1.1.3 [Working with files](#working-with-files)

3.1.1.4 [User login to the application](#user-login-to-the-application)

3.1.1.5 [Logged-in user logging out of their account](#logged-in-user-logging-out-of-their-account)

3.1.2 [Restrictions and exclusions](#restrictions-and-exclusions)

3.2 [Non-functional requirements](#non-functional-requirements)

3.2.1 [Quality attributes](#quality-attributes)

3.2.1.1 [Usability requirements](#usability-requirements)

3.2.1.2 [Security requirements](#security-requirements)

3.2.1.3 [Accessibility/availability requirements](#accessibility/availability-requirements)

3.2.2 [External interfaces](#external-interfaces)

3.2.3 [Limitations](#limitations)

<a name="introduction"/>

## 1 Introduction

<a name="purpose"/>

### 1.1 Purpose

This document, the Software Requirements Specification (SRS), describes the functional and non-functional requirements for the BookFlow application. The purpose of this application is to provide users with a comprehensive and intuitive tool for managing their personal collection of digital books and comfortable reading on various platforms.

<a name="business-requirements"/>

### 1.2 Business requirements

<a name="initial-data"/>

#### 1.2.1 Initial Data

Currently, a huge number of people prefer e-books. Users collect extensive digital libraries on their devices, but often encounter problems with organisation and access. E-books are stored in different folders on different devices, and it can be difficult for users to find the book they want or keep track of what page they left off on. Many reading apps require a constant internet connection for synchronisation and also have an inconvenient interface or intrusive advertising. This creates a need for a simple and effective tool to manage one's collection.

<a name="business-opportunities"/>

#### 1.2.2 Business opportunities

Many users want an application that allows them to easily manage their digital library and read books comfortably, with minimal technical literacy. An app like BookFlow will allow them to spend less time searching for the right book, automatically save their reading progress, and access their collection regardless of internet availability. The interface, designed with a focus on simplicity and convenience for users of all ages, will significantly increase the app's audience.

<a name="project-boundaries"/>

#### 1.2.3 Project boundaries

The BookFlow app will allow users to import e-books in EPUB and PDF formats, organise them into a personal library, read them with a customisable interface, and track their reading progress. The main functionality (reading and library management) will be available without the need for an internet connection.

<a name="analogues"/>

### 1.3 Analogues

Analogues include applications such as Moon+ Reader, FBReader, eBoox, and others. A distinctive feature of these analogues is that they provide a wide range of functions for reading and customising the interface. Most of them support various formats and allow data to be synchronised between devices.

However, many of these applications have disadvantages:
- Inconvenient library management: some of them are not well suited for working with large collections, and their cataloguing functions are limited.
- Dependence on the internet: many similar applications actively use cloud services for synchronisation, which makes them less useful when there is no internet connection.
- Advertising: some free versions of similar applications contain intrusive advertising that distracts from the reading process.

The BookFlow project aims to overcome these shortcomings by offering a simple, clean and completely autonomous solution for managing a digital library.

<a name="user-requirements"/>

## 2 User requirements

<a name="software-interfaces"/>

### 2.1 Software interfaces

The BookFlow application uses the following software interfaces:

- Kivy is the main framework that provides an API for creating a user interface, managing events, and ensuring cross-platform compatibility (Android, iOS, Windows, macOS).
- File handling libraries are nessesary to handle various e-book formats, the application will require specialised libraries such as:
  - PyMuPDF (also known as `fitz`) for working with PDF files.
  - PythEpub or a similar library for parsing and displaying EPUB files.

<a name="user-interface"/>

### 2.2 User interface

The application login window.

<img width="570" height="505" alt="image" src="https://github.com/user-attachments/assets/37011c87-9437-490f-b514-bace147cfd5f" />

New user registration window.

<img width="570" height="505" alt="image" src="https://github.com/user-attachments/assets/0d469686-0d5e-4fec-a984-d261138e9e84" />

New user registration window after entering a name that is already registered in the application.

<img width="568" height="505" alt="image" src="https://github.com/user-attachments/assets/d813bafa-c9ec-44c0-a106-3a44bb0f09e5" />

Login window for registered users.

<img width="570" height="505" alt="image" src="https://github.com/user-attachments/assets/cc351a00-331f-4523-9299-7a87bcfb27ad" />

User account login window with incorrect login entry.

<img width="570" height="505" alt="image" src="https://github.com/user-attachments/assets/8a1b5b50-b251-45c9-9f04-1ac4e2a7a733" />

User account login window with incorrect password entry.

<img width="570" height="505" alt="image" src="https://github.com/user-attachments/assets/90d2d5f2-99ed-4fc4-88c0-9e30b78b159b" />

Main application window.

<img width="570" height="505" alt="image" src="https://github.com/user-attachments/assets/961e752a-50bd-4d6a-9b02-da7006e3ccc8" />

<a name="user-characteristics"/>

### 2.3 User characteristics

<a name="user-classes"/>

#### 2.3.1 User classes

| User class | Description |
|:----|:----|
| Visitors | Users who do not want to register in the application. They have access to partial functionality |
| Registered users | Users who have logged into the application under their own name and want to view information about their favourite films, selected according to their preferences, and add reviews to them. They have access to full functionality |

<a name="application-audience"/>

#### 2.3.2 Application audience

<a name="target-audience"/>

##### 2.3.2.1 Target audience

BookFlow's target audience is people who actively read, collect, and store hundreds of e-books. They often use different sources to obtain content and need to organise this chaos.

<a name="secondary-audience"/>

##### 2.3.2.2 Secondary audience

The app's secondary audience is people who work with large amounts of educational materials, technical documents, and articles (often in PDF format).

<a name="assumptions-and-dependencies"/>

### 2.4 Assumptions and dependencies

1. The application cannot add books to your personal collection without an Internet connection.
1. The application cannot view data about books that have not been added to your personal collection without an Internet connection.

<a name="system-requirements"/>

## 3 System requirements

<a name="functional-requirements"/>

### 3.1 Functional requirements

<a name="main-functions"/>

#### 3.1.1 Main functions

<a name="library-management"/>

##### 3.1.1.1 Library management

| Function | Requirements |
|:----|:----|
| Adding a new book | The application must allow the user to select a file (EPUB or PDF) from the device's file system and add it to the local library |
| Deleting a book  | The application must allow the user to permanently delete a book from the local library. Confirmation must be requested before deletion |
| Search and filtering | The application must allow the user to search by title and author, as well as filter the list of books by genre or reading status |

<a name="reading-and-progress"/>

##### 3.1.1.2 Reading and progress

| Function | Requirements |
|:----|:----|
| Opening a book | The application should display the selected book in reading mode, preserving the formatting of the source file |
| Saving progress | The application should automatically save the current reading position (page number or position in the text) when closing the book or exiting the application |
| Turning pages | The application should provide smooth page turning using gestures (swipe) or tapping the edges of the screen |
| Appearance settings | The application should allow the user to change the font size and type, as well as select one of the available colour schemes (e.g. light, dark) |

<a name="working-with-files"/>

##### 3.1.1.3 Working with files

| Function | Requirements |
|:----|:----|
| EPUB support | The application must correctly parse and display standard EPUB files |
| PDF support | The application must correctly display PDF files, allowing the user to zoom in and out on the page |

<a name="user-login-to-the-application"/>

##### 3.1.1.4 User login to the application

| Function | Requirements |
|:----|:----|
| Logging into the application without creating a profile | The application must allow the user to log into the application anonymously |
| New user registration | The application must ask the user to enter a name to create an account. The user must either enter a name or cancel the action |
| A user with that name already exists | The app should notify the user of a registration error and ask them to enter a name. The user should either enter a name or cancel the action |
| Registered user login | The app should provide the user with a list of registered user names. The user should either select their name from the list or cancel the action |

<a name="logged-in-user-logging-out-of-their-account"/>

##### 3.1.1.5 Logged-in user logging out of their account

| Function | Requirements |
|:----|:----|
| Logging out of the account | The application must allow logged-in users to log out of their account and return to the application login window |

<a name="restrictions-and-exclusions"/>

#### 3.1.2 Restrictions and exclusions

The application can only add new books to the collection when connected to the Internet.

<a name="non-functional-requirements"/>

### 3.2 Non-functional requirements

<a name="quality-attributes"/>

#### 3.2.1 Quality attributes

<a name="usability-requirements"/>

##### 3.2.1.1 Usability requirements

The application implements all the basic functions necessary for library management and comfortable reading.
All functional elements of the user interface (buttons, icons) have clear icons or labels describing the action that will occur when they are selected.
The interface is designed to be minimalistic and does not contain unnecessary elements that distract from the reading process.

<a name="security-requirements"/>

##### 3.2.1.2 Security requirements

Since the application stores data locally and does not use accounts, it does not require authentication mechanisms.
The application does not collect or transfer the user's personal data or library metadata to third parties.

<a name="accessibility/availability-requirements"/>

##### 3.2.1.3 Accessibility/availability requirements

The application's response time to user actions (e.g., turning a page or loading a book) should be minimal.
The application must be available for offline use after installation.

<a name="external-interfaces"/>

#### 3.2.2 External interfaces

The application windows are user-friendly:
The font size must be easily adjustable by the user to ensure comfortable reading.
The interface is designed in accordance with a style that looks harmonious on all target platforms, in accordance with the requirements of the Kivy framework.

<a name="limitations"/>

#### 3.2.3 Limitations

The application is implemented for a cross-platform environment (Android, iOS, Windows, macOS).
The language in which the programme is implemented is Python, using the Kivy framework.
A local SQLite database is used to store data about the library and reading progress.
