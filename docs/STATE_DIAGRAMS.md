# BookFlow - State Diagram

## Overview
This document provides a State Diagram for the BookFlow application. A state diagram is used to model the lifecycle of a single object or component, showing the various states it can be in and the events that cause it to transition from one state to another. For BookFlow, the most complex and stateful component is the **Reader Screen**, which is the subject of this diagram.

## Reader Screen State Diagram

### Description
This diagram models the lifecycle of the `ReaderScreen` component, from the moment a user selects a book until they close it. It covers the crucial asynchronous operation of loading and parsing the book file, the main interactive reading state, the settings customization state, and how the application should behave if the book file is corrupt or unreadable. This model is essential for creating a smooth and resilient reading experience.

### Diagram
![Reader Screen State Diagram](/docs/diagrams/state_diagram.png)

### States and Transitions Explained:

1.  **`Loading` State**:
    *   **Description**: The initial state when a user taps a book in their library. The application is performing an asynchronous operation to open, parse, and prepare the book file (EPUB or PDF) for display.
    *   **UI Behavior**: The screen might show a loading spinner or a placeholder. The reading interface is not yet interactive.
    *   **Transitions**:
        *   `onParseSuccess`: If the book file is successfully parsed, the state transitions to `Reading`.
        *   `onParseFailure`: If the file is corrupt or cannot be read by the parsing library, the state transitions to `Error`.

2.  **`Reading` State**:
    *   **Description**: The primary, interactive state where the user can read the book. The application displays the formatted content and listens for user input to navigate pages. Progress is automatically saved in the background.
    *   **UI Behavior**: The book's content is fully rendered. Page turning gestures (swipes, taps) are active.
    *   **Transitions**:
        *   `user changes page`: An internal action occurs where the new page number is saved to the database. The component remains in the `Reading` state.
        *   `user taps settings icon`: The application prepares to show customization options, transitioning to the `Customizing` state.
        *   `user closes reader`: The final reading position is confirmed, and the component is destroyed, returning the user to the Library screen.

3.  **`Customizing` State**:
    *   **Description**: This state is active when the user is adjusting the appearance of the reader, such as font size, background color, or font type.
    *   **UI Behavior**: A settings menu or an overlay is displayed on top of the reader content. The page-turning gestures may be temporarily disabled.
    *   **Transitions**:
        *   `user confirms settings`: The new settings are applied to the reader view, the overlay is dismissed, and the state returns to `Reading`.
        *   `user cancels/closes settings`: The settings overlay is dismissed without applying changes, and the state returns to `Reading`.

4.  **`Error` State**:
    *   **Description**: A terminal state indicating that the application failed to load the selected book.
    *   **UI Behavior**: An error message is displayed to the user (e.g., an alert or a toast notification) explaining the issue, such as "Could not load book. The file may be corrupt."
    *   **Transitions**:
        *   `user dismisses error`: The user acknowledges the error (e.g., by tapping "OK"). The reader component is closed, and the user is navigated back to the Library screen.
